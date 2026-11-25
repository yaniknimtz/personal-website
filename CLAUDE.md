# Notes for Claude sessions

Academic job market website for Yanik Nimtz. Hugo static site, custom theme in `layouts/`, deployed to GitHub Pages by `.github/workflows/deploy.yml` on pushes to `main`. `PLAN.md` is the original build plan; `README.md` has the how-to for every routine update (CV, papers, references, banner, domain).

## Rules

- **Do not invent facts.** Titles, co-authors, dates, journals, referees and numbers come from Yanik or `PLAN.md` section 4. If something is unknown, ask.
- **Never name the journal the job market paper is submitted to**, anywhere (pages, metadata, commit messages).
- **Never commit** the preliminary drafts (carbon leakage, certification papers), the date of birth, the WhatsApp number or credentials. The repo is public.
- Site text about Yanik is in the first person ("I", "my"); the meta description is the exception.
- Pelin Demirel stays `show: false` in `data/references.yaml` until Yanik confirms.
- PDF file names in `static/files/` are stable. Replace files in place; don't rename.

## Layout

- Content is data-driven: `data/profile.yaml`, `research.yaml`, `teaching.yaml`, `references.yaml`. The bio is `content/_index.md`; `content/research.md` and `content/teaching.md` hold front matter only.
- Templates use Hugo's current layout structure: `layouts/baseof.html`, `home.html`, `page.html`, `research.html`, `teaching.html`, `404.html`, and partials in `layouts/_partials/`. `research` and `teaching` are selected with `layout:` in front matter.
- `paper.html` renders one paper for `kind` = `jmp` | `publication` | `wip`. `links.html` renders profile links; empty URLs are skipped.
- Icons are SVG files in `assets/icons/`, inlined by `icon.html`.
- Emails go through `email.html` ("user [at] domain"), and an inline script in `email-script.html` turns them into mailto links.

## Gotchas

- Use `hugo.Data`, not `site.Data` (deprecated since Hugo 0.156; the build fails on warnings).
- `relURL` treats a leading `/` as host-relative, which breaks the `github.io/personal-website/` subpath. Data paths start with `/`, so use `strings.TrimPrefix "/" . | relURL`.
- `disablePathToLower = true` in `hugo.toml` keeps `/files/Yanik_Nimtz_CV.pdf` case-sensitive-correct; without it Hugo lowercases menu URLs.
- The workflow passes `--baseURL` from `actions/configure-pages`, so `baseURL` in `hugo.toml` only matters locally.

## Checks before committing

```bash
hugo --minify --panicOnWarning
```

Also, as done at launch: lychee (internal links and fragments), axe-core (WCAG 2.1 AA), Lighthouse ≥ 95 on Home and Research (mobile and desktop), and no horizontal scroll at 360, 768 and 1280 px.
