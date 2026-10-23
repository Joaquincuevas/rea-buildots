# 02 · Producto y módulos

Leyenda: **[H]** hecho con fuente · **[I]** inferencia.

## Flujo de trabajo en obra
1. [H] Un trabajador lleva una **cámara 360° montada en el casco** durante sus rondas habituales por la obra, a diario o cada semana. — https://www.theconstructionindex.co.uk/news/view/bim-cams-for-builders?amp=1 · https://ioplus.nl/archive/en/buildots-supplies-construction-helmets-that-chart-construction-workers-progress/
2. [H] Las imágenes se suben y se procesan con algoritmos propios, patentados o en trámite. — https://www.londonbuildexpo.com/news/builders-could-soon-be-wearing-cameras-on-their-hard-hats-to-gather-data-that-automatically-updates-project-plans
3. [H] La visión artificial localiza cada captura dentro del edificio, identifica los elementos instalados y los compara con el **BIM** y el **cronograma**. — https://ccsbestpractice.org.uk/entries/buildots-4d-modelling-engine/
4. [H] Resultado: un gemelo digital "diseño vs. cronograma vs. realidad" con imágenes 360°, informes de estado y discrepancias. — https://www.pbctoday.co.uk/news/digital-construction-news/bim-news/construction-productivity-bim/98470/
5. [I] La captura es **pasiva**: no hay rutas guiadas ni marcado manual, así que el coste marginal por captura para el cliente es bajo.

## Módulos

### Progress Tracking (núcleo)
- [H] Seguimiento del progreso a nivel de **elemento** del modelo, combinando datos objetivos de varias fuentes. — https://buildots.com/product/
- [H] Determina automáticamente el estado de cada elemento del modelo que aparece en las capturas. — https://www.unite.ai/?p=368621
- [I] Granularidad típica: elemento × actividad (p. ej., muro: tabiquería → placa → cinta → pintura), agregada por planta y zona.

### Plan Tracker (jul-2023)
- [H] **Workplan**: divide el cronograma en tareas, asigna fechas, se comparte con los subcontratistas y compara lo ejecutado con lo planificado. — https://bimplus.co.uk/buildots-launches-task-and-milestone-monitoring-suite
- [H] **Targets**: hitos críticos y avance hacia ellos, incluido el rendimiento de cada subcontrata y la cadena de suministro. — https://constructionmanagement.co.uk/buildots-launches-task-and-milestone-monitoring-suite/
- [H] Se inspira en la metodología **Lean Construction**. — https://www.international-construction.com/news/buildots-introduces-new-ai-powered-tools-to-combat-construction-delays/8030093.article

### Delay Forecast (may-2024)
- [H] Integrado en el dashboard: marca las actividades en riesgo, proyecta el retraso probable y sugiere correcciones de ritmo. — https://www.vktr.com/the-wire/buildots-unveils-ai-powered-forecasting-tool-to-mitigate-construction-delays/
- [H] Análisis de causa raíz por actividad, simulación "what-if" con nuevos ritmos y tendencia semanal del riesgo. — https://www.ironpros.com/home/product/22910159/buildots-buildots-launches-ai-forecasting-for-construction-delays
- [H] Probado en beta en un complejo gubernamental de NCC Dinamarca. — https://www.theconstructionindex.co.uk/news/view/ai-tool-predicts-hold-ups

### Dot: asistente de IA generativa (oct-2024 → upgrade oct-2026)
- [H] Responde en lenguaje natural preguntas de estado. Ejemplo: "pisos con trasdosado cerrado y alicatado de baño sin empezar". — https://bimplus.co.uk/buildots-launches-dot-genai-assistant
- [H] Upgrade de 2026: biblioteca de **tareas** preconfiguradas (revisar un retraso previsto, verificar lo que reclama una subcontrata, comparar el rendimiento entre zonas), gráficos en el chat, soporte 24/7 y sin coste adicional. — https://www.prnewswire.com/il/news-releases/buildots-upgrades-dot-turning-its-ai-assistant-into-an-on-demand-construction-analyst-for-project-teams-302915371.html

### Gestión de incidencias y desviaciones
- [H] Las desviaciones (por ejemplo, una instalación incorrecta) se registran como *issues* con evidencia visual y se sincronizan con BIM 360 y Autodesk Build. — https://www.cimdata.com/en/industry-summary-articles/item/25956-buildots-announces-integration-with-autodesk-bim-360-to-automate-field-management-issues-creation · https://iotm2mcouncil.org/iot-library/news/smart-building-construction-news/buildots-increases-autodesk-integration/

### Intelligence Lab (jun-2026)
- [H] Centro de investigación gratuito con IA sobre datos agregados y anonimizados de cientos de proyectos. — https://www.prnewswire.com/news-releases/buildots-launches-intelligence-lab-constructions-first-ai-powered-research-hub-302810700.html
- [H] Informe de benchmarks globales (8-oct-2026) con referencias de producción para 21 actividades. — https://www.prnewswire.com/il/news-releases/nearly-40-of-planned-weekly-work-on-construction-sites-isnt-delivered-new-buildots-intelligence-lab-global-benchmarks-report-302902316.html
- [I] Funciona como marketing basado en datos y como foso defensivo (efecto red de datos entre proyectos).

## Dashboards, informes y alertas
- [H] Dashboard con el estado más reciente, imágenes 360° y discrepancias de diseño o cronograma. — https://www.pbctoday.co.uk/news/digital-construction-news/bim-news/construction-productivity-bim/98470/
- [H] Alertas de actividades en riesgo y tendencias semanales en Delay Forecast. — https://www.vktr.com/the-wire/buildots-unveils-ai-powered-forecasting-tool-to-mitigate-construction-delays/
- [H] Reseña G2: los usuarios piden más control sobre informes y dashboards. — https://g2.com/products/buildots-buildots/reviews
- [I] Las vistas probables son: % completado por actividad y zona, curva planificado vs. real, ranking de subcontratas, mapa de calor por planta y feed de imágenes navegable sobre el plano.

## Modelo de negocio y precios
- [H] No hay precios públicos; hay que "contactar con el proveedor". — https://www.capterra.com/p/210802/Buildots/ · https://www.trustradius.com/products/buildots/pricing
- [H] Capterra indica precio "por usuario", basado en los **m² totales del proyecto**. — https://www.capterra.co.uk/software/210802/buildots
- [H] Suscripción según tamaño y complejidad del proyecto. — https://dealroom.launchvic.org/companies/buildots
- [H] El CEO reconoce: "frente a otras soluciones con cámaras 360°, somos caros". — https://www.thefuture3d.com/software/buildots
- [H] Sin versión de prueba gratuita. — https://www.capterra.com/p/210802/Buildots/
- [I] SaaS enterprise por proyecto o portfolio, con hardware incluido y customer success dedicado (ofertas de CSM). Es un modelo *land & expand* hacia todo el portfolio del cliente.
