# 9. Requerimientos no funcionales

  ID       Categoría               Requisito
  -------- ----------------------- -----------------------------------------------------------------------------------------------------------------------
  NFR-01   Seguridad               Autenticación robusta, control de sesiones, autorización por rol/permiso y protección de información sensible.
  NFR-02   Trazabilidad            Toda operación crítica debe quedar registrada con usuario, fecha/hora, objeto, acción y resultado.
  NFR-03   Disponibilidad          Definir niveles objetivo de disponibilidad, ventanas de mantenimiento y continuidad operativa.
  NFR-04   Rendimiento             Definir tiempos objetivo para consultas, captura, carga documental y operaciones integradas.
  NFR-05   Interoperabilidad       APIs/servicios documentados, versionados y con manejo estandarizado de errores.
  NFR-06   Escalabilidad           Capacidad de crecer en trámites, expedientes, documentos, indicadores y usuarios.
  NFR-07   Respaldo                Copias de seguridad, recuperación y pruebas periódicas de restauración.
  NFR-08   Recuperación            Definir RPO/RTO para componentes críticos.
  NFR-09   Protección documental   Integridad, control de versiones, hash/huella cuando proceda, acceso restringido y conservación.
  NFR-10   Accesibilidad           Interfaces accesibles y compatibles con estándares institucionales aplicables.
  NFR-11   Mantenibilidad          Arquitectura modular, parametrización y documentación técnica.
  NFR-12   Observabilidad          Monitoreo de servicios, integraciones, colas, errores y tareas programadas.
  NFR-13   Compatibilidad          Compatibilidad con infraestructura institucional y navegadores soportados.
  NFR-14   Auditoría               Capacidad de reconstruir la historia del trámite sin alterar el registro histórico.
  NFR-15   Confidencialidad        Separación de expedientes y permisos; control de documentos con información reservada/confidencial según corresponda.


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
