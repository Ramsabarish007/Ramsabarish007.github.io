# Ramsabarish V — Portfolio

Personal portfolio site. Single static page, no build step, no dependencies.
Published with GitHub Pages.

**Live:** https://ramsabarish007.github.io

## What's here

```
index.html                        the entire site (HTML + CSS + JS inline)
assets/Ramsabarish-V-Resume.pdf   résumé — linked from the Résumé section
assets/Ramsabarish-V-Resume.docx  editable source of the résumé
.nojekyll                         tells GitHub Pages to serve files as-is
```

## Editing

Everything lives in `index.html`, in this order:

| Looking for | Search for |
|---|---|
| Colours, fonts, spacing | `TOKENS` at the top of the `<style>` block |
| Career timeline chart | `CAREER CHART` |
| Payment lifecycle diagram | `LEAK MAP` |
| Headline numbers | `class="metrics"` |
| Case studies + filters | `<section id="work">` |
| Skill tags | `<section id="skills">` |
| Résumé downloads | `<section id="resume">` |
| Repository cards | `<section id="code">` |
| Email / LinkedIn | `<section id="contact">` and the `<footer>` |

Save, then refresh. To preview exactly as deployed:

```bash
python -m http.server 8000
```

Then open http://localhost:8000.

## Common changes

### Swapping the résumé

Replace `assets/Ramsabarish-V-Resume.pdf` (and the `.docx`), keeping the
filenames. No HTML edit needed.

### Adding a second résumé variant

In `<section id="resume">`, copy an `<article class="doc">` block, drop the new
file into `assets/`, and point the links at it. To remove a variant, delete its
block. The second card currently points at the case studies rather than a file —
replace it if you'd rather offer a role-specific résumé.

### Adding a case study

Copy an `<article class="case">` block inside `<div class="cases">`. Set:

- `id="case-yourid"` — must be unique
- `data-org="athena|flip|iqvia|icon"` — drives the filter buttons
- the `case-org` badge class: `o-athena`, `o-flip`, `o-iqvia`, `o-icon`

Then update the count in the matching `.filter` button, and bump the `All`
count. If you want it reachable from the lifecycle diagram, add a
`<button class="leak" data-case="yourid">` to the relevant stage — the script
matches `data-case="yourid"` to `id="case-yourid"`.

### Adding a job to the career chart

Add a `<button class="seg">` to `<div class="track">` with `data-job="key"` and
`style="flex:N"`, where **N is the number of months in the role** — that's what
makes the blocks proportional. Add a matching entry to the `JOBS` object in the
script. Adjust the year labels in `<div class="axis">` if the span changes.

### Adding a repository card

Copy an `<a class="repo">` block in the Code section. The
`style="--accent:var(--cyan)"` attribute sets the hover bar colour; options are
`--jade`, `--amber`, `--coral`, `--cyan`, `--slate`.

## Conventions worth keeping

- **No absolute commercial figures.** Results are expressed as rates, ratios and
  latencies. Percentages describe the work without disclosing an employer's
  revenue, patient counts or cost base.
- **Only claim what you can defend.** The skills section is deliberately limited
  to things that would survive an interview question.
- Content is visible without JavaScript; scroll animations are progressive
  enhancement only.
- Light and dark themes follow the OS; the toggle overrides via `localStorage`.
- Respects `prefers-reduced-motion`.

## Deploying updates

```bash
git add . && git commit -m "Update" && git push
```

Live in under a minute.
