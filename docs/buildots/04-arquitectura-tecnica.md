# 04 · Arquitectura técnica deducible

Leyenda: **[H]** hecho con fuente · **[I]** inferencia. Toda la arquitectura interna es **inferencia**: no hay documentación pública del sistema.

## Hardware y captura
- [H] Cámara 360° montada en el casco, usada durante las rondas habituales. — https://ioplus.nl/archive/en/buildots-supplies-construction-helmets-that-chart-construction-workers-progress/
- [H] Buildots "suministra" los cascos con cámara. — https://innovationorigins.com/en/buildots-supplies-construction-helmets-that-chart-construction-workers-progress
- [H] No se encontró en fuentes públicas el modelo de cámara (GoPro/Insta360) ni soporte de drones, LiDAR o smartphone (búsqueda sin resultados, 2026-10-23).
- [I] Lo más probable es una cámara 360° de consumo con montura propia y subida por Wi-Fi o app móvil al terminar la ronda.

## Pipeline de datos (inferencia)
```
casco 360° ──upload──▶ ingesta (object storage) ──▶ cola de trabajos
   │                                             │
   └─ metadatos (proyecto, planta, fecha)         ▼
                                    GPU workers: keyframes → localización
                                    → proyección BIM → clasificación estado
                                                 │
                         QA humano (opcional) ◀──┤
                                                 ▼
             BD de progreso (elemento × actividad × fecha) ─▶ agregados / KPIs
                                                 │
     ┌───────────────┬───────────────┬───────────┴───────┐
     ▼               ▼               ▼                   ▼
 Dashboard web   Delay Forecast   Dot (LLM + tools)   Integraciones (ACC issues)
```
- Entradas estáticas: modelo BIM (importado desde ACC/BIM 360, https://marketplace.autodesk.com/apps/5d0214e5-9653-4142-98ff-e3329a6b07ad) y cronograma.
- [I] Preprocesado BIM: extracción de geometría y propiedades por elemento, mapeo elemento ↔ actividad del cronograma (por WBS o reglas, con configuración asistida por el equipo de onboarding; G2 menciona un "setup inicial lento": https://g2.com/products/buildots-buildots/reviews).

## Cloud y stack (según ofertas de empleo)
- [H] Backend en **Python** sobre cloud moderna, **AWS preferido**. — https://jobs.tlv.partners/companies/buildots/jobs/83767807-senior-backend-engineer
- [H] Investigación con **PyTorch** (antes TensorFlow/PyTorch) y Python; datos visuales y 3D. — https://buildots.com/careers/co/research/CD.A5B/deep-learning-researcher · https://jobs.tlv.partners/companies/buildots/jobs/29426783-deep-learning-researcher
- [H] LLM: OpenAI GPT-4o (versión segura). — https://buildots.com/blog/meet-dot-buildots-ai-assistant/
- [I] Probable: S3 + colas (SQS/Batch) + instancias GPU (EC2/EKS) para la inferencia por lotes; Postgres para el modelo de progreso; frontend web SPA con visor 360° y visor BIM (con probabilidad, un visor WebGL de tipo xeokit, IFC.js o Autodesk APS Viewer; no verificado).
- [I] Procesado **batch** (horas), no en tiempo real: el valor está en la cadencia semanal o diaria.

## Seguridad y datos
- [H] Datos agregados y anonimizados de cientos de proyectos alimentan el Intelligence Lab. — https://www.prnewswire.com/news-releases/buildots-launches-intelligence-lab-constructions-first-ai-powered-research-hub-302810700.html
- [I] Implica cláusulas contractuales de uso de datos entre clientes. Es un punto a revisar en cualquier compra, y también en nuestro diseño.

## Lecciones de arquitectura para nuestro proyecto
- Separar con claridad: **captura → percepción (CV) → modelo de progreso canónico → analítica → interfaz (UI/LLM)**.
- El activo diferencial no es el modelo de CV, sino el **modelo de datos de progreso** (elemento × actividad × tiempo) y su histórico entre proyectos.
- El LLM se sitúa encima, como capa de consulta y análisis con herramientas, y no sustituye a la CV.
