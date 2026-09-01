# 21. Tendencias de arquitectura de sistemas aplicables a SAAEL

La siguiente sección incorpora contexto tecnológico externo al material
de las minutas. Se utiliza como criterio de diseño, no como requisito
obligatorio. La arquitectura definitiva debe ajustarse a
infraestructura, políticas de seguridad, contratación, operación y
capacidades de PROFEPA.

## 21.1 Tendencias relevantes

  Tendencia                    Aplicación a SAAEL                                                                                                                              Relevancia
  ---------------------------- ----------------------------------------------------------------------------------------------------------------------------------------------- -------------------------
  Arquitectura modular         Separar dominios/capacidades con contratos claros, evitando un monolito rígido y también evitando microservicios excesivos sin justificación.   Muy aplicable
  API-first                    Diseñar APIs versionadas como mecanismo de interoperabilidad con EMA, CONANP, SEMARNAT/COA, CFE y futuras fuentes.                              Muy aplicable
  Event-driven                 Usar eventos de negocio para notificaciones, vencimientos, auditoría, tareas y procesos asíncronos, cuando el caso lo justifique.               Aplicable
  Microservicios selectivos    Aislar capacidades con ciclos de vida o escalamiento distintos, especialmente integraciones y procesamiento especializado.                      Aplicable, no dogmático
  Contenedores / DevSecOps     Empaquetado reproducible, automatización de pruebas, análisis de seguridad y despliegues controlados.                                           Aplicable
  Zero Trust                   Autenticación/autorización centradas en identidad, mínimo privilegio y protección de recursos, no sólo del perímetro de red.                    Muy aplicable
  Observabilidad               Métricas, logs, trazas distribuidas y monitoreo de integraciones para detectar fallas y reconstruir transacciones.                              Muy aplicable
  Data platform / Lakehouse    Separar el almacenamiento/transformación analítica de la base transaccional y habilitar histórico, BI y analítica avanzada.                     Muy aplicable
  Capa semántica               Definir métricas institucionales, dimensiones, relaciones y reglas de cálculo en un modelo gobernado para evitar cifras contradictorias.        Muy aplicable
  Analítica aumentada por IA   Exploración en lenguaje natural, detección de anomalías y explicación de tendencias, siempre con controles, trazabilidad y datos gobernados.    Futuro controlado

## 21.2 Recomendación arquitectónica: modularidad antes que microservicios

Para SAAEL se recomienda evitar dos extremos: (a) un monolito funcional
donde cada cambio afecte a toda la aplicación, y (b) una fragmentación
prematura en decenas de microservicios. El punto de partida recomendado
es una arquitectura modular, API-first, con servicios independientes
sólo donde exista una razón verificable: interoperabilidad,
procesamiento asíncrono, documentos/firma, notificaciones, analítica o
necesidades diferenciadas de escalamiento.

  Criterio rector La arquitectura debe derivarse de dominios y procesos de negocio; la tecnología de moda no debe convertirse en un requisito por sí misma.
  -----------------------------------------------------------------------------------------------------------------------------------------------------------

## 21.3 Arquitectura objetivo conceptual

  Capa                      Componentes propuestos                                                                 Propósito
  ------------------------- -------------------------------------------------------------------------------------- -----------------------------------------------------------
  Experiencia               Portal Empresa/Auditor; Portal interno PROFEPA; supervisión; administración            Experiencias diferenciadas por actor sin duplicar reglas.
  API / Seguridad           API Gateway; identidad; autorización; rate limiting; auditoría técnica                 Punto controlado de acceso e interoperabilidad.
  Proceso y negocio         Gestión de trámites; expediente; reglas; plazos; tareas; concertación; auditoría/RDA   Orquestar procesos y reglas de negocio.
  Servicios transversales   Documentos; firma; notificaciones; búsqueda; catálogo; archivos                        Capacidades reutilizables.
  Integración               EMA; CONANP; CONABIO; CONAGUA; SEMARNAT/COA; SEPOMEX; CFE y futuras fuentes            Interoperabilidad desacoplada y observable.
  Datos transaccionales     BD relacional; almacenamiento documental; bitácora; metadatos                          Fuente operacional y evidencia.
  Datos analíticos          ETL/ELT; almacenamiento histórico; modelo dimensional/semántico; BI                    Explotación sin cargar el núcleo transaccional.
  Observabilidad            Logs, métricas, trazas, alertas, monitoreo de integraciones                            Operación y diagnóstico.

## 21.4 Seguridad arquitectónica

-   Aplicar mínimo privilegio y separación de funciones; no confiar
    implícitamente en que una red interna es segura.

```{=html}
<!-- -->
```
-   Separar autenticación, autorización y políticas de acceso a
    recursos.

```{=html}
<!-- -->
```
-   Implementar control por rol/permiso y, cuando proceda, por unidad
    administrativa, materia, territorio y expediente.

```{=html}
<!-- -->
```
-   Aplicar cifrado en tránsito y reposo; gestionar secretos fuera del
    código.

```{=html}
<!-- -->
```
-   Registrar accesos y operaciones críticas, incluyendo consultas a
    fuentes externas y exportaciones de BI.

```{=html}
<!-- -->
```
-   Aplicar controles específicos para documentos confidenciales y para
    información que pueda ser publicada o expuesta en tableros.

```{=html}
<!-- -->
```
-   Realizar pruebas de seguridad sobre APIs, carga documental, firma,
    búsqueda, exportación y filtros de BI.

NIST SP 800-207 plantea Zero Trust como un modelo que elimina la
confianza implícita basada sólo en la ubicación de red y centra el
control en usuarios, activos y recursos. Para SAAEL, esto respalda una
arquitectura de autorización por identidad, recurso y contexto,
particularmente relevante para expedientes y BI.


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


# 25. Plan de trabajo actualizado para la siguiente fase

  Fase     Frente                        Actividades                                                                                                                                                Salida
  -------- ----------------------------- ---------------------------------------------------------------------------------------------------------------------------------------------------------- ------------------------------------------
  Fase 0   Inventario y alcance          Procesos/trámites; funcionalidades vigentes/obsoletas; actividades fuera del sistema; actores; catálogo SCIAN/CMAP; DGOAPA; MULTIREGION; nuevos módulos.   Línea base de alcance aprobada.
  Fase 1   AS-IS / TO-BE                 3--5 procesos prioritarios con responsables, entradas, salidas, reglas, excepciones y tiempos.                                                             Procesos validados.
  Fase 2   Modelo funcional y de datos   Casos de uso, requisitos, reglas, expediente, folios, documentos, firmas, catálogos y modelo conceptual.                                                   Especificación funcional.
  Fase 3   Arquitectura                  API, seguridad, integración, modularidad, observabilidad, documentos, datos analíticos y BI.                                                               Arquitectura conceptual y de referencia.
  Fase 4   Interoperabilidad             EMA, CONANP, COA/SEMARNAT, CONABIO, CONAGUA, SEPOMEX, CFE y otras fuentes autorizadas.                                                                     Matriz de integraciones y contratos.
  Fase 5   BI                            Modelo de hechos/dimensiones, KPIs, capa semántica, dashboards por rol y gobierno del dato.                                                                Prototipo BI y catálogo de indicadores.
  Fase 6   MVP                           Construcción incremental por capacidades, pruebas funcionales, seguridad, rendimiento y aceptación.                                                        MVP verificable.

## 25.1 Decisiones que deben obtenerse de la SPA/PROFEPA

1.  Catálogo de procesos/trámites que sí formarán parte de la primera
    versión.

```{=html}
<!-- -->
```
1.  Confirmación de funcionalidades actuales que se eliminan, se
    conservan o se rediseñan.

```{=html}
<!-- -->
```
1.  Definición del tratamiento de MULTIREGION y de las actividades
    realizadas fuera del sistema.

```{=html}
<!-- -->
```
1.  Definición de clasificación de información y reglas de
    publicación/consulta.

```{=html}
<!-- -->
```
1.  Alcance jurídico y técnico de firma electrónica avanzada/FIEL.

```{=html}
<!-- -->
```
1.  Alcance del módulo de concertación y del vínculo con otros procesos.

```{=html}
<!-- -->
```
1.  Definición de indicadores institucionales y responsables de su
    certificación.

```{=html}
<!-- -->
```
1.  Decisión de arquitectura de despliegue: infraestructura
    institucional, nube, híbrida o combinación autorizada.

```{=html}
<!-- -->
```
1.  Decisión de estrategia BI y criterios de selección de herramienta.

```{=html}
<!-- -->
```
1.  Política de migración/convivencia con SAAEL 2.0 y conservación de
    expedientes históricos.
