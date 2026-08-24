# Librería de Prompts

Esta librería sirve como punto de partida para equipos analíticos. Cada prompt debe versionarse, probarse y ajustarse con ejemplos reales del equipo.

## Implementación como archivos .prompt.md

Cada prompt de esta librería puede convertirse en un archivo `.prompt.md` dentro de `.github/prompts/` del repositorio.

Estructura del archivo:

```markdown
---
mode: agent
description: Descripción breve del prompt
---
[Contenido del prompt con variables {{input}} si aplica]
```

Ventajas:
- Se invoca directamente desde Copilot Chat.
- Se versiona con Git (historial, blame, revisión).
- Se comparte al clonar el repositorio.
- Soporta variables dinámicas.

## Plantilla de Prompt Card

```markdown
## Nombre

## Objetivo

## Cuándo usarlo

## Entrada requerida

## Prompt

## Formato de salida esperado

## Criterios de calidad

## Riesgos o límites

## Dueño / versión
```

## Prompt 1: Revisor de SQL para Rendimiento

**Objetivo:** detectar problemas de costo, filtros, uniones y columnas innecesarias.

**Cuándo usarlo:** antes de enviar una consulta SQL a revisión o integrarla en un pipeline/reporting.

**Entrada requerida:** consulta SQL, motor/plataforma, objetivo de negocio y volumen aproximado de datos.

**Prompt:**

```text
Actúa como arquitecto de datos senior.
Revisa la siguiente consulta SQL para identificar problemas de rendimiento, mantenibilidad y calidad de datos.
No inventes tablas, columnas, índices ni particiones. Si falta contexto, indícalo como supuesto o pregunta.
Entrega una tabla con: hallazgo, severidad, evidencia, recomendación y validación requerida.

Consulta:
[pegar consulta]

Contexto:
[plataforma, volumen, objetivo, restricciones]
```

**Formato de salida esperado:** tabla de hallazgos y versión sugerida de la consulta si aplica.

**Criterios de calidad:** recomendaciones verificables, sin cambios destructivos y con supuestos explícitos.

## Prompt 2: Generador de Documentación Técnica

**Objetivo:** crear documentación clara de notebooks, pipelines, funciones o consultas.

**Cuándo usarlo:** al preparar entregables, handoffs, documentación operacional o onboarding.

**Entrada requerida:** código o descripción del flujo, audiencia objetivo y nivel de detalle.

**Prompt:**

```text
Actúa como documentador técnico para equipos de datos.
Genera documentación del siguiente flujo con lenguaje claro y accionable.
Incluye: propósito, entradas, salidas, dependencias, supuestos, pasos principales, riesgos, validaciones y criterios de operación.
No inventes información no presente. Si falta contexto, crea una sección de preguntas pendientes.

Contenido a documentar:
[pegar código, notebook o descripción]
```

**Formato de salida esperado:** documentación en Markdown lista para README o wiki.

**Criterios de calidad:** explica qué hace, cómo se valida y qué riesgos deben controlarse.

## Prompt 3: Asistente de Debugging Analítico

**Objetivo:** diagnosticar errores en consultas, notebooks, pipelines o transformaciones.

**Cuándo usarlo:** cuando aparece un error técnico, inconsistencia de datos o comportamiento inesperado.

**Entrada requerida:** mensaje de error, fragmento de código, contexto de ejecución y cambio reciente.

**Prompt:**

```text
Actúa como ingeniero de datos senior ayudando a diagnosticar un problema.
Analiza el error y el código. Propón hipótesis ordenadas por probabilidad, evidencia que las respalda, pruebas rápidas para confirmarlas y una corrección mínima.
No saltes directo a una solución si falta información crítica.

Error:
[pegar error]

Código o consulta:
[pegar fragmento]

Contexto:
[ambiente, datos, cambios recientes]
```

**Formato de salida esperado:** hipótesis, prueba discriminante, corrección propuesta y riesgos.

**Criterios de calidad:** orientado a evidencia, con pasos de validación claros.
