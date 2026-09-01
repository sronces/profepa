# 22. Análisis de información transaccional y Business Intelligence (BI)

Las Minutas No. 03 solicitan explícitamente presentar una estrategia de
explotación de información, reporteo y generación de indicadores
mediante Business Intelligence. Esta necesidad debe incorporarse como
una capacidad arquitectónica del proyecto, no como un conjunto de
reportes aislados al final del desarrollo.

## 22.1 ¿Qué aporta BI a SAAEL?

-   Convertir transacciones operativas en información para supervisión,
    dirección y mejora de procesos.

```{=html}
<!-- -->
```
-   Medir tiempos de ciclo, cargas de trabajo, vencimientos,
    prevenciones, subsanaciones, resoluciones, auditorías, renovaciones
    y comportamiento de indicadores.

```{=html}
<!-- -->
```
-   Analizar tendencias históricas por periodo, entidad, instalación,
    materia, tipo de trámite, estado, auditor, región y unidad
    administrativa, sujeto a autorización.

```{=html}
<!-- -->
```
-   Identificar cuellos de botella y variaciones anómalas mediante
    comparación contra metas, históricos o líneas base.

```{=html}
<!-- -->
```
-   Dar trazabilidad desde un indicador hasta el conjunto de
    transacciones que lo sustentan.

```{=html}
<!-- -->
```
-   Permitir autoservicio controlado sin que cada usuario construya su
    propia definición de KPI.

```{=html}
<!-- -->
```
-   Facilitar reportes ejecutivos, operativos, regulatorios y de
    auditoría con una fuente gobernada.

```{=html}
<!-- -->
```
-   Preparar la plataforma para analítica avanzada, pronósticos y
    detección de anomalías sin alterar el sistema transaccional.

## 22.2 Casos de análisis transaccional prioritarios

  Dominio                   Preguntas analíticas                                                                              Nivel
  ------------------------- ------------------------------------------------------------------------------------------------- -------------------------
  Gestión de trámites       Entradas, estados, tiempos de permanencia, prevenciones, subsanaciones, cierres y resoluciones.   Operativo / ejecutivo
  SLA y plazos              Tiempo transcurrido, días hábiles, vencimientos próximos, retrasos y cumplimiento por unidad.     Operativo
  Carga de trabajo          Expedientes por responsable, materia, estado, región y antigüedad.                                Operativo
  Auditores                 Participación, tiempos, materias, resultados y, si se aprueba, evaluación de servicio.            Ejecutivo / supervisión
  RDA                       Solicitudes, elegibilidad, indicadores, renovaciones, cumplimiento anual y pérdida de vía.        Regulatorio / ejecutivo
  No conformidades          Frecuencia, severidad, materias, acciones, tiempos de cierre y recurrencia.                       Analítico
  Integraciones             Disponibilidad, errores, tiempos de respuesta, reintentos y transacciones por fuente.             Operativo / técnico
  Documentos/firma          Documentos generados, pendientes de firma, formalizados, rechazados y tiempos de formalización.   Operativo
  Concertación              Convenios, vigencia, participantes, obligaciones, avances y evidencias.                           Ejecutivo
  COA / interoperabilidad   Cruces y consistencia entre información SAAEL y COA, cuando la integración sea autorizada.        Analítico

## 22.3 Capacidades BI recomendadas

  Capacidad                      Qué permite                                                                                            Aplicación
  ------------------------------ ------------------------------------------------------------------------------------------------------ -------------------------
  Dashboards ejecutivos          KPIs, tendencias, semáforos, mapas, cumplimiento y excepciones.                                        Dirección / supervisión
  Dashboards operativos          Bandejas de trabajo, vencimientos, aging, colas y tareas pendientes.                                   SPA / operación
  Drill-down / drill-through     Ir de KPI → periodo → unidad → expediente → transacción, respetando permisos.                          Todos
  Filtros multidimensionales     Tiempo, trámite, materia, ubicación, auditor, instalación, estado y responsable.                       Analistas
  Análisis temporal              Tendencia, variación interanual, cohortes, estacionalidad y comparación contra meta.                   Dirección
  Análisis geográfico            Mapas de instalaciones, áreas protegidas y distribución de trámites, si la clasificación lo permite.   Especializado
  Alertas                        Notificación por umbral, vencimiento, anomalía o cambio relevante.                                     Operativo
  Autoservicio gobernado         Exploración por usuarios autorizados sobre modelos semánticos y métricas certificadas.                 Analistas
  Narrativa y lenguaje natural   Consultas y explicaciones asistidas, con control de fuentes y trazabilidad.                            Futuro / controlado
  Exportación controlada         Excel/PDF/CSV u otros formatos, aplicando clasificación y permisos.                                    Todos

## 22.4 Arquitectura de datos para BI

  Componente           Función                                                      Criterio para SAAEL
  -------------------- ------------------------------------------------------------ --------------------------------------------------------------------------------------
  OLTP transaccional   Operación diaria y consistencia de trámites                  No debe cargarse con consultas analíticas pesadas.
  CDC / extracción     Capturar cambios de datos operativos                         Definir frecuencia y estrategia sin afectar producción.
  ETL/ELT              Limpiar, transformar, historizar y enriquecer                Reglas reproducibles y auditables.
  Almacén/lakehouse    Conservar histórico y soportar múltiples cargas analíticas   Evaluar infraestructura institucional; evitar dependencia prematura de un proveedor.
  Modelo dimensional   Hechos y dimensiones para análisis                           Facilitar KPIs, tiempos y agregaciones.
  Capa semántica       Definir métricas, relaciones, jerarquías y seguridad         Fuente única de definiciones institucionales.
  BI / visualización   Dashboards, reportes, exploración y alertas                  Separar perfiles y datos según autorización.
  Catálogo/gobierno    Metadatos, linaje, propietario, clasificación y calidad      Obligatorio para información institucional.

## 22.5 Modelo de hechos analíticos propuesto

-   HECHO_TRAMITE: una fila por evento o instancia relevante del
    trámite, con fechas de recepción, prevención, subsanación,
    resolución y cierre.

```{=html}
<!-- -->
```
-   HECHO_ESTADO: historial de transiciones para medir tiempo en cada
    estado.

```{=html}
<!-- -->
```
-   HECHO_NOTIFICACION: eventos de comunicación, canal, fecha, acuse y
    resultado.

```{=html}
<!-- -->
```
-   HECHO_DOCUMENTO: generación, versión, firma, formalización, rechazo
    y descarga, sujeto a permisos.

```{=html}
<!-- -->
```
-   HECHO_AUDITORIA: auditorías, materias, hallazgos, no conformidades y
    resultados.

```{=html}
<!-- -->
```
-   HECHO_INDICADOR: valor, periodo, unidad, meta, fuente y tendencia.

```{=html}
<!-- -->
```
-   HECHO_INTEGRACION: llamada a servicio, fuente, latencia, resultado,
    error y reintento.

```{=html}
<!-- -->
```
-   HECHO_CONCERTACION: obligaciones, hitos, vigencia y avance.

```{=html}
<!-- -->
```
-   Dimensiones comunes: TIEMPO, EMPRESA, INSTALACION, AUDITOR,
    UNIDAD_ADMINISTRATIVA, TRAMITE, MATERIA, UBICACION, ESTADO, USUARIO
    y FUENTE.

## 22.6 Calidad y gobierno del dato

-   Definir propietario funcional (data owner) y custodio técnico para
    cada dominio de información.

```{=html}
<!-- -->
```
-   Establecer reglas de calidad: unicidad, integridad referencial,
    vigencia, completitud, consistencia y valores permitidos.

```{=html}
<!-- -->
```
-   Conservar linaje: fuente → transformación → métrica → visualización.

```{=html}
<!-- -->
```
-   Certificar indicadores institucionales antes de publicarlos como KPI
    oficiales.

```{=html}
<!-- -->
```
-   Aplicar seguridad a nivel de fila/columna o equivalente cuando un
    usuario no deba ver todos los expedientes.

```{=html}
<!-- -->
```
-   Registrar exportaciones y accesos sensibles para auditoría.

```{=html}
<!-- -->
```
-   Separar información de prueba de información real y evitar que datos
    confidenciales aparezcan accidentalmente en ambientes no
    productivos.


# 23. Opciones de herramientas BI y criterios de selección

La herramienta BI debe seleccionarse después de definir arquitectura de
datos, seguridad, licenciamiento, infraestructura, usuarios y
capacidades de autoservicio. No se recomienda seleccionar primero la
herramienta y después adaptar el modelo de datos.

  Opción                        Fortalezas relevantes                                                                                                                         Encaje potencial                                                       Consideraciones
  ----------------------------- --------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------------------------------------------- --------------------------------------------------------------------------------------------
  Microsoft Power BI / Fabric   Integración estrecha con ecosistema Microsoft, modelos semánticos, Direct Lake, visualización y gobierno integrado en el ecosistema Fabric.   Alta si PROFEPA prioriza ecosistema Microsoft y gobierno integrado.    Licenciamiento, dependencia de ecosistema y diseño de arquitectura Fabric deben evaluarse.
  Tableau                       Visualización y exploración avanzada; capa semántica/mediciones y capacidades analíticas asistidas.                                           Alta si se prioriza visualización y exploración sofisticada.           Costo y arquitectura de plataforma deben evaluarse.
  Qlik                          Motor asociativo, exploración, dashboards y analítica; opciones cloud y arquitectura basada en servicios.                                     Alta para exploración transversal y escenarios de múltiples fuentes.   Gobierno, licencias y capacidades disponibles deben validarse.
  Looker                        Capa semántica gobernada con LookML, fuerte enfoque en métricas y reutilización.                                                              Alta si se prioriza semántica central y ecosistema Google Cloud.       Requiere evaluar encaje con infraestructura institucional.
  Apache Superset               Open source, SQL, dashboards y exploración sobre bases SQL existentes.                                                                        Interesante para estrategia open source / self-hosted.                 Mayor responsabilidad institucional en operación, gobierno y soporte.
  Metabase                      Open source y comercial; autoservicio, dashboards, consultas, alertas y seguridad por filas/columnas.                                         Interesante para rapidez y autoservicio controlado.                    Evaluar profundidad analítica y gobierno frente a necesidades institucionales complejas.

## 23.1 Matriz de criterios para una evaluación formal

  Criterio                         Qué evaluar                                                             Peso sugerido
  -------------------------------- ----------------------------------------------------------------------- ---------------
  Seguridad                        SSO, RBAC, RLS/CLS, cifrado, auditoría, exportaciones, segregación.     20%
  Gobierno de datos                Catálogo, linaje, métricas certificadas, control de modelos.            15%
  Integración                      BD, APIs, archivos, servicios, lakehouse/warehouse, fuentes externas.   15%
  Desempeño                        Volumen, concurrencia, caché, consultas directas, refrescos.            10%
  Autoservicio                     Exploración, filtros, drill-down, SQL, modelos reutilizables.           10%
  Visualización                    Dashboards ejecutivos, geoespacial, accesibilidad, narrativa.           10%
  Costo total                      Licencias, infraestructura, operación, soporte y capacitación.          10%
  Interoperabilidad/portabilidad   APIs, estándares, exportación y riesgo de lock-in.                      5%
  Operación                        Monitoreo, respaldo, alta disponibilidad, administración.               5%

Contexto tecnológico consultado: NIST describe Zero Trust como
protección centrada en recursos, usuarios y activos; Microsoft documenta
arquitecturas de lakehouse/OneLake y modelos semánticos de Power BI;
Tableau destaca una capa semántica gobernada; Qlik documenta su
plataforma analítica; Google Cloud documenta LookML como lenguaje de
modelado semántico; Apache Superset y Metabase ofrecen alternativas open
source/self-hosted. Estas referencias sirven para comparar patrones y
capacidades, no constituyen una recomendación contractual.


# 24. Arquitectura de información y BI propuesta para SAAEL

La siguiente separación debe considerarse como arquitectura conceptual
para el análisis técnico posterior:

  Zona              Contenido                                                                                  Acceso                     Objetivo
  ----------------- ------------------------------------------------------------------------------------------ -------------------------- -----------------------------------------
  Operacional       Datos de trámites, expedientes, usuarios, empresas, instalaciones, documentos y estados.   Aplicación transaccional   Consistencia y operación.
  Integración       Mensajes, peticiones/respuestas, colas, reintentos y resultados de servicios.              Servicios de integración   Interoperabilidad observable.
  Histórica         Snapshots/cambios y hechos de negocio.                                                     ETL/ELT                    Análisis temporal y auditoría.
  Semántica         KPI, dimensiones, jerarquías y reglas de cálculo certificadas.                             BI/analistas autorizados   Una sola definición de los indicadores.
  Presentación BI   Dashboards, reportes, alertas y autoservicio.                                              Usuarios autorizados       Decisión y seguimiento.
  Gobierno          Catálogo, linaje, clasificación, calidad y políticas.                                      Gobierno/seguridad         Confianza y cumplimiento.

## 24.1 Principio de no interferencia

El sistema transaccional debe priorizar integridad y tiempo de respuesta
de los procesos regulatorios. Las cargas analíticas, consultas masivas,
agregaciones históricas y exploraciones ad hoc deben ejecutarse
preferentemente en la plataforma analítica. Cuando se requiera
información casi en tiempo real, debe diseñarse explícitamente la
estrategia de replicación/streaming y sus límites.

## 24.2 Indicadores institucionales iniciales

  Indicador           Ejemplos                                                                                       Frecuencia
  ------------------- ---------------------------------------------------------------------------------------------- -----------------------------------
  Volumen             Trámites recibidos, atendidos, concluidos, pendientes y por estado.                            Frecuencia mensual/semanal/diaria
  Oportunidad         Tiempo promedio/mediana de ciclo, tiempo por estado y % dentro de plazo.                       Diaria/mensual
  Calidad             Prevenciones por trámite, reincidencias, datos incompletos y errores de integración.           Mensual
  Carga               Expedientes por responsable/unidad y antigüedad.                                               Diaria
  Auditoría           Auditorías realizadas, hallazgos, no conformidades y cierre de acciones.                       Mensual
  RDA                 Solicitudes, renovaciones, indicadores, cumplimiento anual y casos que pierden elegibilidad.   Mensual
  Interoperabilidad   Éxito/falla, latencia y volumen por fuente.                                                    Diaria
  Formalización       Documentos generados, firmados, pendientes y tiempos de firma.                                 Diaria
  Concertación        Convenios vigentes, vencimientos, obligaciones y avance.                                       Mensual
