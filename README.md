# artemtsikiridis.com

Source of [artemtsikiridis.com](https://artemtsikiridis.com), built with the [al-folio](https://github.com/alshedivat/al-folio) Jekyll theme (v1.2). In al-folio v1 the layouts, includes and styles come from Ruby gems (`al_folio_core` and the other `al_*` gems pinned in `Gemfile.lock`); this repository holds only the site's own content, configuration and a few deliberate overrides.

## Where things live

| What | File |
| --- | --- |
| Home page: bio, number of news items, selected papers on/off | `_pages/about.md` |
| News items | `_news/announcement_N.md` |
| Publications (home page and `/publications/`) | `_bibliography/papers.bib`; `selected = {true}` puts a paper on the home page, `abbr` is its tag (a new conference paper gets the next C number) |
| Sections of the publications page | `_pages/publications.md` |
| Bold venue acronym in publication lists, e.g. (**EC**) | `_includes/hook/bib.liquid`, a hook that al-folio's bib layout calls; it bolds the last parenthesised part of `booktitle` |
| Service page | `_pages/service.md` (each list shows in two columns; keep the `{: .service-cols}` line directly under it) |
| PDFs (papers, posters, theses, CV) | `assets/pdf/` |
| Profile photo | `assets/img/prof_pic.jpg` (the 480/800/1400px WebP versions are generated at build time) |
| Profile links (ORCID, Scholar, LinkedIn, DBLP) | `_data/socials.yml` |
| Name, URL, site-wide switches | `_config.yml` |
| Colours and small style additions (University of Warsaw palette, navy navigation bar, publication tags, gold award button, service columns) | `_sass/_themes.scss` (local override of the file shipped in `al_folio_core`; after editing it, run the `overrides accept` command below) |

## Workflow

1. Work on a branch: `git switch -c <name>`.
2. Preview locally with Docker: `docker compose up`, then open <http://localhost:8080>. Run `docker compose pull` first after an al-folio upgrade.
3. When happy: `git switch master && git pull && git merge --no-ff <name> && git push origin master`.
4. The push to `master` runs `.github/workflows/deploy.yml`, which builds the site and publishes it to the `gh-pages` branch. Pushing any other branch deploys nothing.

## Upgrading al-folio

Follow "Upgrading from a previous version" in al-folio's `docs/INSTALL.md`. Inside the running container:

```bash
docker compose exec jekyll bundle exec al-folio upgrade audit
docker compose exec jekyll bundle exec al-folio upgrade overrides audit
```

The second command reports when a newer `al_folio_core` has changed the file that `_sass/_themes.scss` overrides; `.al-folio-overrides.yml` records the version last reviewed. After reviewing, or after editing `_sass/_themes.scss` yourself, record the current version with:

```bash
docker compose exec jekyll bundle exec al-folio upgrade overrides accept _sass/_themes.scss
```
