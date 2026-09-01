# Plataforma Integral de PROFEPA 1.0

Repositorio documental y técnico para el análisis, diseño, arquitectura, datos,
integraciones, BI, seguridad, pruebas y operación de la **Plataforma Integral de PROFEPA 1.0**.

## Estado

**Baseline inicial:** 1.0  
**Estado:** En construcción / análisis de requerimientos  
**Fecha:** 2026-09-01

## Navegación

| Área | Contenido |
|---|---|
| [Gobierno](docs/00-gobierno/) | Alcance, responsables, decisiones y control |
| [Requerimientos](docs/01-requerimientos/) | FR, NFR, reglas, casos de uso y trazabilidad |
| [Procesos](docs/02-procesos/) | AS-IS, TO-BE, BPMN y procedimientos |
| [Arquitectura](docs/03-arquitectura/) | Aplicaciones, datos, integración y seguridad |
| [Datos](docs/04-datos/) | Modelo, diccionario, calidad y analítica |
| [Integraciones](docs/05-integraciones/) | EMA, CONANP, SEMARNAT, CFE y otras |
| [BI y Analítica](docs/06-bi-analitica/) | Indicadores, modelos y dashboards |
| [Seguridad](docs/07-seguridad/) | NFR, auditoría, trazabilidad y confidencialidad |
| [Pruebas](docs/08-pruebas/) | Estrategia, casos y resultados |
| [Operación](docs/09-operacion/) | Instalación, respaldo, monitoreo y continuidad |
| [Referencias](docs/10-referencias/) | Normatividad, benchmarking y tecnología |
| [Diagramas](diagrams/) | Arquitectura, BPMN, datos, integraciones y BI |
| [Plantillas](templates/) | Formatos para nuevos artefactos |

## Principio de trazabilidad

Cada elemento deberá identificarse y relacionarse mediante un identificador único:

`Proceso → Requerimiento → Regla → Datos → Integración → Arquitectura → KPI → Prueba → Aceptación`

## Documentación migrada

El análisis existente fue migrado a Markdown y también se conserva en Word:

- `docs/01-requerimientos/analisis-completo.md`
- `anexos/word/PIP_1.0_Analisis_de_Requerimientos_y_Procesos.docx`
- `anexos/presentaciones/PIP_1.0_Presentacion_Arquitectura_y_BI.pptx`

## Regla documental

Markdown = versión técnica navegable y versionable.  
Word/PDF = versión institucional.  
Archivos fuente de diagramas = versión editable.  
Git = historial y trazabilidad de cambios.

## Seguridad

No subir secretos, contraseñas, llaves privadas, tokens, certificados, bases de
datos productivas ni expedientes reales o información reservada sin autorización.
