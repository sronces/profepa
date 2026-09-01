# 1. Resumen ejecutivo

Actualización de seguimiento: esta versión incorpora los acuerdos y
observaciones de las Minutas No. 02 y No. 03 (archivos
Minuta_SAAEL_25082027_2_Vfinal.pdf y Minuta_SAAEL_01092027_3.pdf). Se
amplía el alcance con catálogos SCIAN/CMAP, generación y firma
electrónica de documentos, módulo de concertación, interoperabilidad con
la COA de SEMARNAT, estrategia de explotación de información/Business
Intelligence (BI), revisión de funcionalidades vigentes y obsoletas,
actividades externas al sistema, trazabilidad de folios y reglas sobre
información pública/confidencial. Los puntos que la minuta presenta como
posibilidades o acuerdos de revisión se mantienen como candidatos
sujetos a validación técnica, jurídica y funcional.

El conjunto documental analizado muestra una necesidad de evolución de
SAAEL hacia una plataforma centrada en procesos, expediente electrónico,
automatización, interoperabilidad y trazabilidad. La minuta de trabajo
plantea explícitamente iniciar el levantamiento AS-IS/TO-BE, identificar
actores, entradas, salidas, actividades, interacciones, reglas,
excepciones, cuellos de botella y requerimientos; asimismo, solicita
simplificación, eliminación de actividades sin valor, automatización,
integraciones, validaciones, precarga, notificaciones, seguimiento,
reportes y alineación normativa.

Los documentos normativos agregan una segunda dimensión crítica: SAAEL
no debe modelarse sólo como un formulario digital. Debe soportar
expedientes y ciclos de vida regulatorios, con evidencia documental,
indicadores, dictámenes, plazos, prevenciones, resoluciones, auditorías,
renovación por RDA y controles de cumplimiento.

-   La prioridad arquitectónica debe ser el modelo de proceso y de
    datos; las pantallas deben derivarse de ellos.

```{=html}
<!-- -->
```
-   La unidad funcional no debe ser únicamente el trámite: debe existir
    relación entre Empresa, Instalación, Certificado, Auditor,
    Solicitud, Expediente, Evidencia, Indicador, Materia, Dictamen y
    Resolución.

```{=html}
<!-- -->
```
-   La interoperabilidad debe diseñarse como capacidad transversal, no
    como desarrollos aislados por trámite.

```{=html}
<!-- -->
```
-   La trazabilidad debe ser un requisito estructural: quién, qué,
    cuándo, sobre qué objeto, con qué resultado y con qué evidencia.

```{=html}
<!-- -->
```
-   Los requisitos normativos deben convertirse en reglas
    parametrizables cuando sea posible, evitando codificar plazos,
    catálogos o condiciones de negocio directamente en la interfaz.

Conclusión del análisis: se recomienda abordar Plataforma Integral de
PROFEPA 1.0 como una plataforma de gestión de procesos regulatorios
ambientales, con expediente electrónico y motor de reglas, en lugar de
una simple actualización de SAAEL 2.0.


# 2. Fuentes analizadas y metodología

  Fuente                                   Uso en el análisis                               Aspectos relevantes
  ---------------------------------------- ------------------------------------------------ ------------------------------------------------------------------------------------------------------------------------------------
  Minuta_SAAEL_18082026_1.pdf              Necesidad institucional / visión AS-IS y TO-BE   Actores, entradas/salidas, automatización, integraciones, trazabilidad, roles, auditoría, reportes, requerimientos no funcionales.
  Inscripción al SAAEL 2.0 11042025.docx   Referencia de funcionalidad existente            Perfiles, captura, documentos, ubicación geográfica, auditor seleccionado, notificaciones, reglas de operación.
  NMX-AA-163-SCFI-2012.pdf                 Base normativa RDA                               Requisitos del RDA, indicadores, evidencias, sistema de gestión ambiental, renovación y actualizaciones anuales.
  RLGEEPAMAAA_311014.pdf                   Base regulatoria del ciclo de certificación      Solicitud, revisión, prevención, auditoría, plan de acción, renovación, RDA, verificaciones, plazos y obligaciones.
  NMX-AA-162-SCFI-2012.pdf                 Base de auditoría y evidencia                    Materias, evidencias, bitácoras, dictámenes, no conformidades, conservación documental y datos de instalaciones.

## 2.1 Método aplicado

1.  Separación entre necesidad de negocio, proceso, regla de negocio y
    requisito tecnológico.

```{=html}
<!-- -->
```
1.  Identificación de actores y objetos de información recurrentes.

```{=html}
<!-- -->
```
1.  Reconstrucción del AS-IS a partir de la minuta y de la funcionalidad
    de inscripción de SAAEL 2.0.

```{=html}
<!-- -->
```
1.  Diseño conceptual del TO-BE orientado a automatización y control.

```{=html}
<!-- -->
```
1.  Derivación de requisitos funcionales y no funcionales.

```{=html}
<!-- -->
```
1.  Identificación de integraciones externas y validaciones automáticas.

```{=html}
<!-- -->
```
1.  Identificación de puntos que requieren validación funcional antes de
    desarrollo.

  Lectura de la minuta: La minuta proporcionada se visualiza en 9 páginas y contiene, entre otros, el acuerdo de iniciar formalmente el análisis y levantamiento de requerimientos, así como el listado de AS-IS, TO-BE, requerimientos funcionales/no funcionales, integraciones, seguridad, auditoría, reportes y roles. Las páginas 5 a 9 son especialmente relevantes para esta evaluación.
  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------


# 6. Requerimientos funcionales principales

La siguiente matriz constituye una primera línea base para el
levantamiento. Los requisitos FR-xx son derivados de la documentación y
deben ser validados en sesiones funcionales. La numeración está diseñada
para facilitar posteriormente la trazabilidad requisito → proceso → caso
de uso → prueba.

  ID       Funcionalidad                            Descripción                                                                                                                       Prioridad
  -------- ---------------------------------------- --------------------------------------------------------------------------------------------------------------------------------- ------------
  FR-001   Administración de usuarios y perfiles    Alta, consulta, modificación, bloqueo y recuperación de acceso para Empresa, Auditor, personal PROFEPA y administradores.         Alta
  FR-002   Roles y permisos                         Definir permisos por rol, función, trámite, expediente y acción; soportar consulta de solo lectura para supervisión/auditoría.    Alta
  FR-003   Registro de Empresa e Instalación        Mantener datos generales, domicilio, actividad, instalación y relaciones con certificados/trámites.                               Alta
  FR-004   Registro de Auditor Ambiental            Mantener acreditación, aprobación, vigencia, coordinadores, especialistas y materias.                                             Alta
  FR-005   Gestión de inscripción                   Digitalizar el flujo de inscripción existente, incluyendo persona física/moral, documentos, selección de auditor y acuse.         Alta
  FR-006   Gestión de solicitudes                   Crear, editar, validar, enviar, prevenir, subsanar, rechazar, autorizar y cerrar solicitudes.                                     Alta
  FR-007   Gestión de expediente electrónico        Integrar datos, documentos, evidencias, actuaciones, comunicaciones, resoluciones y versiones.                                    Alta
  FR-008   Carga y validación documental            Permitir carga, clasificación, metadatos, vigencia, legibilidad, versión, firma y asociación a requisito.                         Alta
  FR-009   Catálogos y parámetros                   Administrar catálogos CMAP/SCIAN, materias, tipos de trámite, tipos de evidencia, estados, plazos y otros parámetros.             Alta
  FR-010   Validaciones automáticas                 Ejecutar reglas de obligatoriedad, consistencia, vigencia, duplicidad y relaciones entre datos.                                   Alta
  FR-011   Precarga de información                  Prellenar datos desde fuentes autorizadas, evitando recaptura.                                                                    Alta
  FR-012   Validación geográfica                    Capturar coordenadas/poligonal y validar ubicación respecto de fuentes geográficas institucionales cuando exista servicio.        Alta
  FR-013   Integración con fuentes externas         Consultar y registrar resultado de servicios de EMA, CONANP, CONABIO, CONAGUA, SEMARNAT, SEPOMEX y otros autorizados.             Alta
  FR-014   Gestión de auditoría/diagnóstico         Registrar planeación, participantes, materias, evidencias, hallazgos, conformidades, no conformidades y dictámenes.               Alta
  FR-015   Gestión de Plan de Acción                Registrar medidas preventivas/correctivas, responsables, fechas, prioridades, avances, evidencias y verificaciones.               Alta
  FR-016   Gestión RDA                              Capturar diagnóstico básico, generalidades, situación de instalación, sistema de gestión, indicadores y anexos.                   Alta
  FR-017   Indicadores ambientales                  Registrar indicadores específicos y particulares, periodicidad, valores, unidades, metas, tendencias y comparativos.              Alta
  FR-018   Renovación por RDA                       Validar condiciones de elegibilidad, presentar RDA, revisar, prevenir, subsanar y resolver.                                       Alta
  FR-019   Seguimiento de plazos                    Calcular y controlar vencimientos, fechas límite, días hábiles y eventos que cambian el calendario.                               Alta
  FR-020   Notificaciones                           Enviar correos y alertas por eventos: recepción, prevención, cambio de estado, vencimiento, resolución y selección de auditor.    Alta
  FR-021   Buzón / mensajería                       Centralizar comunicaciones y alertas del trámite, con historial consultable.                                                      Media-Alta
  FR-022   Bitácora de operación                    Registrar acciones de usuarios y del sistema, incluyendo fecha, hora, usuario, objeto, evento y resultado.                        Alta
  FR-023   Auditoría de expediente                  Permitir consulta histórica de versiones y acciones, con usuarios de solo lectura.                                                Alta
  FR-024   Reportes e indicadores institucionales   Generar reportes operativos, ejecutivos y regulatorios a partir de datos estructurados.                                           Alta
  FR-025   Tableros de seguimiento                  Mostrar cargas de trabajo, trámites por estado, vencimientos, indicadores y excepciones.                                          Media-Alta
  FR-026   Firma / validación de documentos         Gestionar documentos firmados y su relación con actuaciones, resoluciones o dictámenes.                                           Alta
  FR-027   Búsqueda transversal                     Buscar por empresa, instalación, certificado, trámite, auditor, materia, indicador, documento y estado.                           Alta
  FR-028   Gestión de excepciones                   Registrar excepciones, justificaciones, autorizaciones y efectos sobre el flujo.                                                  Alta
  FR-029   Administración de reglas                 Permitir parametrizar reglas que no requieran cambio estructural de software.                                                     Alta
  FR-030   Archivo y conservación                   Controlar conservación documental, versiones y disponibilidad de evidencias según política institucional y normativa aplicable.   Alta


# 7. Requerimientos funcionales específicos para RDA y desempeño ambiental

Figura 4. Flujo conceptual de renovación mediante RDA.

La NMX-AA-163-SCFI-2012 establece que el RDA integra diagnóstico básico,
generalidades de la empresa, situación de la instalación certificada,
sistema de gestión ambiental, indicadores y anexo
fotográfico/documental. También requiere evidencia actualizada y
contempla actualización anual de indicadores. El Reglamento establece
que la vía RDA aplica cuando la empresa alcanzó el máximo nivel de
desempeño y fija condiciones adicionales para conservar esa vía.

  ID       Área                        Requerimiento
  -------- --------------------------- ---------------------------------------------------------------------------------------------------------------------------------------
  RDA-01   Elegibilidad                Validar que la empresa tenga certificado vigente y máximo nivel de desempeño correspondiente.
  RDA-02   Histórico                   Gestionar histórico continuo de indicadores y periodo requerido.
  RDA-03   Manifestaciones             Registrar las manifestaciones normativas requeridas y sus evidencias.
  RDA-04   Sistema ambiental           Registrar evidencia del funcionamiento del sistema de gestión/administración ambiental.
  RDA-05   Indicadores específicos     Gestionar consumo de agua, descargas, energía, combustibles y residuos por unidad de producción, con justificación cuando no aplique.
  RDA-06   Indicadores particulares    Gestionar indicadores propios de la empresa, sus características, valores y tendencia.
  RDA-07   Comparativos                Generar tabla y gráfica por indicador para determinar mantenimiento o mejora.
  RDA-08   Evidencias                  Asociar fotografías y documentos de respaldo a secciones, requisitos e indicadores.
  RDA-09   Revisión                    Permitir prevención, subsanación y resolución con control de plazos.
  RDA-10   Seguimiento anual           Generar tareas/eventos para actualización anual durante la vigencia del certificado.
  RDA-11   Control de vía RDA          Registrar las condiciones que podrían hacer perder el derecho a la siguiente renovación por RDA.
  RDA-12   Historial de renovaciones   Controlar el número de renovaciones consecutivas por RDA y disparar la necesidad de diagnóstico cuando corresponda.

  Base normativa: La NMX-AA-163 indica, entre otros elementos, seis componentes del RDA y exige indicadores específicos y particulares, conclusiones de comportamiento y evidencia documental/fotográfica. La norma también señala la actualización anual de indicadores durante la vigencia.
  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------


# 8. Reglas de negocio principales

  ID       Regla                  Descripción
  -------- ---------------------- -------------------------------------------------------------------------------------------------------------------------------------------
  RN-001   No avanzar             No permitir avance cuando falten datos o documentos obligatorios.
  RN-002   Perfil                 El perfil del usuario determina el flujo y los datos requeridos.
  RN-003   Auditor aprobado       La selección/participación de un Auditor debe validar su acreditación/aprobación y vigencia.
  RN-004   Vigencia certificado   Las operaciones de renovación deben considerar la fecha de vencimiento y los plazos aplicables.
  RN-005   Prevención             Una prevención debe generar estado, fecha de notificación, plazo, respuesta y resolución.
  RN-006   Días hábiles           Los plazos regulatorios deben calcularse con calendario configurable y excepciones institucionales.
  RN-007   RDA elegible           La vía RDA requiere máximo nivel de desempeño y demás condiciones normativas.
  RN-008   Indicadores anuales    Durante la vigencia de un certificado por RDA debe controlarse la entrega anual de indicadores.
  RN-009   Pérdida de vía RDA     Incumplimientos o medidas de urgente aplicación pueden cambiar la vía de renovación y generar necesidad de diagnóstico.
  RN-010   No conformidad         Una no conformidad debe quedar asociada a materia, requisito/parámetro, evidencia y, en su caso, acción.
  RN-011   Plan de Acción         Cada acción debe tener responsable, plazo, prioridad, tipo, evidencia y estado.
  RN-012   Integración            Toda consulta externa debe guardar fuente, fecha/hora, resultado y, cuando aplique, identificador de transacción.
  RN-013   Documento              Los documentos deben conservar metadatos, versión y relación con el requisito o actuación que respaldan.
  RN-014   Auditoría              Las acciones críticas deben generar eventos de bitácora no editables por usuarios operativos.
  RN-015   Solo lectura           Los usuarios de supervisión/auditoría deben poder consultar sin modificar información.
  RN-016   Excepciones            Toda excepción debe registrar causa, justificación, responsable y autorización cuando corresponda.
  RN-017   Instalación            Los datos de instalación deben ser independientes de la persona/empresa cuando el proceso lo requiera, permitiendo relaciones históricas.
  RN-018   Parametrización        Plazos, catálogos, textos de notificación y reglas cambiantes deben ser parametrizables cuando sea viable.


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


# 16. Vacíos y temas que deben resolverse antes del desarrollo

  ID     Tema                                                   Definición pendiente
  ------ ------------------------------------------------------ ------------------------------------------------------------------------------------------------------------------
  G-01   Alcance exacto de Plataforma Integral de PROFEPA 1.0   Definir catálogo completo de procesos/trámites incluidos en la primera versión.
  G-02   Normativa vigente                                      Validar la vigencia y sustitución de las normas/documentos proporcionados antes de convertirlos en reglas.
  G-03   Servicios externos                                     Confirmar APIs, responsables, autenticación, términos de uso, disponibilidad y datos entregables de cada fuente.
  G-04   Firma electrónica                                      Definir qué documentos requieren firma, qué tipo de firma y cómo se validará.
  G-05   Calendario de días hábiles                             Definir fuente oficial del calendario y manejo de días inhábiles.
  G-06   Clasificación de información                           Definir qué datos/documentos son públicos, reservados, confidenciales o de acceso restringido.
  G-07   Conservación                                           Definir política institucional de retención, transferencia, archivo y disposición documental.
  G-08   Integración con sistemas existentes                    Inventariar SAAEL 2.0 y demás sistemas para decidir migración, coexistencia o retiro.
  G-09   Firma y documentos históricos                          Definir migración y validez de documentos/firmas existentes.
  G-10   Modelo organizacional                                  Definir unidades administrativas, delegaciones, ámbitos territoriales y segregación de funciones.
  G-11   Reglas parametrizables                                 Identificar qué reglas pueden cambiar por configuración y cuáles requieren cambio de software.
  G-12   Indicadores institucionales                            Definir catálogo oficial, fórmulas, periodicidad, fuentes, metas y responsables.
  G-13   Excepciones                                            Catalogar excepciones de negocio y su tratamiento formal.
  G-14   SLA operativo                                          Definir tiempos de atención internos además de los plazos regulatorios.


# 17. Recomendaciones para iniciar formalmente el levantamiento

1.  Validar el mapa de procesos de alto nivel con la SPA y separar
    claramente procesos, subprocesos y trámites.

```{=html}
<!-- -->
```
1.  Seleccionar 3 a 5 procesos prioritarios y documentarlos en AS-IS con
    responsables reales, entradas, salidas, reglas, excepciones y
    tiempos.

```{=html}
<!-- -->
```
1.  Para cada proceso, elaborar TO-BE y decidir explícitamente qué se
    elimina, qué se simplifica, qué se automatiza y qué permanece
    manual.

```{=html}
<!-- -->
```
1.  Construir un catálogo de requisitos funcionales con criterios de
    aceptación.

```{=html}
<!-- -->
```
1.  Construir un catálogo de reglas de negocio independiente del diseño
    de pantallas.

```{=html}
<!-- -->
```
1.  Definir el modelo conceptual de datos antes de diseñar formularios.

```{=html}
<!-- -->
```
1.  Confirmar las integraciones y obtener especificaciones técnicas de
    las fuentes externas.

```{=html}
<!-- -->
```
1.  Definir el expediente electrónico y la estrategia documental.

```{=html}
<!-- -->
```
1.  Definir el modelo de seguridad, roles, segregación de funciones y
    auditoría.

```{=html}
<!-- -->
```
1.  Definir una estrategia de migración/convivencia con SAAEL 2.0.

```{=html}
<!-- -->
```
1.  Convertir los requisitos prioritarios en casos de uso, historias de
    usuario o especificaciones funcionales detalladas.

```{=html}
<!-- -->
```
1.  Preparar una matriz de trazabilidad requisito--proceso--regla--caso
    de uso--prueba.

  Criterio de cierre de análisis: El objetivo de esta etapa no debe ser producir de inmediato pantallas. La salida correcta de la etapa de análisis es una definición verificable de procesos, datos, reglas, roles, integraciones, requisitos y criterios de aceptación.
  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------


# 19. Dictamen de análisis

Con base en la documentación proporcionada, existe suficiente materia
para iniciar formalmente la etapa de análisis y levantamiento de
requerimientos de Plataforma Integral de PROFEPA 1.0. La necesidad
principal no es únicamente modernizar la interfaz de SAAEL 2.0, sino
transformar el modelo operativo hacia una plataforma que gestione
procesos regulatorios ambientales de punta a punta.

La línea base recomendada para la siguiente fase es: (1) mapa de
procesos, (2) catálogo de actores, (3) modelo de información, (4)
catálogo de reglas, (5) catálogo de requerimientos funcionales y no
funcionales, (6) matriz de integraciones, (7) modelo de expediente
electrónico, (8) seguridad y auditoría, y (9) criterios de aceptación.
Una vez aprobados estos elementos, podrá iniciarse el diseño funcional y
técnico con un riesgo considerablemente menor.

FIN DEL DOCUMENTO


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


# 27. Dictamen actualizado

Con la incorporación de las Minutas No. 02 y No. 03, el alcance de SAAEL
se perfila con mayor claridad como una plataforma de gestión de procesos
regulatorios y ambientales, con expediente electrónico,
interoperabilidad, generación/formalización documental, reglas
parametrizables y explotación analítica. Los nuevos acuerdos refuerzan
que la solución no debe limitarse a replicar SAAEL 2.0: debe identificar
qué capacidades se conservan, cuáles se eliminan y cuáles se rediseñan.

La recomendación técnica es mantener una arquitectura modular y
API-first, con servicios especializados para integración,
documentos/firma, notificaciones y analítica; utilizar una capa de datos
analíticos separada del OLTP; establecer una capa semántica gobernada
para BI; y aplicar seguridad, trazabilidad y clasificación de
información desde el diseño.

El siguiente entregable recomendado no es todavía un diseño de
pantallas. Es una especificación funcional y de arquitectura validada
que contenga: inventario de procesos, AS-IS/TO-BE, requisitos, reglas,
modelo de datos, matriz de integraciones, modelo documental, seguridad,
indicadores BI, criterios de aceptación y estrategia de
migración/convivencia.

  Criterio de cierre actualizado La etapa de análisis se considera suficientemente madura para diseño/construcción cuando cada proceso prioritario tenga trazabilidad proceso → requisito → regla → dato → integración → caso de uso → criterio de aceptación → prueba.
  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
