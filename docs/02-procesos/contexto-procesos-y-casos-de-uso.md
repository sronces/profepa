# 3. Modelo de contexto

El sistema debe concebirse como un núcleo de gestión de trámites y
expedientes que recibe información de Empresas, Auditores y personal de
PROFEPA, y que consulta o intercambia información con fuentes externas.
La minuta identifica expresamente la necesidad de revisar con EMA,
CONANP y otras instituciones la existencia de servicios o mecanismos de
consulta/validación.

Figura 1. Contexto conceptual de Plataforma Integral de PROFEPA 1.0.

## 3.1 Actores principales

  Actor                       Responsabilidad / interacción
  --------------------------- --------------------------------------------------------------------------------------------------------------------------------------
  Empresa / Instalación       Captura solicitudes, mantiene datos, aporta evidencias, indicadores y manifestaciones; recibe notificaciones y resoluciones.
  Auditor Ambiental           Participa en auditorías/diagnósticos/verificaciones; aporta dictámenes, evidencias y resultados; requiere expediente y trazabilidad.
  Personal SPA / PROFEPA      Revisa, previene, valida, autoriza, da seguimiento, consulta expedientes y genera reportes.
  Administrador del sistema   Administra usuarios, roles, catálogos, parámetros, reglas, integraciones y configuración.
  Fuentes externas            Proveen datos para validar identidad, acreditación, ubicación, concesiones, áreas protegidas, biodiversidad, padrones y otros datos.


# 4. Análisis del proceso actual (AS-IS)

La minuta identifica un escenario donde parte relevante de las
actividades son manuales o semiautomatizadas. Entre las necesidades
señaladas se encuentran la reducción de tareas, automatización de envíos
y notificaciones, precarga de datos, consultas a fuentes externas,
generación de indicadores, seguimiento y trazabilidad.

Figura 2. Síntesis del AS-IS identificable a partir de la documentación.

## 4.1 Principales problemas / oportunidades

  ID    Situación                                                               Impacto                                                     Prioridad
  ----- ----------------------------------------------------------------------- ----------------------------------------------------------- ------------
  P01   Captura repetitiva y manual de datos                                    Errores, retrabajo y tiempos mayores                        Alta
  P02   Validaciones externas no integradas                                     Revisión manual y riesgo de información desactualizada      Alta
  P03   Dependencia de documentos PDF externos                                  Pérdida de estructura de datos y poca reutilización         Alta
  P04   Correos/oficios/notificaciones manuales                                 Riesgo de omisiones y falta de oportunidad                  Alta
  P05   Trazabilidad dispersa                                                   Dificultad para auditoría y reconstrucción del expediente   Alta
  P06   Reglas y parámetros poco visibles/parametrizables                       Dependencia de cambios de código                            Media-Alta
  P07   Reportes que dependen de consolidación manual                           Tiempo operativo y menor oportunidad de información         Alta
  P08   Procesos con participación humana en puntos que podrían automatizarse   Costo operativo sin valor agregado                          Media-Alta


# 5. Modelo TO-BE propuesto

La propuesta es evolucionar hacia un modelo de gestión basado en
expediente electrónico, procesos configurables, motor de reglas,
integraciones, gestor documental, notificaciones y auditoría. El
objetivo no es digitalizar cada paso manual existente, sino rediseñar el
proceso para eliminar pasos sin valor.

Figura 3. Proceso TO-BE conceptual.

## 5.1 Principios de diseño

-   Captura única y reutilización de información.

```{=html}
<!-- -->
```
-   Validación automática antes de permitir avanzar de etapa.

```{=html}
<!-- -->
```
-   Precarga de datos cuando exista una fuente institucional confiable.

```{=html}
<!-- -->
```
-   Separación entre datos estructurados y documentos/evidencias.

```{=html}
<!-- -->
```
-   Motor de reglas y parámetros administrables.

```{=html}
<!-- -->
```
-   Estados de trámite explícitos y controlados.

```{=html}
<!-- -->
```
-   Notificaciones generadas por eventos de negocio.

```{=html}
<!-- -->
```
-   Expediente único por asunto/trámite, con versiones y evidencias.

```{=html}
<!-- -->
```
-   Bitácora inmutable de acciones relevantes.

```{=html}
<!-- -->
```
-   Roles y permisos por función, materia, trámite y operación.

```{=html}
<!-- -->
```
-   Diseño API-first para integraciones.

```{=html}
<!-- -->
```
-   Reportes derivados de datos operativos, no de consolidaciones
    manuales.


# 11. Mapa de procesos y módulos funcionales

Figura 6. Mapa funcional propuesto.

El mapa sugiere una separación entre capacidades transversales y
procesos de negocio. Esta separación reduce duplicidad y permite que
inscripción, certificación, renovación, auditoría y RDA compartan
expediente, usuarios, documentos, reglas, notificaciones y auditoría.


# 14. Casos de uso prioritarios para la siguiente fase

  ID      Caso de uso                      Actor                Objetivo
  ------- -------------------------------- -------------------- -----------------------------------------------------------------------------------
  CU-01   Inscribir Empresa                Empresa              Capturar datos, documentos, domicilio, actividad, auditor y obtener acuse/acceso.
  CU-02   Inscribir Auditor                Auditor              Registrar datos, acreditación/aprobación, domicilio y obtener acceso.
  CU-03   Iniciar trámite                  Empresa / PROFEPA    Crear solicitud y asociar instalación/certificado.
  CU-04   Validar información              Sistema / PROFEPA    Ejecutar reglas y consultas externas.
  CU-05   Revisar expediente               Personal SPA         Consultar expediente, evidencias y resultados de validación.
  CU-06   Emitir prevención                Personal SPA         Registrar observaciones, notificar y controlar plazo.
  CU-07   Subsanar prevención              Empresa              Corregir datos/documentos y reenviar.
  CU-08   Gestionar auditoría              Auditor              Registrar actividades, materias, evidencias, hallazgos y dictamen.
  CU-09   Gestionar RDA                    Empresa              Capturar RDA, indicadores, manifestaciones y evidencias.
  CU-10   Revisar RDA                      PROFEPA              Validar contenido, evidencias, indicadores y condiciones.
  CU-11   Actualizar indicadores anuales   Empresa              Capturar y presentar indicadores dentro del periodo requerido.
  CU-12   Dar seguimiento                  PROFEPA              Controlar plazos, tareas, verificaciones y compromisos.
  CU-13   Emitir resolución/certificado    PROFEPA              Formalizar decisión y actualizar vigencia/estado.
  CU-14   Consultar trazabilidad           Supervisor/Auditor   Reconstruir historial sin modificarlo.
  CU-15   Generar reporte                  Usuario autorizado   Obtener información operativa, ejecutiva o regulatoria.


# 15. Priorización recomendada

Se recomienda una estrategia por capacidades, no por pantallas.

  Fase                        Capacidades                                                                                        Resultado esperado
  --------------------------- -------------------------------------------------------------------------------------------------- -----------------------------------------------------
  Fase 0 --- Descubrimiento   Inventario AS-IS, procesos, actores, reglas, datos, integraciones y normativa aplicable            Línea base validada y catálogo de requerimientos.
  Fase 1 --- Núcleo           Usuarios, roles, empresas, instalaciones, auditores, catálogos, expediente, documentos, bitácora   Plataforma transversal reutilizable.
  Fase 2 --- Trámites         Solicitud, validación, prevención, subsanación, resolución y notificaciones                        Digitalización integral del ciclo de trámite.
  Fase 3 --- Auditoría/RDA    Auditoría, evidencias, indicadores, RDA, renovación y seguimiento anual                            Cobertura de los procesos sustantivos prioritarios.
  Fase 4 --- Integraciones    EMA, CONANP, CONABIO, CONAGUA, SEMARNAT, SEPOMEX y otras                                           Validaciones y precarga automáticas.
  Fase 5 --- Analítica        Tableros, indicadores de gestión, explotación histórica                                            Información oportuna para supervisión y dirección.
