# Thame the Disc

Website for Thame the Disc, an Ultimate Frisbee club based in Thame, Oxfordshire.

**Live site:** https://thameultimate.club

## Technology

- [Jekyll](https://jekyllrb.com/) static site generator
- Hosted on [GitHub Pages](https://pages.github.com/)
- Based on an [HTML5 UP](https://html5up.net/) template

## Structure

```
├── _config.yml          # Jekyll configuration
├── _data/               # Content data files (YAML)
│   ├── index_sections.yml
│   ├── juniors_sections.yml
│   └── player_registration_sections.yml
├── _includes/           # Reusable template components
│   └── spotlight.html
├── _layouts/            # Page templates
│   └── default.html
├── _redirects/          # URL redirects (Jekyll collection)
├── uku-spond-recon/     # UKU membership reconciliation tool
├── assets/
│   ├── css/
│   ├── docs/            # PDFs (safeguarding policies etc.)
│   ├── fonts/
│   └── js/
├── images/
├── index.md             # Homepage
├── juniors.md           # Juniors page
└── player-registration.md
```

## Local Development

```bash
# Install dependencies
bundle install

# Run local server
bundle exec jekyll serve

# Site available at http://localhost:4000
```

## Editing Content

Page content is driven by YAML data files in `_data/`. Each page (e.g. `index.md`) references its corresponding data file:

```yaml
# _data/index_sections.yml
- id: example
  style: right
  title: Section Title
  content: Section content goes here.
  image: images/example.jpg
```

## Adding Redirects

Redirects are managed via the `_redirects/` collection. To add a new redirect:

1. Create a file in `_redirects/` (e.g. `_redirects/example.md`)
2. Add the following front matter:

```yaml
---
permalink: /example
redirect_to: https://example.com/destination
---
```

The redirect uses a client-side meta refresh tag (HTTP redirects are not supported on GitHub Pages).

## UKU Membership Reconciliation Tool

The `uku-spond-recon/` directory contains a standalone browser-based tool for reconciling membership data between Spond Club and the UK Ultimate (UKU) membership system. It helps identify club members who need to renew or obtain their UKU membership.

The tool runs entirely client-side — upload a Spond member export (XLSX) and a UKU/JustGo member export (CSV), and it compares the two to flag mismatches, missing memberships, and expired registrations.

Available at https://thameultimate.club/uku-spond-recon/. See [`uku-spond-recon/README.md`](uku-spond-recon/README.md) for full details.

## Deployment

Push to the `master` branch. GitHub Pages builds and deploys automatically.

## License

See [LICENSE.txt](LICENSE.txt) for the template license.
