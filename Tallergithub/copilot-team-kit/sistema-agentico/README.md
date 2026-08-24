# Sistema Agéntico para Equipos de Datos

Este es un sistema multi-agente construido con archivos nativos de GitHub Copilot. No requiere servidor, framework externo ni configuración adicional: funciona al clonar el repositorio y abrir VS Code con Copilot habilitado.

## Arquitectura

```
.github/
├── copilot-instructions.md              ← Reglas del sistema (aplican a todos los agentes)
└── prompts/
    ├── orchestrator.prompt.md           ← Orquestador: analiza y delega
    ├── sql-review.prompt.md             ← Agente: Revisor de SQL
    ├── code-review.prompt.md            ← Agente: Revisor de Código
    ├── doc-generator.prompt.md          ← Agente: Generador de Documentación
    ├── data-quality.prompt.md           ← Agente: Analista de Calidad de Datos
    └── debug-assistant.prompt.md        ← Agente: Asistente de Debugging
```

## Cómo funciona

| Componente | Rol | Archivo |
|---|---|---|
| **Instrucciones del sistema** | Reglas globales que todos los agentes respetan | `copilot-instructions.md` |
| **Orquestador** | Recibe la solicitud, identifica el agente correcto y delega | `orchestrator.prompt.md` |
| **Agentes especializados** | Ejecutan tareas específicas con formato y restricciones definidas | `*.prompt.md` |

## Cómo usarlo

1. Clonar o copiar esta carpeta `.github/` en la raíz de cualquier repositorio del equipo.
2. Abrir el repositorio en VS Code con GitHub Copilot habilitado.
3. En Copilot Chat, invocar un agente directamente o usar el orquestador.

### Invocación directa de un agente

Desde Copilot Chat, hacer clic en el ícono de prompt (📎) y seleccionar el archivo `.prompt.md` deseado, o escribir:

```
@workspace /sql-review [pegar consulta SQL]
```

### Usando el orquestador

```
@workspace /orchestrator Necesito revisar esta consulta SQL y luego documentar el pipeline completo.
```

El orquestador identificará que necesita dos agentes (sql-review + doc-generator) y ejecutará en secuencia.

## Gobernabilidad

- Las instrucciones del sistema en `copilot-instructions.md` limitan lo que todos los agentes pueden hacer.
- Cada agente tiene restricciones explícitas en su archivo `.prompt.md`.
- Los cambios a agentes pasan por pull request como cualquier otro código.
- Los roles de aprobación se definen en el equipo, no en la herramienta.

## Observabilidad

- Cada invocación queda registrada en el historial de Copilot Chat.
- Los resultados se documentan en PRs y commits.
- La versión del agente se rastrea por hash de Git del archivo `.prompt.md`.

## Evaluación

Para evaluar si un agente funciona correctamente:

1. Crear casos de prueba con entrada y salida esperada.
2. Ejecutar el agente con cada caso.
3. Comparar la salida real vs. esperada.
4. Registrar falsos positivos y negativos.
5. Ajustar las instrucciones del agente según hallazgos.
6. Versionar el cambio con pull request.

## Evolución

| Versión | Descripción |
|---|---|
| v0 | Prompt simple con instrucciones fijas (actual) |
| v1 | Agregar variables `{{input}}` para contexto dinámico |
| v2 | Conectar herramientas externas vía MCP si la complejidad lo requiere |
| v3 | Flujo multi-agente con orquestación automática |
