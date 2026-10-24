# 03 · IA y modelos

Leyenda: **[H]** hecho con fuente · **[I]** inferencia. Buildots no publica papers técnicos (no se encontró ninguno); casi todo el detalle técnico es inferencia a partir de patentes, ofertas de empleo y literatura académica.

## Lo que se sabe

- [H] La CV localiza la captura en el edificio, detecta los elementos instalados y los compara con el BIM y el cronograma. — https://ccsbestpractice.org.uk/entries/buildots-4d-modelling-engine/
- [H] Estado por elemento del modelo mediante "wearable cameras and computer vision algorithms". — https://www.unite.ai/?p=368621
- [H] Las ofertas de investigación hablan de "deep learning y computer vision sobre datos visuales y **3D** de obra". — https://jobs.tlv.partners/companies/buildots/jobs/81785536-senior-deep-learning-researcher · https://buildots.com/careers/co/research/CD.A5B/deep-learning-researcher
- [H] Dot usa una versión segura de **GPT-4o de OpenAI**, entrenada o ajustada por Buildots; la CV es un modelo aparte. — https://buildots.com/blog/meet-dot-buildots-ai-assistant/ · https://bimplus.co.uk/buildots-launches-dot-genai-assistant
- [H] Dot interpreta la petición y **consulta la base de datos del proyecto** (patrón text-to-query/tool use). — https://www.theconstructionindex.co.uk/news/view/buildots-launches-ai-assistant-for-site-managers
- [H] Delay Forecast proyecta retrasos a partir de los ritmos medidos y permite simular ritmos nuevos. — https://www.ironpros.com/home/product/22910159/buildots-buildots-launches-ai-forecasting-for-construction-delays

## Patentes (indicios del método)

| Nº                | Título                                                                                     | Fecha                      | Estado    | Fuente                                           |
| ----------------- | ------------------------------------------------------------------------------------------ | -------------------------- | --------- | ------------------------------------------------ |
| CA3136056A1       | Construction project tracking (familia: "Determining position of an image capture device") | prioridad 2019-04-02       | publicada | https://patents.google.com/patent/CA3136056A1/de |
| US-20240005556-A1 | System and method for assessing imaged object location                                     | 1ª presentación 2020-05-21 | pendiente | https://pitchbook.com/profiles/company/339838-66 |
| US-20230185978-A1 | Interactive GUI for presenting construction information                                    | 2021-12-14                 | pendiente | https://pitchbook.com/profiles/company/339838-66 |

- [I] Los títulos apuntan a tres piezas: (1) **localización de la cámara** en el modelo, (2) decidir si un objeto observado está en la posición del elemento BIM y (3) la UI de presentación.

## Pipeline probable de CV (inferencia)

1. **Ingesta de vídeo 360°** (equirectangular) y extracción de keyframes con su timestamp.
2. **Localización / SLAM visual**: SfM/VSLAM relativo por ronda y registro al sistema de coordenadas del BIM, con anclas aprendidas de rondas anteriores y alineación con geometría del modelo (la patente de 2019 se centra en la posición de la cámara).
3. **Reconstrucción 3D** escasa o densa (SfM/MVS o profundidad monocular) que permite proyectar elementos BIM sobre cada imagen.
4. **Proyección BIM → imagen**: para cada elemento visible se calcula una máscara esperada (renderizado del IFC/Revit con la pose estimada) y se gestionan las oclusiones.
5. **Clasificación de estado por elemento y actividad**: una red de segmentación o clasificación sobre el recorte proyectado (p. ej., "estructura", "placa", "cinta", "pintado"). Lo más probable es multi-vista y temporal, con agregación entre rondas y restricciones de precedencia (no puede haber pintura sin placa).
6. **Control de calidad humano-en-el-bucle** (inferencia; competidores como Disperse lo declaran abiertamente: https://www.constructiondive.com/news/openspace-acquires-disperse-contech-merger/804410/).
7. **Agregación**: el estado por elemento se convierte en % por actividad, zona y planta, y se mapea a las tareas del cronograma (WBS ↔ elementos).

- Literatura de apoyo (no es de Buildots):
  - Segmentación 3D en obra activa, escasez de datasets: https://arxiv.org/pdf/2508.05922
  - Nube de puntos → grafo → clasificación → matching con BIM (Georgia Tech): https://rical.ce.gatech.edu/research_23.html
  - Detección 2D + modelo pinhole + BIM para as-built (CONVR 2023): https://media.fupress.com/files/pdf/24/14498/39659
  - GroundingDINO + SAM para elementos de construcción (ISARC 2025): https://www.iaarc.org/publications/fulltext/026_Enhancing_Robotic_Vision_through_Deep_Learning_Techniques__From_Detection_to_Construction.pdf

## Analítica predictiva (inferencia)

- Las series temporales de producción por actividad y zona permiten estimar ritmos y proyectar el fin con el ritmo actual, comparándolo con el planificado.
- Modelo de riesgo: ritmo, varianza, dependencias del cronograma (camino crítico) y benchmarks de otros proyectos (Intelligence Lab).
- Datos que lo sustentan: "62 % de actividades van más lentas de lo planificado" (https://www.vktr.com/the-wire/buildots-unveils-ai-powered-forecasting-tool-to-mitigate-construction-delays/); "solo el 29,3 % de las actividades empiezan a tiempo" (https://www.prnewswire.com/il/news-releases/nearly-40-of-planned-weekly-work-on-construction-sites-isnt-delivered-new-buildots-intelligence-lab-global-benchmarks-report-302902316.html).

## IA generativa / copiloto

- [H] Dot v1 (2024): Q&A en lenguaje natural sobre los datos del proyecto, con preguntas de seguimiento. — https://www.cdomagazine.tech/others/buildots-launches-dot-first-genai-assistant-to-answer-real-construction-status-queries
- [H] Dot v2 (2026): agente con biblioteca de tareas y gráficos en el chat. — https://www.prnewswire.com/il/news-releases/buildots-upgrades-dot-turning-its-ai-assistant-into-an-on-demand-construction-analyst-for-project-teams-302915371.html
- [I] Arquitectura probable: un LLM con herramientas (SQL o API sobre el modelo de datos de progreso), plantillas de análisis predefinidas y un renderizador de gráficos. **Este es el punto donde rea (MCP + ledger de evidencias) encaja mejor.**

## Huecos

- No hay métricas públicas de precisión (accuracy/recall) del reconocimiento por elemento.
- No consta qué ocurre con los elementos ocultos (MEP en falso techo) ni con las fases sin cambio visual.
- No hay evaluación independiente del "hasta un 50 % menos de retrasos".
