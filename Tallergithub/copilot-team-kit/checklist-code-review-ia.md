# Lista de Verificación de Revisión de Código Asistida por IA

Usa esta lista de verificación para convertir a GitHub Copilot en un primer filtro de calidad antes de la revisión humana.

## Prompt base

```text
Actúa como revisor técnico senior para equipos de datos.
Revisa el siguiente cambio y entrega hallazgos priorizados.
Evalúa: correctitud, rendimiento, seguridad, datos sensibles, mantenibilidad, pruebas, documentación y cumplimiento de estándares del equipo.
No apruebes automáticamente. Indica qué evidencia falta y qué debe validar una persona.

Cambio a revisar:
[pegar diff, consulta, notebook o función]

Contexto:
[objetivo, plataforma, tablas/datos involucrados, restricciones]
```

## Lista de verificación

| Dimensión | Preguntas guía | Resultado |
|---|---|---|
| Correctitud | ¿El cambio resuelve el problema? ¿Hay casos borde? |  |
| Rendimiento | ¿Hay filtros costosos, uniones riesgosas, `SELECT *` o lecturas innecesarias? |  |
| Seguridad | ¿Aparecen secretos, rutas sensibles, tokens o permisos excesivos? |  |
| Privacidad | ¿Se exponen datos personales, sensibles o regulados? |  |
| Mantenibilidad | ¿El código es legible, simple y consistente con el equipo? |  |
| Trazabilidad | ¿Quedan supuestos, entradas y salidas documentadas? |  |
| Pruebas | ¿Hay validaciones unitarias, de datos o smoke tests suficientes? |  |
| Operación | ¿Se entiende cómo monitorear, ejecutar o revertir el cambio? |  |

## Severidad sugerida

- **Alta:** puede causar pérdida de datos, exposición de información, error productivo o costo material.
- **Media:** puede generar retrabajo, degradación del rendimiento o mantenimiento complejo.
- **Baja:** mejora de estilo, claridad, documentación o consistencia.

## Antipatrones a evitar

- Aceptar el resultado de Copilot sin validar contra datos reales.
- Usar prompts vagos como "revisa esto" sin criterios específicos.
- Asumir que Copilot conoce el esquema de datos o contexto interno.
- Saltarse la revisión humana porque "la IA ya lo revisó".
- Instrucciones contradictorias entre el prompt y las Custom Instructions del repo.

## Trazabilidad para entornos regulados

| Qué registrar | Cómo |
|---|---|
| Quién usó el prompt de revisión | Comentario en PR o commit |
| Qué hallazgos generó Copilot | Resumen en el body del PR |
| Quién validó los hallazgos | Aprobador del pull request |
| Versión del prompt utilizado | Referencia al archivo .prompt.md (hash del commit) |

## Gobernabilidad, observabilidad y evaluación en revisión asistida

### Gobernabilidad

- El prompt de revisión debe tener alcance definido (qué revisa y qué no).
- No debe acceder a datos sensibles más allá del diff o consulta proporcionada.
- Los hallazgos del agente requieren aprobación humana antes del merge.
- El archivo `.prompt.md` de revisión debe tener dueño y estar versionado.

### Observabilidad

| Señal | Dónde registrarla |
|---|---|
| Prompt usado | Referencia en comentario del PR |
| Hallazgos generados | Sección del body del PR |
| Decisión humana | Aprobación/rechazo del revisor |
| Versión del prompt | Hash del commit del `.prompt.md` |

Señales de alerta:
- PRs aprobados sin evidencia de revisión humana post-Copilot.
- Hallazgos ignorados sin justificación.
- Prompt de revisión desactualizado (sin cambios en >3 meses).

### Evaluación

| Dimensión | Cómo medirla |
|---|---|
| Correctitud | ¿Los hallazgos reportados son reales? (falsos positivos) |
| Cobertura | ¿Detecta problemas que un humano también encontraría? (falsos negativos) |
| Utilidad | ¿Reduce tiempo de revisión sin perder calidad? |
| Consistencia | ¿Ante el mismo código, produce los mismos hallazgos? |

Ciclo de mejora: revisar mensualmente los falsos positivos/negativos y ajustar el prompt.

## Regla de uso

Copilot puede acelerar el hallazgo de problemas, pero la decisión final de aprobar, rechazar o escalar pertenece al revisor humano.
