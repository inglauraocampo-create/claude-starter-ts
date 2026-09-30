## Claude Starter README

## Skills de Claude Code

- `/test [filtro]`: corre los tests con Vitest y, si algo falla, diagnostica la causa sin modificar código.
- `/diff-review [foco]`: revisa el diff local (`git diff HEAD` + archivos sin trackear) contra una checklist de tipos, manejo de errores, tests faltantes y secretos, y devuelve una tabla de severidad.
  - Se llama `diff-review` y no `review` ni `code-review` porque ambos nombres ya son comandos integrados de Claude Code.
