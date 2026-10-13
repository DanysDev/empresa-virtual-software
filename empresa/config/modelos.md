# Modelos y respaldo de la empresa

Misma cadena que la agencia. Todo gratis: Google AI Studio + OpenCode ZEN.

## Cadena de modelos

| Orden | Modelo | Notas |
|-------|--------|-------|
| Principal | `google/gemini-3.8-flash` | Fijado en cada agente y en `.opencode/opencode.json` |
| Respaldo 1 | `opencode/big-pickle` | ZEN gratis, el más fuerte |
| Respaldo 2 | `opencode/nemotron-3-ultra-free` | ZEN gratis, segundo |

El respaldo entra solo si el principal falla de forma recuperable (429, 5xx,
timeout, red).

## Reglas y límites (comprobados en la v2.0.26)

- ⚠️ **Nunca pongas `shell: deny` en un agente.** La capa gratis de ZEN rechaza
  la petición con `403 FreeTierError` cuando la herramienta `shell` no va en la
  petición. Si quieres frenar el shell, usa `effect: ask`, que sí funciona.
- `edit: deny` sí es seguro (los respaldos de ZEN funcionan con eso).
- Los cortes de socket sin clasificar (`error.type = unknown`) no pasan por el
  hook de reintento: si la sesión muere así, hay que volver a lanzarla.
- La cuota gratis de Google AI Studio se agota con facilidad; el respaldo está
  para eso.

## Trazas y ajustes

- Traza del respaldo: `/tmp/opencode/model-fallback.log`
  (pon `EMPRESA_FALLBACK_DEBUG=0` para silenciarla).
- Para cambiar la cadena: edita la constante `CADENA_POR_DEFECTO` en
  `.opencode/plugins/model-fallback.ts` y, si cambias el principal, también los
  `model:` de los 9 agentes y `.opencode/opencode.json`.

## Cobertura del plugin

`.opencode/plugins/model-fallback.ts` cubre a los 7 de la agencia + los 9 de la
empresa (Director Técnico y 8 especialistas). Si cambias el principal, cambia
los `model:` de los 16 agentes + `opencode.json` + `CADENA_POR_DEFECTO`.
