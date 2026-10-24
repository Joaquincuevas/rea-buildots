# Plan: rea × capacidades estilo Buildots

Estado: propuesta · 2026-10-23 · Todo este documento es **diseño propio (inferencia)**, basado en `docs/00-rea-analisis.md` y `docs/buildots/*`.

## 0. Principios y límites

- **No** se usa rea ni ninguna otra herramienta para hacer ingeniería inversa de Buildots ni de su software. La referencia son solo sus capacidades públicas (ver `DISCLAIMER.md` de rea).
- Se aprovecha de rea lo que es reutilizable y tiene licencia MIT: el **servidor MCP**, los **contratos tipados**, el **ledger de evidencias** (observación / derivación / inferencia / unknown), la supervisión de procesos y el patrón de adaptadores de proveedor.
- Código nuevo **aislado** (`site/`), sin tocar `src/` de upstream, para poder seguir haciendo `git fetch upstream && git merge upstream/main` sin conflictos.
- Estándares abiertos primero: IFC, BCF, P6 XER/XML y MS Project XML.

## 1. Encaje: qué aporta rea

| Necesidad estilo Buildots                            | Pieza de rea reutilizable                                      |
| ---------------------------------------------------- | -------------------------------------------------------------- |
| Copiloto tipo Dot con respuestas trazables           | Servidor MCP (`src/server`, `src/main`) y prompts MCP          |
| "Por qué dice que va retrasado" con evidencia        | `EvidenceLedger`, `InvestigationRecords`, modelo de _unknowns_ |
| Orquestar workers de CV (Python/GPU) de forma segura | `src/process` (procesos propios, deadlines, limpieza)          |
| Esquemas estables para las herramientas del agente   | `src/contracts` + validación ajv                               |
| CLI y MCP con un solo workflow                       | Patrón `src/application` compartido                            |

## 2. Arquitectura propuesta

```
               ┌──────────────── site/ (nuevo) ────────────────┐
captura 360° ─▶│ ingest (Python)  ─▶ object store (S3/MinIO)    │
               │       │                                        │
IFC/BIM  ─────▶│ bim-prep: IfcOpenShell → elementos, geometría,│
P6/MSP   ─────▶│ schedule-prep: XER/XML → WBS, actividades     │
               │       │                                        │
               │ perception (PyTorch, GPU batch)               │
               │  1 keyframes equirect → cubemap               │
               │  2 SfM/VSLAM (COLMAP/hloc) + registro a BIM    │
               │  3 proyección BIM→imagen (raycast, oclusión)   │
               │  4 clasificador estado por elemento×actividad  │
               │  5 fusión temporal + reglas de precedencia     │
               │       │                                        │
               │ progress-store (Postgres + PostGIS/pgvector)   │
               │  element_status(elem, activity, t, p, evid[]) │
               │       │                                        │
               │ analytics: ritmos, forecast, riesgo, EV        │
               └───────┬──────────────────────────────────────┘
                       │ contratos JSON Schema
        ┌──────────────┴──────────────┐
        ▼                             ▼
 rea MCP adapter (TS, site/mcp)   Web UI (visor 360 + xeokit/IFC)
  tools: progress.query,           dashboards, issues
  progress.explain, forecast.run,
  issue.create (BCF/ACC/Procore)
        │
        ▼
  Agente LLM (Claude u otro) = "Dot" con evidencia
```

### Modelo de datos canónico (el activo central)

- `Element(guid_ifc, tipo, planta, zona, geometría)`
- `Activity(id_p6, wbs, tipo_trabajo, precedencias)`
- `ElementActivity(element, activity, peso)` → mapeo BIM ↔ cronograma
- `Observation(capture_id, frame, pose, element, label, score)` → hecho observado
- `ElementStatus(element, activity, fecha, estado, confianza, evidence_ids[])` → derivación
- `Forecast(activity, fecha_fin_p50/p90, ritmo, drivers[])` → inferencia
- Cada respuesta del copiloto cita `evidence_ids`, siguiendo la misma semántica que el ledger de rea.

## 3. MVP (8-10 semanas)

**Objetivo:** en una planta piloto, medir el % completado por actividad para 3 o 4 actividades visibles (tabiquería, placa, pintura, alicatado) y consultarlo por MCP.

| Semana | Entregable                                                                                                                         |
| ------ | ---------------------------------------------------------------------------------------------------------------------------------- |
| 1      | `site/` scaffold; modelo de datos y contratos JSON Schema; docker-compose (Postgres, MinIO)                                        |
| 2      | `bim-prep`: IFC → elementos (IfcOpenShell); `schedule-prep`: MS Project XML / P6 XML                                               |
| 3-4    | Ingesta 360° (Insta360/GoPro .mp4 → keyframes); SfM con COLMAP/hloc; registro manual asistido a BIM (3 o 4 puntos de control)      |
| 5-6    | Proyección BIM→imagen; clasificador base (backbone DINOv2/ConvNeXt + cabeza por clase), etiquetado con CVAT; fusión temporal       |
| 7      | Agregados por actividad y zona; ritmo y forecast lineal (p50)                                                                      |
| 8      | Adaptador MCP en TS reutilizando el patrón de rea: `progress.query`, `progress.explain`, `forecast.run`                            |
| 9-10   | UI mínima (tabla + imagen de evidencia) y validación contra un conteo manual (objetivo: error de % por actividad inferior a 10 pp) |

**Fuera del MVP:** localización automática sin puntos de control, MEP oculto, multi-proyecto, integraciones de escritura.

## 4. Roadmap

- **Fase 1 · Fiabilidad (T+3 meses):** relocalización automática entre rondas; QA humano-en-el-bucle; métricas por clase; desenfoque de caras (RGPD).
- **Fase 2 · Integraciones (T+5):** BCF y _issues_ de ACC (APS API); observaciones de Procore; import P6 XER; webhooks.
- **Fase 3 · Analítica (T+7):** forecast probabilístico (p50/p90) con camino crítico; ranking de subcontratas; earned value y certificación por avance, el hueco que Buildots no cubre.
- **Fase 4 · Copiloto (T+9):** biblioteca de tareas en MCP (equivalente a las tareas de Dot 2026); gráficos; respuestas con citas a la evidencia.
- **Fase 5 · Escala (T+12):** multi-proyecto; benchmarks internos; despliegue self-hosted o on-prem; otras fuentes de captura (LiDAR del móvil, drones).

## 5. Riesgos

- **Datos etiquetados:** no hay datasets públicos de obra activa (https://arxiv.org/pdf/2508.05922). Hay que presupuestar etiquetado propio.
- **Calidad del BIM del cliente:** exigir LOD ≥ 300 y un mapeo de actividades.
- **Registro a BIM:** es el problema técnico más duro (es lo que cubre la patente de Buildots CA3136056A1). Hay que diseñar una solución propia y revisar la libertad de operación (_freedom to operate_) frente a sus patentes antes de comercializar.
- **Merge con upstream:** rea evoluciona muy rápido (4.484 commits). Mantener `site/` desacoplado y depender de rea vía npm (`rea-agents`) cuando sea posible.

## 6. Próximos pasos inmediatos

1. Verificar a mano las URLs marcadas `[?]` en `05-integraciones.md`.
2. Revisar en la USPTO/EPO las patentes de Buildots (freedom to operate).
3. Conseguir 1 IFC + 1 cronograma + 2 rondas 360° de una obra piloto.
4. Scaffold de `site/` con contratos y docker-compose.
