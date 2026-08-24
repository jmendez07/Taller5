# Canvas de Agente Especializado

Usa este canvas para diseñar un acelerador reutilizable para un equipo de datos.

## 1. Nombre del acelerador

Ejemplo: Agente de SQL para rendimiento, revisor de código analítico o generador de documentación de pipelines.

## 2. Usuario objetivo

- Rol:
- Nivel técnico:
- Momento del flujo de trabajo:
- Frecuencia de uso esperada:

## 3. Problema repetible

Describe la tarea que consume tiempo, genera retrabajo o depende de expertos.

```text
Hoy el equipo pierde tiempo en...
Esto ocurre cuando...
El impacto es...
```

## 4. Entradas requeridas

- Código, consulta o notebook:
- Contexto funcional:
- Plataforma o motor:
- Datos/tablas involucradas:
- Restricciones conocidas:

## 5. Instrucciones principales

```text
Actúa como [rol experto].
Tu objetivo es [objetivo concreto].
Usa como contexto [plataforma, estándares, convenciones].
Debes entregar [formato de salida].
No debes [límites, datos sensibles, acciones no permitidas].
Si falta información, pregunta o declara supuestos.
```

## 6. Salida esperada

- Tipo de salida:
- Formato:
- Nivel de detalle:
- Evidencia requerida:
- Validación recomendada:

## 7. Controles y límites

| Riesgo | Control | Responsable |
|---|---|---|
| Datos sensibles |  |  |
| Recomendación incorrecta |  |  |
| Uso fuera de contexto |  |  |
| Cambio productivo no validado |  |  |

## 8. Gobernabilidad del agente

| Pregunta | Respuesta del equipo |
|---|---|
| ¿Qué datos puede ver este agente? |  |
| ¿Qué acciones tiene prohibidas? |  |
| ¿Quién aprueba cambios sugeridos por el agente? |  |
| ¿Cómo se versiona y actualiza el prompt? |  |
| ¿Qué pasa si el agente se usa fuera de contexto? |  |

## 9. Observabilidad

| Señal | Cómo capturarla |
|---|---|
| Entrada del usuario | Registro en PR o comentario de commit |
| Instrucciones aplicadas | Hash del `.prompt.md` en el commit |
| Respuesta generada | Resumen en el body del PR |
| Decisión humana final | Aprobación o rechazo del PR |
| Frecuencia de uso | Conteo de invocaciones por sprint |

Señales de alerta a monitorear:
- Agente usado fuera del contexto definido.
- Respuestas aceptadas sin revisión humana.
- Prompts sin dueño ni versión activa.
- Caída sostenida en la tasa de uso.

## 10. Evaluación

| Dimensión | Pregunta clave | Método |
|---|---|---|
| Correctitud | ¿La respuesta es técnicamente correcta? | Casos de prueba con salida esperada |
| Relevancia | ¿Resuelve el problema planteado? | Revisión entre pares |
| Seguridad | ¿Respeta límites de datos y acciones? | Pruebas con entradas sensibles |
| Consistencia | ¿Produce resultados similares ante entradas similares? | Ejecución repetida |
| Utilidad | ¿Reduce tiempo o mejora calidad? | Comparación antes/después |

Ciclo de mejora:
1. Ejecutar casos de prueba periódicamente.
2. Registrar falsos positivos y negativos.
3. Ajustar instrucciones según hallazgos.
4. Versionar cambios con pull request.

## 11. Métrica de éxito

- Tiempo reducido:
- Errores evitados:
- Reutilización esperada:
- Mejora de calidad:

## 9. Demo simulada

Entrada de ejemplo:

```text
[pegar ejemplo realista]
```

Respuesta esperada:

```text
[describir o simular la salida esperada]
```

## 13. Ruta de implementación en el repositorio

Una vez validado el diseño, materializar el acelerador:

1. Crear `.github/prompts/[nombre-agente].prompt.md` con las instrucciones del paso 5.
2. Si hay reglas globales, incluirlas en `.github/copilot-instructions.md`.
3. Si el agente necesita reglas por carpeta, crear `.instructions.md` en la ubicación correcta.
4. Probar con un caso real del equipo.
5. Enviar pull request para revisión y aprobación.

Evolución progresiva:
- **v0:** prompt simple con instrucciones fijas.
- **v1:** prompt con variables `{{input}}` y contexto dinámico.
- **v2:** agente con herramientas (MCP) si la complejidad lo requiere.
- **v3:** flujo multi-agente con orquestación.

## 14. Decisión final

- [ ] Listo para piloto
- [ ] Requiere ajustes
- [ ] Requiere revisión de seguridad o gobernanza
- [ ] No viable por ahora
