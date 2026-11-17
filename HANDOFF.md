# HANDOFF — sysagent (MVP)

**Fecha:** 2026-11-17 · **Estado:** proyecto arrancado, diseño SDD PENDIENTE · **Issue:** [#1](https://github.com/atareao/sysagent/issues/1)

## Qué se ha hecho

- Repo nuevo `atareao/sysagent` (público) con gitflow (`main` + `development`).
- `openspec init` (tools: opencode, idioma: es) → `openspec/`, `.opencode/`.
- Issue #1 con contexto, decisiones, alcance y criterios de aceptación.

## Decisiones tomadas (no re-decidir)

- **Runtime:** binario propio en Rust, estilo `llm-gateway` (`tokio` + `reqwest` + `serde` + `clap`).
- **Permisos:** allowlist — lo permitido se ejecuta solo; el resto pide confirmación explícita.
- **Tools v1:** `run_shell`, `read_file`, `write_file`, `list_dir`, `systemctl` (`--user`), `git`.
- **Modelo:** vía ruta del gateway (p. ej. `local-agent`) → fallback OpenRouter. Aprovechar el failover de tool-calls del gateway.
- **Interacción:** CLI interactivo + modo one-shot (`--one-shot`, `--model`, `--max-steps`, `--json`).

## Siguiente paso (PRIMERA ACCIÓN de la próxima sesión)

Generar la propuesta SDD y el plan, y **parar a esperar aprobación**:
1. `openspec new change add-mvp-agent` (o `/opsx-propose`) → `proposal.md`, `specs/sysagent/spec.md`, `tasks.md`.
2. `plans/PLAN-001.md` referenciando el issue #1.
3. Presentar al usuario. NO escribir código hasta aprobación.

## Contratos a definir en el spec

- Formato de la config local `~/.config/sysagent/config.toml`: `[gateway]` (base_url, model, api_key) y `[permissions] allowlist = [...]`.
- Semántica de confirmación (UX en terminal) y qué se considera "destructivo".
- JSON Schema de cada tool (nombre, args, resultado) para el `tools` de la API.
- Códigos de salida y logging.

## Notas de entorno

- Memoria de máquina: VRAM 16 GB, ya ~14,9 GB (Ollama + LocalAI). Preferir modelos pequeños (4B/9B) con escalado al remoto.
- Trampa LocalAI: mantiene modelos residentes hasta su watchdog (5m).
- El `llm-gateway` ya tiene failover de tool-calls (`add-toolcall-failover`): red de seguridad de fiabilidad para el agente.

## Cómo retomar

```bash
cd /data/rust/sysagent && git checkout development && git pull
gh issue view 1 -R atareao/sysagent
openspec list
```
