# 10. Integraciones e interoperabilidad

Figura 5. Arquitectura conceptual de integraciones.

La minuta plantea revisar con EMA la existencia de una plataforma para
consultar y validar acreditaciones de laboratorios y auditores; con
CONANP la validación de ubicación respecto de áreas protegidas; y
considerar otras fuentes como CONABIO, CONAGUA y SEMARNAT. También se
plantea precargar información de domicilio a partir del código postal
mediante SEPOMEX.

  ID       Fuente                 Datos                        Uso
  -------- ---------------------- ---------------------------- --------------------------------------------------------------------------------------------------------------------
  INT-01   EMA                    Auditores/laboratorios       Validar acreditación, aprobación, vigencia y condición.
  INT-02   CONANP                 Áreas naturales protegidas   Validar ubicación/polígono respecto de áreas protegidas.
  INT-03   CONABIO                Biodiversidad                Consultar información relevante para análisis/validación.
  INT-04   CONAGUA                Concesiones y pozos          Consultar concesiones, vigencias, pozos, coordenadas y volúmenes autorizados cuando aplique.
  INT-05   SEMARNAT               Padrones/autorizaciones      Consultar información ambiental institucional, residuos, autorizaciones y otros padrones aplicables.
  INT-06   SEPOMEX                Domicilios                   Precargar colonia, municipio/alcaldía y entidad a partir de código postal, sujeto a disponibilidad y autorización.
  INT-07   Catálogos CMAP/SCIAN   Clasificación de actividad   Precargar/validar giro o actividad y determinar atención institucional cuando corresponda.
  INT-08   Otros                  Fuentes futuras              Diseñar una capa reutilizable para incorporar nuevas fuentes sin rediseñar los procesos.

  Criterio de diseño: Cada integración deberá tener contrato de servicio, autenticación, límites de consumo, timeout, reintentos, manejo de indisponibilidad y bitácora. El resultado de una consulta externa debe conservarse como evidencia de la validación realizada en ese momento.
  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------


# 20. Actualización derivada de las minutas de seguimiento

Esta sección consolida los elementos nuevos o precisados en las Minutas
No. 02 y No. 03. No sustituye el levantamiento AS-IS/TO-BE; establece
una línea de trabajo para convertir los acuerdos en requisitos
verificables.

## 20.1 Acuerdos y decisiones que deben incorporarse al análisis

  ID     Tema                           Incorporación al análisis                                                                                                                                                                                                         Prioridad/estado
  ------ ------------------------------ --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ------------------------------
  M-01   Interoperabilidad con EMA      Investigar una plataforma/servicio que permita consultar y validar acreditaciones emitidas a auditores y las aprobaciones requeridas por PROFEPA, procurando que la validación pueda ejecutarse automáticamente entre sistemas.   Alta / sujeto a factibilidad
  M-02   Interoperabilidad con CONANP   Consultar/validar si un domicilio o coordenadas de instalación se encuentran dentro de un área protegida y automatizar el intercambio cuando exista servicio disponible.                                                          Alta / sujeto a factibilidad
  M-03   Catálogos SCIAN/CMAP           La nueva plataforma debe utilizar catálogos de clasificación de actividad como componente de datos y reglas, evitando catálogos embebidos en pantallas.                                                                           Alta
  M-04   Folios                         Revisar el esquema de folios para considerar prefijos, confirmación del número de trámite y atributos como tipo, año y ubicación, según definición funcional.                                                                     Alta
  M-05   Auditor ↔ empresa              Analizar una dinámica más flexible de interacción/selección entre auditor y empresa, con reglas de elegibilidad y trazabilidad.                                                                                                   Alta
  M-06   Eliminación de valor           No replicar actividades que actualmente son manuales o en papel si no agregan valor; rediseñar el proceso TO-BE antes de automatizar.                                                                                             Alta
  M-07   MULTIREGION                    La minuta señala que ya no existen solicitudes MULTIREGION; esta funcionalidad no debe trasladarse automáticamente a la nueva plataforma sin justificación de negocio.                                                            Alta / decisión de alcance
  M-08   Clasificación de información   Definir desde el diseño qué campos/documentos serán públicos, confidenciales, reservados o restringidos, incluyendo pruebas de exposición de información.                                                                         Alta
  M-09   Evaluación de auditores        Considerar un mecanismo para que empresas califiquen a auditores ambientales y definir tratamiento/publicidad de esa información.                                                                                                 Media / decisión de política
  M-10   Actor CFE                      Incorporar a la Comisión Federal de Electricidad como actor/fuente a contactar para determinar si existe información interoperable relevante.                                                                                     Media / por validar
  M-11   Módulo de concertación         Considerar un módulo específico para convenios de concertación, con expediente, participantes, documentos, estados, firmas y seguimiento.                                                                                         Media-Alta
  M-12   Documentos y FIEL              Integrar generación de documentos y, cuando jurídicamente corresponda, firma electrónica avanzada de participantes para formalización y notificación.                                                                             Alta / validación jurídica
  M-13   COA / SEMARNAT                 Evaluar integración con la Cédula de Operación Anual (COA) de SEMARNAT mediante interoperabilidad/microservicios, evitando replicación manual.                                                                                    Alta / factibilidad
  M-14   BI                             Definir estrategia de explotación, reporteo e indicadores mediante una capacidad BI separada del núcleo transaccional.                                                                                                            Alta
  M-15   Inventario funcional           Generar listado de funcionalidades actuales que ya no son útiles/no están vigentes y de nuevas funcionalidades deseadas; usarlo como control de alcance.                                                                          Alta
  M-16   Actividades externas           Identificar actividades realizadas fuera del sistema y el mecanismo de control/seguimiento de DGOAPA, para incorporarlos al modelo de proceso integral.                                                                           Alta
  M-17   Nombre de plataforma           La minuta plantea valorar un nombre distinto de Plataforma Integral de PROFEPA 1.0; debe tratarse como decisión institucional independiente del diseño técnico.                                                                   Baja / institucional

## 20.2 Implicaciones funcionales nuevas

-   El catálogo SCIAN/CMAP debe convertirse en una entidad gobernada,
    versionada y con vigencia; las selecciones de actividad deben quedar
    asociadas a la empresa/instalación y a la decisión de atención
    correspondiente.

```{=html}
<!-- -->
```
-   El folio debe ser una entidad de negocio, no sólo un número de
    pantalla: debe tener unicidad, trazabilidad, composición
    configurable y relación con expediente, trámite, ubicación y año.

```{=html}
<!-- -->
```
-   El expediente debe soportar generación de documentos a partir de
    plantillas, control de versiones, firma electrónica cuando proceda,
    evidencia de firma y estado de formalización.

```{=html}
<!-- -->
```
-   El módulo de concertación debe reutilizar expediente, documentos,
    participantes, firmas, notificaciones, calendario y auditoría,
    evitando crear una plataforma paralela.

```{=html}
<!-- -->
```
-   Las integraciones deben diseñarse como servicios reutilizables. La
    minuta de COA refuerza el principio de interoperabilidad por
    microservicios, pero la selección entre API Gateway, ESB, mensajería
    o integración directa deberá definirse en arquitectura.

```{=html}
<!-- -->
```
-   El BI no debe consultar indiscriminadamente la base transaccional en
    producción. Debe existir una capa analítica, modelos semánticos y
    controles de seguridad que permitan explotación sin comprometer el
    desempeño ni la integridad operacional.

## 20.3 Requisitos funcionales adicionales

  ID       Funcionalidad                 Descripción                                                                                                               Prioridad
  -------- ----------------------------- ------------------------------------------------------------------------------------------------------------------------- ------------
  FR-031   Gestión de folios             Generar/validar folios con reglas de unicidad, prefijo, tipo, año, ubicación y confirmación, según catálogo aprobado.     Alta
  FR-032   Catálogos SCIAN/CMAP          Administrar clasificación de actividad con vigencias, versiones, equivalencias y relación con reglas de atención.         Alta
  FR-033   Generación de documentos      Generar documentos institucionales a partir de plantillas y datos del expediente, con control de versión.                 Alta
  FR-034   Firma electrónica             Gestionar documentos que requieran firma electrónica avanzada, evidencias de firma y estado de formalización.             Alta
  FR-035   Módulo de concertación        Gestionar convenios de concertación, participantes, obligaciones, documentos, firmas, vigencia y seguimiento.             Media-Alta
  FR-036   Integración COA               Consultar/intercambiar información con COA/SEMARNAT cuando exista mecanismo autorizado y técnicamente disponible.         Alta
  FR-037   Evaluación de auditor         Registrar evaluación de servicio por parte de la empresa, con reglas de visibilidad y publicación por definir.            Media
  FR-038   Inventario de funcionalidad   Mantener catálogo de funcionalidades vigentes, candidatas a retirar y nuevas funcionalidades, como control de alcance.    Alta
  FR-039   Actividades externas          Registrar o integrar hitos que ocurren fuera de SAAEL y su evidencia/seguimiento institucional.                           Alta
  FR-040   BI y explotación              Exponer datos gobernados a una capa analítica para indicadores, tableros, análisis histórico y autoservicio controlado.   Alta

## 20.4 Reglas de negocio adicionales

  ID       Regla                          Descripción
  -------- ------------------------------ -----------------------------------------------------------------------------------------------------------------------------------------------------
  RN-019   Folio único                    No puede existir más de un folio activo con la misma clave de negocio; las correcciones deben conservar el historial.
  RN-020   SCIAN/CMAP vigente             La actividad debe validarse contra la versión de catálogo vigente y conservar la versión utilizada en la decisión.
  RN-021   Formalización                  Un documento sujeto a firma no debe considerarse formalizado hasta que se cumplan las firmas requeridas y se registre la evidencia correspondiente.
  RN-022   Clasificación de información   La clasificación de un dato/documento determina su visualización, descarga, publicación y tratamiento en BI.
  RN-023   BI no transaccional            Los procesos analíticos no deben alterar información operativa; la capa BI será de lectura y explotación.
  RN-024   Integración COA                Toda transacción con COA deberá registrar fuente, fecha/hora, identificador de operación, petición/respuesta y resultado.
  RN-025   Funcionalidad obsoleta         Una funcionalidad identificada como obsoleta no se implementará en Plataforma Integral de PROFEPA 1.0 sin una decisión explícita de alcance.
  RN-026   Actividad externa              Un hito externo relevante debe tener responsable, fecha, estado y evidencia o referencia verificable.
