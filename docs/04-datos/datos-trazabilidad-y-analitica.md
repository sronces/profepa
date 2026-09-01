# 12. Trazabilidad, auditoría y expediente electrónico

Figura 7. Modelo de trazabilidad.

La trazabilidad debe permitir reconstruir una decisión administrativa o
técnica. No basta con almacenar el estado actual; se requiere conservar
el historial de eventos y la relación entre datos, documentos y
decisiones.

-   Identificador único de expediente y de trámite.

```{=html}
<!-- -->
```
-   Historial de estados y transiciones.

```{=html}
<!-- -->
```
-   Usuario/rol que ejecutó cada acción.

```{=html}
<!-- -->
```
-   Fecha y hora institucional.

```{=html}
<!-- -->
```
-   Objeto afectado y versión anterior/nueva cuando corresponda.

```{=html}
<!-- -->
```
-   Resultado de validaciones automáticas y consultas externas.

```{=html}
<!-- -->
```
-   Documentos/evidencias relacionados.

```{=html}
<!-- -->
```
-   Notificaciones emitidas y acuses.

```{=html}
<!-- -->
```
-   Resoluciones, dictámenes y firmas.

```{=html}
<!-- -->
```
-   Registro de excepciones y autorizaciones.


# 13. Entidades de información que deben considerarse

  Entidad                          Contenido mínimo conceptual
  -------------------------------- ------------------------------------------------------------------------------------------
  Empresa                          Identidad, razón social, RFC, representación, contactos y relaciones.
  Instalación                      Ubicación, coordenadas/polígono, actividad, características y situación histórica.
  Auditor Ambiental                Unidad de verificación, aprobación, acreditación, vigencia, especialistas y materias.
  Usuario                          Identidad de acceso y relación con actor/organización.
  Rol / Permiso                    Autorizaciones para operar dentro del sistema.
  Certificado                      Tipo, nivel, vigencia, instalación, estado y renovaciones.
  Solicitud / Trámite              Tipo, modalidad, fechas, estado, responsable, plazos y resolución.
  Expediente                       Contenedor lógico de documentos, datos y actuaciones.
  Documento / Evidencia            Archivo, tipo, versión, metadatos, vigencia, firma y relación con requisito.
  Materia                          Agua, aire/ruido, suelo, residuos, energía, recursos, riesgo, gestión, emergencias, etc.
  Indicador                        Tipo, unidad, periodo, valor, meta, fuente, tendencia y evidencia.
  No Conformidad                   Materia, requisito, evidencia, severidad/prioridad, estado y acciones asociadas.
  Plan de Acción                   Acción, tipo, responsable, fechas, prioridad, avance y evidencia.
  Prevención                       Observación, fecha, plazo, respuesta, estado y resolución.
  Notificación                     Evento, destinatario, canal, fecha, contenido, acuse y estado.
  Integración / Consulta externa   Fuente, fecha, petición, respuesta, resultado y evidencia.
  Evento de auditoría              Usuario, acción, objeto, fecha/hora, IP/sistema y resultado, según política.
  Catálogo / Parámetro             Valor, vigencia, versión, fuente y responsable de administración.


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
