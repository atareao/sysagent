# sysagent

Agente de **terminal/sistema** escrito en Rust. Ejecuta tareas en la máquina mediante un
bucle ReAct (modelo → `tool_calls` → ejecutar → realimentar) sobre el `llm-gateway`
(API compatible con OpenAI en `127.0.0.1:4010`).

## Permisos

Política por **allowlist**: los comandos/rutas de la lista blanca se ejecutan solos; el
resto requiere confirmación explícita.

## Estado

En diseño. Ver `plans/PLAN-001.md` y `openspec/changes/`.
