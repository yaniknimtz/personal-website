# Project plan: Yanik Nimtz – academic job market website

**Owner:** Yanik Nimtz · **Purpose:** personal academic website for the academic job market (PhD expected late summer 2027) · **Plan version:** 24 Nov 2026, v4

This file is written to be handed directly to Claude Code. It is self-contained: Claude Code should read it top to bottom, follow the phases in section 8 in order, and stop at the points marked **[ASK YANIK]**.

**All site content is in section 4.** Claude Code must use that text as written (it has been drafted from Yanik's CV and papers) and must **not invent** any further facts, titles, co-authors, journals, dates or referees. Anything still unknown is marked `TODO` and listed in section 13.

---

## 1. Goal and success criteria

Build a fast, clean, professional static website that a hiring committee member can scan in under 30 seconds and find:

1. Who Yanik is, where he is, and that he is on the job market.
2. The **job market paper** (title, key findings, abstract, PDF) without scrolling far.
3. The **CV as a PDF**.
4. The publication, work in progress, teaching and contact details.
5. The reference (letter writer).

The site is done when every item in the **Final checklist** (section 12) is ticked.

---

## 2. Input files

Yanik's files are in the folder `inputs/` next to this plan. Copy them into the repo as follows:

| Input file | Use | Published path in the site |
|---|---|---|
| `inputs/headshot.jpeg` (1023×1278 px, portrait) | Home page photo | processed by Hugo from `assets/img/headshot.jpeg` |
| `inputs/Yanik_Nimtz_CV.pdf` | CV download | `/files/Yanik_Nimtz_CV.pdf` |
| `inputs/Nimtz_Teruel_MSR_Firm_Profitability.pdf` | Job market paper | `/files/Nimtz_Teruel_JMP_MSR_Firm_Profitability.pdf` |
| `inputs/Nimtz_Teruel_2026_Corporate_Decarbonization_BSE.pdf` | Published article (open access, CC BY-NC, so it may be hosted) | `/files/Nimtz_Teruel_2026_Corporate_Decarbonization_BSE.pdf` |
| `inputs/jmp_roa_event_study.png` | JMP event-study figure (4.4) | processed from `assets/img/jmp_roa_event_study.png` |

The two preliminary drafts (carbon leakage, certification) are **not** given to Claude Code and must never be in the repository. Section 4 already contains everything the site needs from them. The repository is public, so anything committed to it can be seen by anyone.

Filenames are stable (no dates or version numbers), so links sent by email never break. To update a file later, overwrite it with the same name.
check for the correct names online in guthub

---

## 3. Tech stack

**Hugo (static site generator) with a small custom theme written in this repo, hosted on GitHub Pages, deployed by GitHub Actions, on the custom domain `yaniknimtz.com`.**

Why:

- **Free, permanent hosting** that does not disappear when Yanik leaves URV.
- **Content in plain Markdown and YAML.** Adding a paper or replacing the CV is a text edit plus a push. No database, no CMS.
- **Single binary, fast builds**, no Ruby/Node dependency chains to break.
- **Custom minimal theme instead of a third-party academic theme** (Hugo Blox, al-folio). Those are heavy and have had breaking upgrades; a few hand-written templates are easier to maintain, and job market sites in economics are deliberately simple.

Pin the current Hugo *extended* release in the GitHub Actions workflow so builds are reproducible.

---

## 4. Site content (ready to use)

### 4.1 Site-wide

- **Name:** Yanik Nimtz
- **Title line:** PhD Candidate in Economics, Universitat Rovira i Virgili (confirmed by Yanik)
- **Job market banner (Home, top):** "I am on the 2026–2027 academic job market and will complete my PhD in late summer 2027."
- **Site `<title>` / meta description:** "Yanik Nimtz | Economics PhD Candidate, Universitat Rovira i Virgili" / "Yanik Nimtz is an economics PhD candidate at Universitat Rovira i Virgili working on environmental economics, climate policy and the EU Emissions Trading System. Job market paper, CV and research."
- **Language:** English.

### 4.2 Bio (Home page)

Use this text exactly. It is written in the first person, as Yanik asked, and is based on his own draft, expanded with his papers and CV:

> I am a PhD candidate in Economics at the Universitat Rovira i Virgili (URV) in Reus, Spain, supervised by Mercedes Teruel, and a member of the research groups GRIT and ECO-SOS. My research lies at the intersection of environmental economics, climate policy and the economics of innovation. I study how carbon pricing and environmental regulation affect firms: their profitability, their greenhouse gas emissions, and where those emissions take place.
>
> My job market paper shows that the tightening of the EU Emissions Trading System through the Market Stability Reserve temporarily reduced the profitability of regulated firms, which then adjusted through higher labour productivity and lower employment. My other work examines the drivers of corporate decarbonization in OECD countries, carbon leakage within multinational firms under high carbon prices, and the effect of innovation certificates on the growth of Spanish SMEs. I combine large firm-level datasets (EU Transaction Log, Orbis, CDP, Compustat, Refinitiv) with quasi-experimental methods such as difference-in-differences with entropy balancing and event studies.
>
> In 2026 I was a Visiting Research Fellow at Imperial College London. I hold a BSc in General Management from PFH Private University of Applied Sciences Göttingen and two Master's degrees from URV, in International Markets and in Entrepreneurship and Innovation, both awarded the Extraordinary Master's Award. My doctorate, which I started in May 2024, is funded by a Joan Oró (FI) predoctoral grant from the Generalitat de Catalunya.

All other site text that speaks about Yanik (banner, meta description excepted) also uses the first person ("I", "my").

### 4.3 Research interests

- Environmental Economics
- Sustainability
- Innovation Economics

(Optional secondary line, from the CV: "Corporate decarbonization · Climate policy · EU ETS".)

### 4.4 Job market paper

- **Title:** Impact of the Market Stability Reserve on firm profitability
- **Authors:** Yanik Nimtz, Mercedes Teruel
- **Status:** Submitted. (Don't name the journal.)
- **Latest version:** November 2026
- **PDF:** `/files/Nimtz_Teruel_JMP_MSR_Firm_Profitability.pdf`, labelled "Working paper version, November 2026".
  - Yanik has confirmed he may post this PDF on his website. Never name the journal the paper is submitted to, anywhere on the site or in metadata.
- **JEL:** H23, Q54, Q58 · **Keywords:** Climate policy, Difference-in-differences, EU ETS, Financial performance
- **Presented at:** 14th PhD-Student Workshop on Industrial and Public Economics (WIPE), Reus, Feb 2026; 28th Applied Economics Meeting (ALdE), Cádiz, Jun 2026

**Key findings (for the Home page box; improved from Yanik's draft):**

- The 2019 introduction of the Market Stability Reserve tightened the EU ETS and pushed up carbon prices. In 2019 it reduced the return on assets of regulated firms by about **1 percentage point**, but there are no significant losses in later years.
- Firms adjusted with a **two-to-three-year lag** by raising labour productivity and reducing employment. This is a shift from short-run compliance costs, as neoclassical theory predicts, to adaptation, in line with the Porter hypothesis.
- Policy implication: **predictable, long-term reform paths** give firms time to adapt and can avoid sudden profitability shocks. This matters for the current debate on reforming the EU ETS.
- Data and method: 755 EU ETS firms and 10,545 comparable non-regulated firms, 2015–2023, combining EUTL and Orbis Europe. Entropy-balanced difference-in-differences and event study.

**Abstract (Research page, always visible):**

> The European Union Emissions Trading System (EU ETS) is the world's largest carbon market and foundation of climate policy in the EU. While previous research found little evidence that earlier phases of the EU ETS negatively affected regulated firms' economic performance, the 2019 introduction of the Market Stability Reserve (MSR) fundamentally changed the system's allowance dynamics and contributed to a sharp increase in CO₂ prices. This paper investigates whether the MSR directive and the resulting tightening of the EU ETS imposed measurable costs on regulated firms, thereby challenging the previously observed neutrality of the system on firm profitability. We combine data from the European Union Transaction Log (EUTL) with firm-level financial information from the Orbis Europe database and apply entropy balancing to a panel of 755 regulated firms and 10,545 comparable non-regulated firms between 2015 and 2023 to estimate the causal impact of the MSR-era tightening of the EU ETS through a difference-in-difference and event-study approach. Our results indicate that regulated firms experienced a temporary decline in profitability, particularly in the year of the MSR's introduction, while longer-term effects remain limited and statistically insignificant in most specifications. We further find evidence that firms responded through productivity improvements and reductions in employment, which may have partially offset the increased carbon-related cost burden. The findings suggest that the MSR-era tightening created tangible financial pressure on regulated firms, while substantial long-term adverse effects on firms' economic performance are not detected.

**Figure (Research page under the JMP abstract, and optionally a small version in the Home JMP box):** `inputs/jmp_roa_event_study.png` → `assets/img/jmp_roa_event_study.png`, served responsively.
- Caption: "Event-study estimates of the effect of the MSR-era EU ETS tightening on regulated firms' return on assets (percentage points), 2015–2023, relative to 2018. Bars show confidence intervals."
- Alt text: "Event-study chart. The effect on return on assets is close to zero in 2015–2017, drops to about −1 percentage point in 2019, the year the Market Stability Reserve was introduced, and is not statistically different from zero from 2020 to 2023."

### 4.5 Publications

**Nimtz, Y., & Teruel, M. (2026).** Corporate Decarbonization: Understanding CO₂ Emission Drivers Across High- and Low-Polluting Firms in OECD Countries. *Business Strategy and the Environment.* DOI: https://doi.org/10.1002/bse.70849 · Open access · PDF: `/files/Nimtz_Teruel_2026_Corporate_Decarbonization_BSE.pdf`

Abstract (in a collapsible `<details>`):

> Decarbonization of the economy is a central challenge in the fight against climate change. Although most governments show clear commitment to limiting global warming, the drivers of corporate decarbonization remain underexplored. Using a dataset of 1052 firms from OECD, this article analyses how intangible assets and environmental innovation affect corporate environmental performance. By applying bootstrapped quantile regressions, we show how firm- and country-level factors are associated with high- and low-polluting firms. Our results suggest that intangible assets and environmental innovation improve environmental performance across quantiles, with a stronger effect for high-polluting firms. Furthermore, environmental innovation can reduce short-term emission growth. Finally, intangible assets depend on the sectorial CO₂ intensity and have limited significance in sectors with low carbon intensity. At the policy level, our results call for emission-related regulation because it improves corporate decarbonization. Furthermore, it is necessary to have a regulatory strategy that incorporates incentives for intangible asset development and innovation, differentiating between high- and low-polluting firms.

Volume/issue/pages: `TODO` once assigned (currently online-first, 2026).

### 4.6 Work in progress

Both are preliminary drafts: **no PDFs**, short description only. The text is summarised from the drafts.

1. **Does carbon leakage appear under high CO₂ prices? Impact of high carbon prices on emission behaviour of multinationals under the EU ETS**, with Mercedes Teruel and Pelin Demirel (Imperial College London).
   *Description:* Revisits carbon leakage for 2012–2024, when the EU allowance price rose roughly tenfold to over €80. Using CDP scope 1 emissions and Compustat data for 1,722 multinational firms, it finds that EU ETS firms reduce the EU share of their emissions through slower EU emission growth rather than faster growth elsewhere. Firms more exposed to carbon costs cut EU emissions more, with no detectable increase abroad. So far there is no evidence of carbon leakage within multinationals.

2. **The role of certification of innovation on firm growth: an empirical analysis of Spanish SMEs**, with Mercedes Teruel (Teruel listed as first author).
   *Description:* Studies whether Spain's official "innovative SME" certificate signals superior performance. Using 2,525 certified firms and 58,424 controls (2012–2024) with a cohort-stacked entropy-balanced difference-in-differences design, it finds that certification raises sales (about +4.6%) and employment (about +7.6%) in the first three years, while labour productivity falls by about 3.5% in the short run. (Numbers confirmed by Yanik.)

### 4.7 Teaching (from the CV)

| Year | Course | Role | Institution |
|---|---|---|---|
| 2026 | Principles of Applied Economics | Teaching Assistant | Universitat Rovira i Virgili |
| 2025 | Global Economy | Teaching Assistant | Universitat Rovira i Virgili |
| 2024 | Innovation Economy & Innovation Systems | Teaching Assistant | Universitat Rovira i Virgili |
| 2017 | Introduction to Macroeconomics (Review Course) | Instructor | PFH Private University of Applied Sciences Göttingen |

Course levels (undergraduate/master) are `TODO` (optional). **[ASK YANIK]**

### 4.8 Presentations (from the CV, Research page, "Selected presentations")

- 2026: 28th Applied Economics Meeting (ALdE), Universidad de Cádiz, Spain (JMP)
- 2026: 14th PhD-Student Workshop on Industrial and Public Economics (WIPE), Reus, Spain (JMP)
- 2025: KID 2025 Summer School, Université Côte d'Azur, Nice, France
- 2025: PhD Summer School on the Economics of the Green and Digital Transitions, Maastricht University & UNU-MERIT, Netherlands
- 2025: 27th Applied Economics Meeting (ALdE), Universidad de Murcia, Spain
- 2025: II Seminar of PhD Students on Energy and Environment, Chair of Energy Sustainability, Universitat de Barcelona, Spain
- 2025: 6th International PhDays Conference, Ingenio (CSIC-UPV), Valencia, Spain
- 2025: 13th PhD-Student Workshop on Industrial and Public Economics (WIPE), Reus, Spain
- 2024: 9th ECO-SOS Doctorials, Universitat Rovira i Virgili, Reus, Spain
- 2024: 2nd Bi-annual Workshop of the Eco-Innovation Society, HEC Paris, France

### 4.9 Other facts available for the site (from the CV)

- **Visiting:** Visiting Research Fellow, Imperial College London, UK, May–July 2026
- **Affiliations:** Member of ECO-SOS (Research Center on Economics and Sustainability) and GRIT (Research Group of Industry and Territory), URV
- **Grant:** Joan Oró (FI) predoctoral grant, Generalitat de Catalunya, co-funded by the EU (2024–2027)
- **Awards:** Extraordinary Master's Award, International Markets (2021) and Entrepreneurship and Innovation (2022), URV
- **Thesis title:** Sustainability Synergy: Exploring the Nexus of Climate Change, Corporate Social Responsibility, Innovation, and Circular Economy in the Pursuit of Decarbonization
- **Skills** (show as a short "Skills" block at the end of the Home page, or on the CV/Teaching page):
  - **Languages:** German (native) · English (fluent, C1; Master's in International Markets taught in English) · Spanish (fluent, C1; Master's in Entrepreneurship and Innovation taught in Spanish) · Catalan (B1, certified)
  - **Software:** Stata (advanced: panel data econometrics, difference-in-differences, event studies, entropy balancing) · LaTeX (advanced) · Python (working knowledge) · R (basic) · AI-assisted coding and research workflows with Claude Code
    - Note: the Stata and LaTeX levels are from the CV ("professional knowledge") and the methods in the papers. The Python and Claude Code wording is a draft. Yanik should adjust it if he uses them more or less than this.

Do **not** publish the date of birth, the WhatsApp number or anything else personal from the CV.

### 4.10 Contact

- **Email:** yanik.nimtz@urv.cat (render as copyable text; see 10.3)
- **Phone:** +34 622 497 529 (Yanik asked for it to be listed; note that it is a personal mobile)
- **Address:**
  Department of Economics, Faculty of Economics and Business
  Universitat Rovira i Virgili, Campus Bellissens
  Av. de la Universitat 1, 43204 Reus, Spain
  Office: `TODO` (optional) **[ASK YANIK]**
- **Links:**
  - ORCID: https://orcid.org/0009-0005-4239-2289
  - LinkedIn: https://www.linkedin.com/in/yanik-nimtz-14b0bb23a/
  - CV (PDF): `/files/Yanik_Nimtz_CV.pdf`
  - Google Scholar, SSRN, RePEc/IDEAS, GitHub: none yet. Add the data fields but leave them empty so no icon shows. (Recommended: create a Google Scholar profile and a RePEc/IDEAS registration before the market. See section 11.)

### 4.11 References

| Name | Role | Institution | Email |
|---|---|---|---|
| Mercedes Teruel (link name to https://sites.google.com/view/mercedes-teruel-urv) | Full Professor of Economics (PhD supervisor) | Universitat Rovira i Virgili, Department of Economics | mercedes.teruel@urv.cat |
| ~~Pelin Demirel~~ (prepared but **hidden** until Yanik confirms) | `TODO` | Imperial College London, Dyson School of Design Engineering | `TODO` |

Implement references from `data/references.yaml` with a `show: true/false` flag per person, so Pelin Demirel can be switched on later by editing one line.

### 4.12 Placement officer section: leave out

Yanik asked what this is. In US-style economics PhD programmes, the department names a **placement director** (a faculty member who coordinates the job market) and a **placement administrator**, and candidates list them on their website for hiring committees to contact. Many European programmes, including URV as far as we know, do not have this role. **Do not build this section.** If URV's doctoral programme has a job market coordinator, it can be added later as one line in `references.yaml`.

---

## 5. Site structure

Navigation bar on every page: **Home · Research · Teaching · CV** (CV links straight to the PDF and opens in a new tab). Contact details live on Home and in the footer, so no separate Contact page is needed.

```
/            Home
/research/   Job market paper, publications, work in progress, selected presentations
/teaching/   Teaching
/files/Yanik_Nimtz_CV.pdf
/404.html
```

### 5.1 Home page, in this order

1. Photo (left on desktop, top on mobile), crop to 4:5 or a circle, alt text "Photo of Yanik Nimtz".
2. **Name** (H1) and title line.
3. Job market banner (4.1). It is controlled by `profile.yaml: on_market: true`.
4. Bio (4.2).
5. Research interests (4.3).
6. **Job Market Paper box:** title, co-author, key findings bullets (4.4), buttons *Paper (PDF)* and *Abstract* (to `/research/#jmp`).
7. References (4.11).
8. Contact block and icon links (4.10). Add "CV (PDF), updated `TODO: Month 2026`".

### 5.2 Research page, sections with anchors

1. `#jmp` Job Market Paper: full details and abstract from 4.4.
2. `#publications` Publications (4.5).
3. `#wip` Work in Progress (4.6). No PDF links.
4. `#presentations` Selected presentations (4.8).

Empty sections are hidden automatically.

### 5.3 Teaching page

Table or list from 4.7.

### 5.4 Footer

"© Yanik Nimtz · yanik.nimtz [at] urv.cat · Last updated: {build date}" plus ORCID and LinkedIn icons.

---

## 6. Repository layout and data model

```
.
├── PLAN.md                       # this file
├── CLAUDE.md                     # short notes for future sessions (how to add a paper, update CV)
├── README.md                     # run locally, deploy, update content
├── hugo.toml                     # baseURL = "https://yaniknimtz.com/", title, menu
├── content/
│   ├── _index.md                 # bio (4.2)
│   ├── research.md               # front matter only; body rendered from data
│   └── teaching.md
├── data/
│   ├── profile.yaml              # name, title, affiliation, address, email, phone, links, on_market, cv_updated
│   ├── research.yaml             # jmp, publications, work_in_progress, presentations
│   ├── teaching.yaml
│   └── references.yaml           # letter writers with show: true/false
├── layouts/                      # custom theme
│   ├── _default/baseof.html
│   ├── index.html
│   ├── research/single.html (or conditional in _default/single.html)
│   ├── 404.html
│   └── partials/ head.html nav.html footer.html paper.html links.html jsonld.html
├── assets/
│   ├── css/main.css
│   └── img/headshot.jpeg
├── static/
│   ├── files/                    # CV + 2 PDFs (section 2)
│   ├── CNAME                     # yaniknimtz.com
│   └── favicon files (simple "YN" monogram)
└── .github/workflows/deploy.yml
```

### `data/research.yaml` (prefilled)

```yaml
jmp:
  title: "Impact of the Market Stability Reserve on firm profitability"
  authors: ["Yanik Nimtz", "Mercedes Teruel"]
  status: "Submitted"
  updated: "November 2026"
  pdf: "/files/Nimtz_Teruel_JMP_MSR_Firm_Profitability.pdf"
  jel: "H23, Q54, Q58"
  key_findings: [...]   # the four bullets in 4.4
  abstract: "..."       # the abstract in 4.4
  figure: "img/jmp_roa_event_study.png"
  figure_caption: "..." # 4.4
  figure_alt: "..."     # 4.4

publications:
  - authors: "Nimtz, Y., & Teruel, M."
    year: 2026
    title: "Corporate Decarbonization: Understanding CO2 Emission Drivers Across High- and Low-Polluting Firms in OECD Countries"
    journal: "Business Strategy and the Environment"
    volume: ""          # TODO when assigned
    pages: ""
    doi: "10.1002/bse.70849"
    pdf: "/files/Nimtz_Teruel_2026_Corporate_Decarbonization_BSE.pdf"
    open_access: true
    abstract: "..."     # 4.5

work_in_progress:
  - title: "Does carbon leakage appear under high CO2 prices? Impact of high carbon prices on emission behaviour of multinationals under the EU ETS"
    coauthors: ["Mercedes Teruel", "Pelin Demirel"]
    description: "..."  # 4.6
  - title: "The role of certification of innovation on firm growth: an empirical analysis of Spanish SMEs"
    coauthors: ["Mercedes Teruel"]
    description: "..."  # 4.6

presentations: [...]    # 4.8, newest first, {year, event, place, paper}
```

Co-author names may optionally link to their staff pages. Leave the URL fields empty unless Yanik provides them.

---

## 7. Design requirements

- **Look:** clean and text-first, with generous white space and one muted accent colour (e.g. a deep green or petrol blue that fits the climate topic). Use a readable system font stack or one self-hosted font. No animations, carousels or stock-template look.
- **Typography:** body 17–18 px, line length 60–80 characters, line height ~1.6.
- **Contrast:** WCAG AA (4.5:1 body text).
- **Dark mode:** optional, via `prefers-color-scheme`.
- **No JavaScript needed** for content. Collapsible abstracts use native `<details>`.
- **Performance:** Home under ~500 KB. Serve the headshot as responsive WebP/JPEG through Hugo image processing. Lighthouse Performance ≥ 95.
- **Print stylesheet** so the Research page prints cleanly.

---

## 8. Build tasks for Claude Code (step by step)

Commit after each phase.

### Phase 0: Setup
1. Work in the current repository, which Yanik has already created on GitHub. It contains `PLAN.md` and `inputs/`.
2. Install Hugo extended, `hugo new site . --force --format toml` (the repo is not empty), add `.gitignore` (`public/`, `resources/_gen/`, `.hugo_build.lock`, `.DS_Store`).
3. Move the input files to their places per section 2, then delete the `inputs/` folder so files aren't duplicated.

### Phase 1: Theme skeleton
4. `baseof.html`, `head.html`, `nav.html`, `footer.html`, `main.css`. Use a responsive nav (a wrapped horizontal list on mobile, no JS hamburger).

### Phase 2: Data
5. Create the four data files with the content from section 4. Keep `TODO` only where section 4 says `TODO`.

### Phase 3: Pages
6. Home (5.1), Research (5.2), Teaching (5.3), 404 page. Use a reusable `paper.html` partial.

### Phase 4: SEO, metadata, accessibility
7. Everything in section 10.

### Phase 5: Deployment
8. `.github/workflows/deploy.yml` with the official Pages actions (`actions/configure-pages`, `actions/upload-pages-artifact`, `actions/deploy-pages`) and a pinned Hugo version.
9. Tell Yanik to set **Settings → Pages → Source: GitHub Actions** and to complete the domain steps in section 9.
10. Verify the live site.

### Phase 6: Quality checks
11. `hugo --minify` with no warnings.
12. Link check (e.g. `lychee` or `htmltest`).
13. Lighthouse on Home and Research, mobile and desktop: all categories ≥ 95.
14. Check at 360, 768 and 1280 px: no horizontal scroll.
15. `grep -rn TODO` and give Yanik the remaining list.

### Phase 7: Docs
16. `README.md` and `CLAUDE.md`: how to run locally (`hugo server`), add a paper, replace the CV, toggle `on_market`, switch a reference on, and deploy.

---

## 9. Deployment and domain `yaniknimtz.com`

Yanik chose `yaniknimtz` as the domain name. Recommended: **yaniknimtz.com** (about €10–15 per year).

Steps for Yanik (Claude Code must not handle registrar logins or payment, only give the exact records):

1. Check availability and buy `yaniknimtz.com` at any registrar (e.g. Cloudflare Registrar, Porkbun, Namecheap). If the .com is taken, use `yaniknimtz.eu` or `.net`.
2. GitHub repo → Settings → Pages → Custom domain: `yaniknimtz.com`. Keep `static/CNAME` containing `yaniknimtz.com` so deploys don't remove it.
3. DNS at the registrar:
   - Apex `yaniknimtz.com`: four `A` records `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153` (and the matching `AAAA` records if desired). Check these against GitHub's current Pages docs before setting them.
   - `www`: `CNAME` → `<github-username>.github.io` (Yanik's GitHub username).
4. Verify the domain in GitHub account settings → Pages (prevents domain takeover).
5. After DNS propagates (minutes to hours), tick **Enforce HTTPS**.

Until the domain is live, the site is reachable at `https://<github-username>.github.io/website/`. Set `baseURL` accordingly during that period.

---

## 10. SEO, accessibility, mobile

### 10.1 SEO and metadata
- Unique `<title>` and meta description per page (4.1).
- Open Graph and Twitter card tags with the headshot as the image.
- **JSON-LD `Person`** on Home: name, jobTitle "PhD Candidate in Economics", affiliation Universitat Rovira i Virgili, alumniOf (URV, PFH Göttingen), url, image, email, `sameAs` [ORCID, LinkedIn].
- `sitemap.xml` and `robots.txt` allowing indexing.
- Set the PDF title metadata of the JMP and CV PDFs (e.g. with `exiftool` or `qpdf`) so search results show proper titles.

### 10.2 Accessibility (WCAG 2.1 AA)
- Semantic HTML, one `<h1>` per page, `lang="en"`, `<nav>`, `<main>`, `<footer>`.
- Alt text on the photo. `aria-label` on icon-only links ("ORCID profile", "LinkedIn profile").
- Skip-to-content link, visible focus styles, links not distinguished by colour alone.
- PDF links say "(PDF)".

### 10.3 Email
Show it as `yanik.nimtz [at] urv.cat`, plus a `mailto:` link assembled by a tiny inline script that falls back to the plain text.

### 10.4 Mobile
Mobile-first CSS, viewport meta, tap targets ≥ 44 px, `img { max-width: 100%; }`.

---

## 11. Privacy, permissions, and recommended extra steps

- Before going live, ask Mercedes Teruel whether she agrees to be listed with her email. (Pelin Demirel stays hidden until Yanik confirms.)
- No analytics by default. If wanted, use GoatCounter (privacy-friendly, no cookie banner). Avoid Google Analytics because of GDPR consent requirements.
- Never commit credentials.
- **Recommended before the market (Yanik, outside the build):** create a **Google Scholar** profile, register on **RePEc/IDEAS**, and optionally post the JMP on **SSRN**. Then add the links to `profile.yaml`.
- After launch: submit `https://yaniknimtz.com/sitemap.xml` in Google Search Console. Add the URL to ORCID, LinkedIn, the CV, the email signature and the URV staff/PhD page if there is one.

---

## 12. Final checklist

Content
- [ ] Name, title line, URV department and expected PhD date (late summer 2027) correct
- [ ] Headshot displays sharply and loads fast
- [ ] Bio and research interests as in section 4
- [ ] Job market banner shown
- [ ] JMP on Home (key findings + PDF) and Research (abstract + figure + PDF + "November 2026")
- [ ] Web version of the CV has no date of birth or WhatsApp number
- [ ] BSE 2026 publication with DOI and open-access PDF
- [ ] Two work-in-progress papers, without PDFs
- [ ] Teaching and presentations complete
- [ ] CV PDF linked from the nav and Home, "updated" date set
- [ ] Mercedes Teruel (Full Professor) listed with consent; Pelin Demirel hidden
- [ ] Email, phone, Campus Bellissens address, ORCID and LinkedIn correct
- [ ] No date of birth or WhatsApp number anywhere
- [ ] No `TODO` left

Technical
- [ ] Live on GitHub Pages, `yaniknimtz.com` configured, HTTPS enforced
- [ ] Link check passes
- [ ] Lighthouse ≥ 95 in all categories (mobile + desktop)
- [ ] Looks right at 360, 768 and 1280 px
- [ ] Meta tags, Open Graph, JSON-LD, sitemap, robots.txt, favicon, 404 page in place
- [ ] README.md and CLAUDE.md written

Launch
- [ ] Search Console sitemap submitted
- [ ] URL added to ORCID, LinkedIn, CV, email signature
- [ ] Checked by Yanik (and ideally his supervisor) on a phone and a laptop

---

## 13. Remaining open items for Yanik

1. Export a web version of the CV without date of birth and WhatsApp number, and give its "updated" month.
2. Mercedes Teruel's consent to be listed. Pelin Demirel later.
3. Confirm the software wording (4.9).
4. Buy `yaniknimtz.com` (section 9).
5. Optional: office number, course levels for teaching.

---

## Prompt to start Claude Code

*"Read PLAN.md and build the site phase by phase. Use the content in section 4 exactly as written and the files in inputs/ as listed in section 2. Ask me about anything marked [ASK YANIK] before Phase 5. Work on a branch and open a pull request when the site builds."*
