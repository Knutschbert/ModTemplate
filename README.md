# __NAME__

__DESCRIPTION__

Documentation site: [__SITE_URL__](__SITE_URL__)

---

## About this repository

This repository was created from the [ModTemplate](https://github.com/Knutschbert/ModTemplate) for **Chivalry 2** mods built with **ArgonSDK**. It combines a place for your mod's notes and documentation (published as a website via MkDocs / GitHub Pages) with the release tooling needed to submit your mod to the [C2ModRegistry](https://github.com/Chiv2-Community/C2ModRegistry).

New to modding Chivalry 2? Start with the **[ArgonSDK Field Guide](https://knutschbert.github.io/ArgonSDK-FieldGuide/)**, a community-maintained reference with:

- [Requirements](https://knutschbert.github.io/ArgonSDK-FieldGuide/Tutorials/Requirements.html) and step-by-step tutorials (swapping a texture, FFA and TDM maps, your first Blueprint mod)
- Overviews of game systems: spawns, weapons, game modes and objectives
- Unchained mod loading: file lists, mod loader flags and command line arguments
- Case studies of existing mods
- The [ModTemplate page](https://knutschbert.github.io/ArgonSDK-FieldGuide/Mods/ModTemplate.html) describing this template

## Getting started

1. **Clone** this repository and build your mod following the [Field Guide](https://knutschbert.github.io/ArgonSDK-FieldGuide/).
2. **Write your docs** in the [`docs/`](docs) folder (see below). The site is rebuilt and published by the `ci` workflow on every push to `main`.
3. **Enable GitHub Pages** once. After the first `ci` run has finished successfully (check the [Actions tab](__REPO_URL__/actions)), the `gh-pages` branch exists. Open the **[Pages settings](__REPO_URL__/settings/pages)**, choose **Deploy from a branch**, then select the branch `gh-pages` with folder `/ (root)` and save. Your site will be available at [__SITE_URL__](__SITE_URL__) a minute later.
    - The `ci` workflow also tries to enable Pages itself on the first run. That only works if you add a `PAGES_PAT` secret with a token that has Pages write access.
    - If the branch list is empty, the first `ci` run has not succeeded yet. Check the Actions tab, or run the `ci` workflow by hand.
    - Tip: when creating your repository from the template, copy only the `main` branch. The `gh-pages` branch is created for you.
4. **Publish a release** (see [Releasing](#releasing)).

## Editing the docs with Obsidian

The [`docs/`](docs) folder is a plain Markdown folder, so you can open this repository (or just `docs/`) as a vault in [Obsidian](https://obsidian.md/) and edit your notes there. The Field Guide itself is written this way.

- Folders in `docs/` become sections in the site navigation, and notes become pages. The page title is the note's first-level heading.
- Obsidian-style `[[wikilinks]]` work in the published site.
- Math (LaTeX), Mermaid diagrams, task lists and footnotes are supported.
- `docs/index.md` is the homepage. It starts as a placeholder mod description, and the `Init from template` workflow fills in your mod's name, description and repository link.
- Avoid spaces in new folder and file names, since they end up in the page URLs.
- To arrange pages manually, use the `nav` option in [`mkdocs.yml`](mkdocs.yml). See the [MkDocs docs](https://www.mkdocs.org/user-guide/configuration/#nav) and the [Material theme setup](https://squidfunk.github.io/mkdocs-material/setup/setting-up-navigation/).

Just commit and push your changes. GitHub Actions publishes them using [MkDocs](https://www.mkdocs.org/) with the [Material theme](https://squidfunk.github.io/mkdocs-material/).

## Releasing

Releases are submitted to the [C2ModRegistry](https://github.com/Chiv2-Community/C2ModRegistry) automatically:

1. Publish a **GitHub release** with a version tag (for example `v1.0.0`) from the `Releases` page of this repository. The release must contain exactly one `.pak` file. Pre-releases are not submitted.
2. The **Create Registry Issue** workflow ([`release_reg.yml`](.github/workflows/release_reg.yml)) starts on its own. It uses the registry's [`automated-publish`](https://github.com/Chiv2-Community/zero-infra-mod-registry/blob/v1/docs/plugin/release-requests.md) action, which checks the release and opens a registration issue in the registry, so the maintainers can review and merge the new version.
3. If the registration fails, fix the release and reply `retry` on the registry issue. You can also run the workflow by hand from the `Actions` tab, choosing the release tag in the "Use workflow from" dropdown.

This requires a repository secret named `C2MODREGISTRY_PAT`, a personal access token that is allowed to create issues in `Chiv2-Community/C2ModRegistry`. Add it under `Settings > Secrets and variables > Actions`. Without it the workflow skips the submission and shows a notice instead of failing.

## Credits

- Template: [Knutschbert/ModTemplate](https://github.com/Knutschbert/ModTemplate)
- Field Guide: [ArgonSDK-FieldGuide](https://knutschbert.github.io/ArgonSDK-FieldGuide/)
- Website scaffolding based on [jobindjohn/obsidian-publish-mkdocs](https://github.com/jobindjohn/obsidian-publish-mkdocs), built with [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/)
