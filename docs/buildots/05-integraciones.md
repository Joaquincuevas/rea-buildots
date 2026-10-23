# 05 · Integraciones

Leyenda: **[H]** hecho con fuente · **[I]** inferencia · **[?]** solo fuente secundaria, no verificada.

| Sistema | Estado | Qué hace | Fuente |
|---|---|---|---|
| Autodesk BIM 360 (Docs) | [H] | Importa los modelos directamente desde BIM 360 o ACC Docs | https://marketplace.autodesk.com/apps/5d0214e5-9653-4142-98ff-e3329a6b07ad |
| Autodesk BIM 360 (Issues) | [H] oct-2024 | Las desviaciones se crean automáticamente como *issues* con evidencia visual | https://www.cimdata.com/en/industry-summary-articles/item/25956-buildots-announces-integration-with-autodesk-bim-360-to-automate-field-management-issues-creation |
| Autodesk Build / ACC (Forma Build) | [H] ago-2025 | Sincroniza las *issues* de Buildots con Autodesk Build; disponible para todos los clientes | https://iotm2mcouncil.org/iot-library/news/smart-building-construction-news/buildots-increases-autodesk-integration/ · https://www.autodesk.com/integrations/partner/buildots |
| Revit | [H] (indirecto) | Build Group enlazó sus modelos Navisworks con gemelos digitales en el "entorno Revit" de Buildots | https://enr.com/articles/52262-build-group-sees-results-with-site-intelligence-app-buildots |
| Navisworks | [H] (indirecto) | Mismo caso Build Group | https://enr.com/articles/52262-build-group-sees-results-with-site-intelligence-app-buildots |
| Procore | [?] | Listado como integración | https://aidirectory.aecmag.com/?p=373 |
| Primavera P6 | [?] | Listado como integración | https://aidirectory.aecmag.com/?p=373 |
| MS Project | [?] | Listado como integración | https://aidirectory.aecmag.com/?p=373 |
| Synchro 4D, Revizto | [?] | Listados como integraciones | https://aidirectory.aecmag.com/?p=373 |
| IFC | [?] sin evidencia | No se encontró ninguna mención pública a la importación de IFC | búsqueda 2026-10-23 sin resultados |

## Notas
- [H] La app de BIM 360 es gratuita, pero la integración requiere suscripción de pago a Buildots. — https://apps.autodesk.com/BIM360/RP/List/Search?page=3
- [I] Para el cronograma hay que importar al menos P6 (XER/XML) y MS Project (MPP/XML), porque son los formatos del mercado objetivo (GC enterprise). Que el producto acepte ambos es muy probable, pero no está verificado.
- [I] En IFC: si aceptan modelos de ACC, la conversión pasa por Autodesk APS (Model Derivative), que también admite IFC. Es probable, pero no está confirmado.
- [I] Las integraciones conocidas son **salientes** de incidencias y **entrantes** de diseño. No consta ninguna exportación de % completado a ERP o certificaciones (pago por avance), y es un hueco claro.

## Implicaciones para nuestro plan
- Mínimo viable: **IFC** (abierto, con IfcOpenShell), **P6 XER/XML** y **MS Project XML**, más la API de **ACC/APS** (OAuth de 3 patas, Data Management + Model Derivative + Issues).
- Procore: REST API pública (Projects, Observations, Schedule) para crear observaciones con evidencia.
