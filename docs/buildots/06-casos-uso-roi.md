# 06 · Casos de uso y ROI declarado

Leyenda: **[H]** hecho con fuente · **[I]** inferencia. **Todas las métricas son del proveedor o de sus clientes; ninguna está auditada de forma independiente.**

## Métricas citadas

| Métrica                                  | Valor                                             | Contexto                     | Fuente                                                                                                                                                                                  |
| ---------------------------------------- | ------------------------------------------------- | ---------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Reducción de retrasos                    | "hasta un 50 %"                                   | Claim de marketing           | https://www.theconstructionindex.co.uk/news/view/ai-tool-predicts-hold-ups · https://careers.viola-group.com/companies/buildots/jobs/71149919-construction-customer-success-manager     |
| Ahorro en retrabajo                      | 4,3 % por fab                                     | Caso Intel                   | https://pages.buildots.com/hubfs/Intel-case%20study-08-Insights.pdf                                                                                                                     |
| Retraso evitado                          | 4 semanas por fab                                 | Caso Intel                   | https://pages.buildots.com/intel-case-study                                                                                                                                             |
| Actividades más lentas de lo planificado | 62 %                                              | Investigación interna (2024) | https://www.vktr.com/the-wire/buildots-unveils-ai-powered-forecasting-tool-to-mitigate-construction-delays/                                                                             |
| Actividades que empiezan a tiempo        | 29,3 %                                            | Benchmarks 2026              | https://www.prnewswire.com/il/news-releases/nearly-40-of-planned-weekly-work-on-construction-sites-isnt-delivered-new-buildots-intelligence-lab-global-benchmarks-report-302902316.html |
| Trabajo semanal planificado no entregado | 37 %                                              | Benchmarks 2026              | ídem                                                                                                                                                                                    |
| Trabajo activo que va en plazo           | 52,8 %                                            | Benchmarks 2026              | ídem                                                                                                                                                                                    |
| Mejor mes vs. semana típica              | 1,8× más rápido                                   | Benchmarks 2026              | ídem                                                                                                                                                                                    |
| Cumplimiento por vertical                | Sanidad 65 %, data centers ~57 %, educación <39 % | Benchmarks 2026              | ídem                                                                                                                                                                                    |
| Brecha MEP en data centers               | 20-50 % entre lo planificado y lo entregado       | Intelligence Lab (jun-2026)  | https://www.enr.com/articles/63235-buildots-launches-intelligence-lab-an-ai-powered-project-data-research-hub                                                                           |
| Crecimiento de ingresos                  | ×3 anual durante varios años                      | Compañía                     | https://www.ynetnews.com/business/article/bkvw3ybkfx                                                                                                                                    |

## Casos de uso

- [H] **Seguimiento semanal de producción por subcontrata** (Workplan/Targets); EllisDon: "identifico hitos críticos y monitorizo el avance". — https://bimplus.co.uk/buildots-launches-task-and-milestone-monitoring-suite
- [H] **Predicción de retrasos** y simulación de ritmos (NCC Dinamarca, beta). — https://www.theconstructionindex.co.uk/news/view/ai-tool-predicts-hold-ups
- [H] **Detección de desviaciones** y su envío como _issue_ a ACC/BIM 360. — https://www.cimdata.com/en/industry-summary-articles/item/25956-buildots-announces-integration-with-autodesk-bim-360-to-automate-field-management-issues-creation
- [H] **Integración en el pipeline BIM** (Build Group con Navisworks). — https://enr.com/articles/52262-build-group-sees-results-with-site-intelligence-app-buildots
- [H] **Verificar lo que reclama una subcontrata** (tarea de Dot 2026). — https://www.prnewswire.com/il/news-releases/buildots-upgrades-dot-turning-its-ai-assistant-into-an-on-demand-construction-analyst-for-project-teams-302915371.html
- [H] **Rascacielos en Nueva York** con apoyo de Buildots. — https://archive.israel21c.org/israeli-ai-construction-tech-helps-build-nyc-skyscraper/
- [H] **Megaproyectos**: fabs de Intel, centros de datos (Digital Realty, Green Mountain). — https://www.prnewswire.com/news-releases/buildots-raises-130m-to-bring-ai-to-the-16t-construction-industry--and-power-the-global-data-center-buildout-302877516.html

## Cálculo de ROI ilustrativo (inferencia)

- Proyecto de $200M y 24 meses, con coste indirecto (overhead + financiación) de ~$150-250k por semana.
- 4 semanas evitadas → **$0,6-1,0M**; 4,3 % de retrabajo evitado sobre una partida de retrabajo del ~5 % → efecto pequeño en coste directo.
- [I] Solo es plausible frente a una suscripción enterprise de seis cifras en megaproyectos. En proyectos pequeños el ROI se diluye, lo que cuadra con el foco en data centers y fabs.

## Limitaciones y críticas

- [H] G2: solo 2 reseñas (3,5/5). Críticas: personalización limitada, setup inicial lento, sin trial, faltan seguimiento de presupuesto y acceso móvil. — https://g2.com/products/buildots-buildots/reviews
- [H] Capterra: 0 reseñas; sin prueba gratuita. — https://www.capterra.com/p/210802/Buildots/
- [H] Los resultados de Intel proceden de Buildots, no de un análisis auditado. — https://www.remio.ai/ja/post/buildots-funding-round-adds-130-million-as-mega-projects-test-construction-ai-ja
- [H] Caro frente a otras soluciones 360° (palabras del propio CEO). — https://www.thefuture3d.com/software/buildots
- [I] **Dependencia del BIM**: sin un modelo LOD 300-350 bien estructurado y vinculado al cronograma, el valor cae mucho.
- [I] **Elementos ocultos o no visibles** (MEP tras el falso techo, instalaciones enterradas, calidad no visual) quedan fuera del alcance de una cámara RGB.
- [I] **Granularidad temporal** limitada por la frecuencia de las rondas.
- [I] **Sin pago por avance ni earned value** expuesto en ERP (no consta en ninguna fuente).
- [I] **Lock-in de hardware y proceso**; la adopción depende de la disciplina de captura (el podcast admite que al principio el 90 % de usuarios no obtenía valor).
- [I] **Privacidad laboral**: las cámaras en el casco graban a los trabajadores, lo que en la UE exige base legal RGPD y desenfoque de caras. No hay información pública al respecto.
