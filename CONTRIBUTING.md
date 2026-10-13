# Cómo contribuir

Este repositorio usa **Gitflow**. La rama `main` es la versión estable y está
**protegida**: no admite push directo, todo entra por Pull Request.

## Ramas

| Rama | Para qué | Sale de | Se fusiona en |
|---|---|---|---|
| `main` | Versión estable / publicable | — | — |
| `develop` | Integración del trabajo en curso | `main` | `main` (al cerrar release) |
| `feature/<tema>` | Nueva función o mejora | `develop` | `develop` |
| `release/<version>` | Preparar una entrega | `develop` | `main` y `develop` |
| `hotfix/<tema>` | Arreglo urgente sobre estable | `main` | `main` y `develop` |

`main`, `develop`, `release/*` y `hotfix/*` están protegidas: sin push directo,
sin borrado y sin reescritura de historial. Las ramas `feature/*` son de trabajo
y se borran al mergear.

## Flujo típico

```bash
git switch develop && git pull
git switch -c feature/lo-que-sea
# ...trabajas y commiteas...
git push -u origin feature/lo-que-sea
gh pr create --base develop --fill
```

## Commits

Formato corto estilo Conventional Commits: `tipo(alcance): resumen`
(`feat`, `fix`, `docs`, `chore`, `refactor`).

## Reglas del proyecto que no se negocian

- **Nada de secretos al repo:** `.env`, claves y tokens quedan fuera por
  `.gitignore`. Solo `.env.example` con valores falsos.
- **`src/` y `tests/` no se mezclan:** el dev nunca toca tests, testing nunca
  toca src (regla R2).
- **Sin APROBADO de QA no hay entrega** (regla R4).
