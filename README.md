# rea-buildots

Fork privado de [morluto/rea](https://github.com/morluto/rea) (MIT) más una investigación de fuentes públicas sobre [Buildots](https://buildots.com) y un plan para combinar ambos.

- **rea**: servidor MCP y CLI de análisis con evidencia trazable. El README original está en [`README.rea.md`](README.rea.md).
- **Objetivo**: reutilizar el framework MCP y de evidencias de rea para una capa de *site intelligence* estilo Buildots (progreso de obra por visión artificial contra BIM y cronograma).
- **Límite**: no se hace ingeniería inversa de software propietario; solo se usan fuentes públicas.

## Relación con upstream
```bash
git fetch upstream
git merge upstream/main   # el código nuevo vive aparte (site/), así que no hay conflictos con src/
```

## Índice
| Doc | Contenido |
|---|---|
| [docs/00-rea-analisis.md](docs/00-rea-analisis.md) | Licencia, propósito, stack y arquitectura de rea |
| [docs/buildots/01-empresa.md](docs/buildots/01-empresa.md) | Historia, fundadores, financiación, clientes, mercados |
| [docs/buildots/02-producto-modulos.md](docs/buildots/02-producto-modulos.md) | Módulos, flujo en obra, dashboards, precios |
| [docs/buildots/03-ia-modelos.md](docs/buildots/03-ia-modelos.md) | CV, BIM y cronograma, patentes, forecast, Dot (GenAI) |
| [docs/buildots/04-arquitectura-tecnica.md](docs/buildots/04-arquitectura-tecnica.md) | Hardware, pipeline y stack deducido |
| [docs/buildots/05-integraciones.md](docs/buildots/05-integraciones.md) | Autodesk, Procore, P6, MS Project, IFC |
| [docs/buildots/06-casos-uso-roi.md](docs/buildots/06-casos-uso-roi.md) | Casos, métricas de ROI y limitaciones |
| [docs/buildots/07-competidores.md](docs/buildots/07-competidores.md) | OpenSpace, Disperse, Doxel, DroneDeploy, Reconstruct… |
| [docs/buildots/08-fuentes.md](docs/buildots/08-fuentes.md) | Todas las URLs con fecha de consulta |
| [docs/integracion/plan-rea-x-buildots.md](docs/integracion/plan-rea-x-buildots.md) | Arquitectura propuesta, MVP y roadmap |
| [research/raw/](research/raw/) | Notas y extractos en bruto |

Convención en los docs: **[H]** = hecho con fuente · **[I]** = inferencia · **[?]** = fuente secundaria no verificada.

## Licencia
El código de rea es MIT (© 2026 morluto, ver [LICENSE](LICENSE)). Las aportaciones propias mantienen la misma licencia, salvo que se indique otra cosa.
