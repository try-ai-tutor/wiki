# try-ai-tutor wiki

Public landing page + platform documentation for [try-ai-tutor](https://github.com/try-ai-tutor).

Lives at **https://try-ai-tutor.github.io/wiki/** once GitHub Pages is enabled.

## Stack

[Hugo](https://gohugo.io) (extended), deployed to GitHub Pages via `.github/workflows/hugo.yml`.
English-only for v0. No theme — inline `layouts/` and a small `static/css/style.css`.

## Local preview

```bash
hugo server -D
# open http://localhost:1313/wiki/
```

## Deploy

Push to `main`. The workflow builds and deploys. A commit SHA + date shows in the footer.

## Scope

This wiki is **platform-generic** — anything a new adopter would want to read. Course-specific
operational state (per-semester assignment schedules, cohort stats) lives in the private
`try-ai-tutor/sync-assignments-wiki` repo.
