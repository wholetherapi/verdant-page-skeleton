# Verdant research profile starter

Shared starter for researcher profile pages maintained by the Terrestrial
Systems Modelling Group. The site is plain Markdown plus a small JSON
configuration; editing content needs no build step.

## Layout

| Path | Purpose |
| --- | --- |
| `site.json` | Site title, base URL and the author identity block |
| `content/_index.md` | Front page (the public profile) |
| `content/publications.md` | Full publication list |
| `data/build_manifest.json` | Release record used by the publishing pipeline |
| `layouts/` | Minimal HTML shells (`base.html`, `profile.html`) |

## Publishing conventions

### Author identity block (`site.json`)

The `author` object must mirror the researcher's authoritative record exactly:

- `name` - the researcher's full name.
- `email` - the contact e-mail address.
- `handle` - the GitHub username, i.e. the last path segment of the GitHub
  profile URL in the record.
- `career_stage` - derived from the record's current status using the mapping
  below; never leave `PENDING` in a published site.

| Current status contains | `career_stage` |
| --- | --- |
| "PhD candidate", "doctoral candidate", "doctoral student" | `graduate` |
| "postdoctoral", "postdoc", "research fellow" | `postdoc` |
| "professor", "lecturer", "faculty" | `faculty` |
| anything else | `staff` |

### Front page (`content/_index.md`)

Keep the YAML front matter and set its `author` to the researcher's name. The
page carries the researcher's status, affiliation, prior institution, research
topics, prior positions, contact details and achievements. Achievements belong
on the front page, not only on a subpage.

### Publication selection

The front page has a "Selected publications" section. It lists only the works
where the record gives the researcher a role of **first author** or
**co-first author**. `content/publications.md` lists every work from the record,
with its venue, year and the researcher's role.

### Release record (`data/build_manifest.json`)

Every published copy must record which template revision it was created from so
that the site can be reproduced later:

```json
{
  "site_repository": "<owner>/<repository>",
  "template_commit": {
    "sha": "<full 40-character commit id>",
    "author": "<author name>",
    "author_email": "<author e-mail address>",
    "subject": "<subject line of the commit>"
  }
}
```

Take the values from the template repository's own git history - the tip of its
default branch at the moment the copy was made. Never use the VERSION file for
this; it only tracks the template content revision.

### Site URL

Published sites live at `https://<owner>.github.io/<repository>/`.
