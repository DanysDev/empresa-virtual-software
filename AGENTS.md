# Empresa virtual de software (instrucciones del proyecto)

Empresa multi-proyecto sin stack fijo. El usuario da una idea cruda al Director
Técnico y la empresa la convierte en software corriendo.

## Cómo se trabaja

- **Multi-proyecto** con portafolio vivo (`empresa/portafolio.md`).
- El **Director Técnico** es el único que habla con el usuario. Los otros ocho
  son **subagentes** que el Director lanza.
- La comunicación entre agentes es por **archivos** (pizarra compartida): gestión
  en `empresa/proyectos/<slug>/`, código en `proyectos/<slug>/vN/`.
- Cada subagente escribe su parte y responde al Director con un **resumen corto**.
- La empresa entrega corriendo en **local**; Docker/despliegue solo con el OK
  explícito del usuario.

## Idioma y tono

Técnico directo en **español neutro**. Código y comentarios en **inglés**.

## Estructura del proyecto

```
AGENTS.md                     # este manual
.opencode/agents/             # los 9 agentes
.opencode/opencode.json       # modelo por defecto (Google) + agente primario
.opencode/plugins/            # cadena de respaldo de modelos
empresa/
  README.md                   # guía rápida de uso
  config/politica.md          # reglas inviolables R1-R13
  config/modelos.md           # modelos de IA y cadena de respaldo
  portafolio.md               # todos los proyectos y su estado
  proyectos/_indice.md        # índice de proyectos
  proyectos/<slug>/           # brief.md + cambios.md + vN/
  proyectos/<slug>/vN/        # 8 documentos + tareas + registro
  plantillas/                 # plantillas de los 11 documentos
proyectos/
  <slug>/vN/src/              # código (solo el dev lo toca)
  <slug>/vN/tests/            # tests (solo testing los toca)
docs/
  arquitectura.html           # diagrama interactivo del sistema
```

## Flujo por versión (lo orquesta el Director)

1. `brief.md` — el Director guarda la idea cruda.
2. **Investigador de Stack** → `investigacion.md` (Context7 obligatorio).
3. **Analista de Requerimientos** → `requerimientos.md` (MVP, CU-01…).
4. **Arquitecto de Software** → `arquitectura.md` (contrato para el dev).
5. **Diseñador UX/UI** → `diseno_uxui.md` (criterios medibles).
6. **Desarrollador Fullstack** → `src/` + `README.md` corriendo en local.
7. **Ingeniero de Testing** → `tests/` + `test_reporte.md` (cobertura ≥70%).
8. **Control de Calidad** → `qa_reporte.md` (APROBADO o CAMBIOS, bloquea).
9. **DevOps / Documentador** → `entrega.md` fase local; fase Docker/despliegue
   solo con OK del usuario.
10. Mantenimiento → `cambios.md` + tareas nuevas + regresión completa (R13).

## Contrato de archivos (resumen)

- `investigacion.md`: 2-3 stacks comparados, ganador justificado, riesgos.
- `requerimientos.md`: objetivo vN, MVP, fuera de alcance, casos, entidades,
  reglas, dudas.
- `arquitectura.md`: árbol de `src/`, DB, API/endpoints, decisiones AD-01….
- `diseno_uxui.md`: flujos, pantallas, componentes, accesibilidad, criterios.
- `test_reporte.md`: casos TC-01…, cobertura %, comando, fallos.
- `qa_reporte.md`: veredicto, checklist, problemas, a quién se devuelve.
- `entrega.md`: fase local + fase despliegue (con OK fechado).
- `tareas.md` + `registro.md`: cola T-01… y trazabilidad (solo el Director).

## Salidas cortas

Cada subagente responde al Director con **≤ 12 líneas**: qué hizo, rutas de
archivos, dudas y bloqueos. El detalle vive en los archivos.

## Límites honestos

- Sin APROBADO de QA no hay entrega. Sin suite verde de tests, QA ni entra.
- Los modelos gratis pueden fallar o ir lento; la cadena de respaldo cubre
  cuotas y caídas. Si algo no se puede, se dice claro.
