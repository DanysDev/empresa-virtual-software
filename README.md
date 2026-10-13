# Empresa Virtual de Software

**Un equipo multiagente que convierte una idea cruda en software corriendo.**
Sin stack fijo, multi-proyecto, con testing independiente, regresión obligatoria
y un QA que bloquea entregas.

Todo con modelos de IA **gratuitos** (Google AI Studio + OpenCode ZEN) sobre
**OpenCode V2**, colaboración **por archivos** (auditable y barata en tokens) y
reglas inviolables que separan poderes: quien escribe código nunca toca los tests.

> **🇬🇧 Summary (EN).** A 9-role virtual software company built on **OpenCode V2**
> (multi-project, no fixed stack) that turns raw ideas into running code: stack
> research with live docs, requirements, architecture, UX/UI design, fullstack
> build, independent testing (≥70% coverage + regression suite) and a blocking QA
> gate. File-based collaboration, free-tier models with a local fallback chain.

*Diagrama interactivo del sistema (zoom, temas claro/oscuro): `docs/arquitectura.html`.*

## El problema

Convertir una idea de software en código real exige varios oficios (investigar el
stack, especificar, diseñar la arquitectura y la interfaz, codificar, testear,
auditar, desplegar) que un solo prompt no cubre con calidad. Esta empresa reparte
cada oficio a un especialista con rol cerrado, contrato de archivos y un gate de
calidad que puede devolver el trabajo.

## Los 9 agentes

Un **Director Técnico** (agente primario, única autoridad) habla contigo, gestiona
el portafolio y reparte las tareas. Los otros ocho son subagentes independientes.

| Agente | Rol | Qué entrega |
|---|---|---|
| **Director Técnico** | Única autoridad: portafolio, tareas, historial y reparto | `brief.md`, `tareas.md`, `registro.md` |
| **Investigador de Stack** | Compara 2-3 stacks con documentación actual (Context7 obligatorio) | `investigacion.md` |
| **Analista de Requerimientos** | Convierte la idea en MVP, casos de uso y reglas de negocio | `requerimientos.md` |
| **Arquitecto de Software** | Diseño técnico que el dev debe respetar | `arquitectura.md` |
| **Diseñador UX/UI** | Flujos, pantallas y criterios medibles que QA validará | `diseno_uxui.md` |
| **Desarrollador Fullstack** | Construye el código (nunca toca `tests/`) | `proyectos/<slug>/vN/src/` |
| **Ingeniero de Testing** | Tests independientes + regresión, cobertura ≥70% (nunca toca `src/`) | `tests/` + `test_reporte.md` |
| **Control de Calidad** | Auditor final: funcional + UX/UI + regresión. **Bloquea entregas** | `qa_reporte.md` (APROBADO o CAMBIOS) |
| **DevOps / Documentador** | Local primero; Docker/despliegue **solo con tu OK** | `entrega.md` |

## Cómo funciona

**Multi-proyecto con versiones aisladas.** Gestión en `empresa/proyectos/<slug>/`,
código en `proyectos/<slug>/vN/` (`vN` no rompe `vN-1`):

```
idea ─▶ Director ─┬─▶ Investigador ──▶ stack ganador (con docs actuales)
                  ├─▶ Analista ──────▶ MVP + CU-01… + reglas
                  ├─▶ Arquitecto ────▶ carpetas, DB, API
                  ├─▶ Diseñador ─────▶ pantallas + criterios medibles
                  ├─▶ Fullstack ─────▶ src/ corriendo en local
                  ├─▶ Testing ───────▶ suite ≥70% + regresión
                  ├─▶ QA ────────────▶ APROBADO (bloqueante) / CAMBIOS
                  │                       │
                  │            CAMBIOS ───┘ vuelve al responsable
                  └─▶ DevOps ────────▶ entrega local ──tu OK──▶ Docker/despliegue
```

Mantenimiento: bugfix/feature → `cambios.md` + tareas nuevas → dev → testing con
regresión completa → QA → devops. Nada que funcionaba se rompe en silencio.

**La comunicación es por archivos, no por chat.** Cada subagente lee lo que dejó
el anterior y escribe su parte. El Director solo recibe resúmenes cortos (≤12
líneas): auditable, barato en tokens y reanudable.

## Reglas inviolables

Detalle en [`empresa/config/politica.md`](empresa/config/politica.md):

- **R2** Separación total dev/testing (`src/` solo el dev, `tests/` solo testing)
- **R3** Cobertura mínima 70% · **R13** regresión obligatoria en cada cambio
- **R4** QA bloquea: sin APROBADO no hay entrega
- **R5** Despliegue en 2 fases, solo con OK explícito
- **R6** Cero secretos en repo (solo `.env.example`)
- **R11** Código legible en inglés, nombres descriptivos
- **R12** Solo el Director decide y reparte

## Estrategia de modelos y resiliencia

Todo con **capas gratuitas**:

| Orden | Modelo | Proveedor |
|---|---|---|
| Principal | `google/gemini-3.8-flash` | Google AI Studio (capa gratis) |
| Respaldo 1 | `opencode/big-pickle` | OpenCode ZEN (gratis) |
| Respaldo 2 | `opencode/nemotron-3-ultra-free` | OpenCode ZEN (gratis) |

OpenCode V2 admite **un solo modelo por agente**, sin respaldo nativo. Un
**plugin local en TypeScript** (`.opencode/plugins/model-fallback.ts`) engancha el
evento de reintento, clasifica el error (cuota, 429/5xx, timeout, red) y cambia al
siguiente modelo de la cadena. Cubre a los 9 agentes.

## Estructura del repositorio

```
AGENTS.md                        # manual del proyecto
.opencode/
  opencode.json                  # modelo por defecto + agente primario
  agents/*.md                    # los 9 agentes: prompt + modelo + permisos
  plugins/model-fallback.ts      # cadena de respaldo de modelos
empresa/
  README.md                      # guía rápida de uso
  config/politica.md             # reglas inviolables R1-R13
  config/modelos.md              # modelos y cadena de respaldo
  portafolio.md                  # todos los proyectos y su estado
  proyectos/_indice.md           # índice de proyectos
  proyectos/<slug>/              # brief.md + cambios.md + vN/
  plantillas/                    # plantillas de los 11 documentos
proyectos/
  <slug>/vN/src/                 # código · tests/ · README · .env.example
docs/
  arquitectura.html              # diagrama interactivo del sistema
.github/
  CODEOWNERS                     # dueño del repo
  pull_request_template.md       # plantilla de PR
CONTRIBUTING.md                  # flujo de ramas (Gitflow)
LICENSE                          # MIT
```

> **Nota de privacidad:** el repo es público. Los docs internos por proyecto
> (`empresa/proyectos/<slug>/`) quedan en local por `.gitignore`; el sistema
> (agentes, reglas, plantillas) y el código de `proyectos/` sí se versionan.

## Cómo se monta

1. Instala **OpenCode V2** (app de escritorio o CLI) y conecta un proveedor de
   **Google AI Studio** con su clave (capa gratis).
2. Abre este proyecto. Los agentes y el plugin se cargan solos desde `.opencode/`.
3. Abre sesión con el **Director Técnico** y mándale tu idea: qué quieres, para
   quién, restricciones.
4. Te devuelve el proyecto corriendo en local + `entrega.md`. Pruébalo; el
   despliegue espera tu OK.

## Ramas y flujo de trabajo

Gitflow, con `main` como rama estable y protegida:

| Rama | Para qué |
|---|---|
| `main` | Versión estable / publicable (protegida: sin push directo, todo por PR) |
| `develop` | Integración del trabajo en curso (protegida: sin push directo, todo por PR) |
| `feature/<tema>` | Nueva función o mejora → PR a `develop` |
| `release/<version>`, `hotfix/<tema>` | Cierre de versión y arreglos urgentes (protegidas) |

Todo entra por **Pull Request** revisado por el dueño. Detalle en
[`CONTRIBUTING.md`](CONTRIBUTING.md). Escaneo de secretos y protección de push
activados.

## Notas técnicas

- **Stack:** OpenCode V2 (agentes en Markdown + plugin TypeScript), datos en
  Markdown, diagramas en HTML.
- **Separación de poderes:** dev y testing no pueden tocarse el código
  mutuamente ni por permisos ni por reglas; la regresión es obligatoria.
- Tono técnico directo en español neutro; código y comentarios en inglés.

## Licencia

MIT — ver [`LICENSE`](LICENSE).
