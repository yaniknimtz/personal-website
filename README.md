# yaniknimtz.com

Personal academic website of Yanik Nimtz (PhD candidate in Economics, Universitat Rovira i Virgili), built for the 2027–2028 academic job market.

Static site made with [Hugo](https://gohugo.io/) and a small custom theme in this repository. Hosted on GitHub Pages and deployed automatically by GitHub Actions. There is no database and no JavaScript framework: content is plain YAML and Markdown.

## Run it on your computer

1. Install **Hugo extended, version 0.170.1** (the version the deployment uses): <https://gohugo.io/installation/>. Check with `hugo version`.
2. In this folder, run:

   ```bash
   hugo server
   ```

3. Open <http://localhost:1313>. The page reloads automatically when you save a file.

Before pushing, you can check that the site builds exactly as it will online (any warning stops the build):

```bash
hugo --minify --panicOnWarning
```

## Where the content lives

| What | File |
|---|---|
| Name, title line, job market banner, email, address, profile links, skills | `data/profile.yaml` |
| Bio (home page text) | `content/_index.md` |
| Job market paper, publications, work in progress, presentations | `data/research.yaml` |
| Teaching | `data/teaching.yaml` |
| References (letter writers) | `data/references.yaml` |
| PDFs (CV, papers) | `static/files/` |
| Photo and JMP figure | `assets/img/` |
| Page titles and descriptions | front matter of `content/*.md`; site-wide in `hugo.toml` |
| Design | `assets/css/main.css` and `layouts/` |

Text fields in `data/research.yaml` accept Markdown, e.g. `**bold**`. Empty sections and empty fields are hidden automatically.

## Common updates

**Replace the CV.** Export the *web version* (no date of birth, no WhatsApp number). Save it over `static/files/Yanik_Nimtz_CV.pdf`, keeping exactly that file name so links in emails keep working. Then set `cv_updated` in `data/profile.yaml` (e.g. `"January 2027"`).

**Update the job market paper.** Save the new PDF over `static/files/Nimtz_Teruel_JMP_MSR_Firm_Profitability.pdf`. In `data/research.yaml`, update `jmp.updated` and `jmp.pdf_label`. Never name the journal the paper is submitted to, anywhere on the site.

**Add a publication.** Copy an entry under `publications:` in `data/research.yaml` and edit it. If the article is open access, put the PDF in `static/files/` and set `pdf: "/files/<name>.pdf"`; otherwise leave `pdf: ""`. When a working paper is published, move it from `work_in_progress:` to `publications:`.

**Add volume/issue/pages** to the Business Strategy and the Environment article once they are assigned: fill `volume`, `issue` and `pages` in `data/research.yaml`.

**Add a presentation.** Add an entry at the top of `presentations:` (newest first). Use `paper: "JMP"` for talks on the job market paper.

**Job market banner on/off.** Set `on_market: true` or `false` in `data/profile.yaml`.

**Show another reference.** In `data/references.yaml`, fill in the person's details and set `show: true`. Ask the person first.

**Add Google Scholar, SSRN, RePEc/IDEAS or GitHub.** Paste the profile URL into `links:` in `data/profile.yaml`. The icon appears automatically.

**Change the photo.** Replace `assets/img/headshot.jpeg` (portrait, roughly 4:5, at least 600 px wide). Hugo crops and compresses it.

## Publishing

Pushing to the `main` branch publishes the site. GitHub Actions (`.github/workflows/deploy.yml`) builds it with the pinned Hugo version and deploys it to GitHub Pages; this takes about a minute. Progress is visible under the repository's **Actions** tab. Pull requests are built too (without publishing), so a broken change shows up as a failed check before it is merged.

### One-time setup

1. GitHub repository → **Settings → Pages → Build and deployment → Source: GitHub Actions**.
2. Push to `main` (or run the workflow from the **Actions** tab). The site is at <https://yaniknimtz.github.io/> once the repository is named `yaniknimtz.github.io` (otherwise at `https://yaniknimtz.github.io/<repository-name>/`). The workflow picks up the correct address automatically, so no configuration change is needed when the repository is renamed or the custom domain goes live.

### Custom domain `yaniknimtz.com`

1. Buy `yaniknimtz.com` at any registrar (e.g. Cloudflare Registrar, Porkbun, Namecheap). If the .com is taken, use `.eu` or `.net` and change `baseURL` in `hugo.toml` and `static/CNAME`.
2. **Verify the domain first** (prevents domain takeover): GitHub → your profile picture → **Settings → Pages → Add a domain**. GitHub shows a `TXT` record to add at your registrar; add it, then click **Verify**.
3. At your registrar, add these DNS records. **Check the addresses against GitHub's current documentation before saving them**: <https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site>

   | Type | Name | Value |
   |---|---|---|
   | A | `@` | `185.199.108.153` |
   | A | `@` | `185.199.109.153` |
   | A | `@` | `185.199.110.153` |
   | A | `@` | `185.199.111.153` |
   | CNAME | `www` | `yaniknimtz.github.io` |

   Optional IPv6 `AAAA` records for `@` are listed on the same GitHub page.
4. Repository → **Settings → Pages → Custom domain**: enter `yaniknimtz.com` and save.
5. When DNS has propagated (minutes to hours) and GitHub shows the domain check as successful, tick **Enforce HTTPS**.
6. After launch: submit `https://yaniknimtz.com/sitemap.xml` in Google Search Console, and add the URL to ORCID, LinkedIn, the CV and your email signature.

`static/CNAME` contains `yaniknimtz.com`. GitHub takes the custom domain from the repository settings when deploying with Actions, so the file is only a record of the domain.

### Upgrading Hugo

Change `HUGO_VERSION` in `.github/workflows/deploy.yml`, install the same version locally, and run `hugo --minify --panicOnWarning`. If it builds without warnings, commit.

## Privacy

The repository is public: everything committed here can be seen by anyone, including old versions. Never commit preliminary drafts, unpublished PDFs, the date of birth, the WhatsApp number or any credentials. There are no analytics or cookies. If analytics are ever wanted, use a privacy-friendly service such as GoatCounter rather than Google Analytics.

## Credits

Icons: [Simple Icons](https://simpleicons.org/) (CC0) and [Bootstrap Icons](https://icons.getbootstrap.com/) (MIT); see `assets/icons/README.md`.
