# Empresa virtual de software (instrucciones del proyecto)

Empresa multi-proyecto sin stack fijo. El usuario da una idea cruda al Director
Técnico y la empresa la convierte en software corriendo.

## Cómo se trabaja

- **Multi-proyecto** con portafolio vivo (`empresa/portafolio.md`).
- El **Director Técnico** es el único que habla con el usuario. Los otros nueve
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
.opencode/agents/             # los 10 agentes
.opencode/opencode.json       # modelo por defecto (Google) + agente primario
.opencode/plugins/            # cadena de respaldo de modelos
empresa/
  README.md                   # guía rápida de uso
  config/politica.md          # reglas inviolables R1-R14
  config/modelos.md           # modelos de IA y cadena de respaldo
  portafolio.md               # todos los proyectos y su estado
  proyectos/_indice.md        # índice de proyectos
  proyectos/<slug>/           # brief.md + cambios.md + vN/
  proyectos/<slug>/vN/        # 9 documentos + tareas + registro + evidencias/
  plantillas/                 # plantillas de los 12 documentos
proyectos/
  <slug>/vN/src/              # código (solo el dev lo toca)
  <slug>/vN/tests/            # tests (solo testing los toca)
docs/
  arquitectura.html           # diagrama interactivo del sistema
```

## Flujo por versión (lo orquesta el Director)

1. `brief.md` — el Director guarda la idea cruda.
2. **Investigador de Stack** → `investigacion.md` (evidencia + matriz + Plan B).
3. **Analista de Requerimientos** → `requerimientos.md` (RF/RNF/CU/RB/DU + matriz).
4. **Arquitecto de Software** → `arquitectura.md` (ADRs con trade-offs).
5. **Diseñador UX/UI** → `diseno_uxui.md` (15 reglas + checklist anti-errores).
6. **Desarrollador Fullstack** → `src/` + `README.md` corriendo en local.
7. **Ingeniero de Testing** → `tests/` + `test_reporte.md` (cobertura ≥70%).
8. **Control de Calidad** → `qa_reporte.md` (APROBADO o CAMBIOS, bloquea).
9. **Hacker Ético** → `pentest_reporte.md` (SEGURO o VULNERABLE, bloquea).
   Si VULNERABLE: fullstack → testing → QA → re-test.
10. **DevOps / Documentador** → `entrega.md` fase local; fase Docker/despliegue
    solo con OK del usuario.
11. Mantenimiento → `cambios.md` + tareas nuevas + regresión (R13) + re-test.

## Contrato de archivos (resumen)

- `investigacion.md`: requisitos, matriz ponderada, madurez, TCO, trade-offs,
  ganador + Plan B, PoCs, vigencia.
- `requerimientos.md`: objetivo, MVP, fuera de alcance, RF/RNF, CU, entidades,
  RB, DU, gaps, matriz RF↔CU↔RB↔ENT.
- `arquitectura.md`: árbol de `src/`, DB, API/endpoints, ADRs con trade-offs,
  checklist anti-errores.
- `diseno_uxui.md`: flujos, pantallas, componentes, accesibilidad, criterios +
  checklist 15 reglas y anti-errores.
- `test_reporte.md`: casos TC-01…, cobertura %, comando, fallos.
- `qa_reporte.md`: veredicto, alcance, AC verificados, bloqueantes con
  evidencia, regresión, rationale, a quién se devuelve.
- `pentest_reporte.md`: control ID, autorización, alcance, hallazgos con
  severidad y custodia, rationale, re-test.
- `entrega.md`: fase local + fase despliegue (con OK fechado).
- `tareas.md` + `registro.md`: cola T-01… y trazabilidad (solo el Director).

## Salidas cortas

Cada subagente responde al Director con **≤ 12 líneas**: qué hizo, rutas de
archivos, dudas y bloqueos. El detalle vive en los archivos.

## Límites honestos

- Sin APROBADO de QA no hay entrega. Sin SEGURO del hacker no hay despliegue.
  Sin suite verde de tests, QA ni entra.
- Los modelos gratis pueden fallar o ir lento; la cadena de respaldo cubre
  cuotas y caídas. Si algo no se puede, se dice claro.
