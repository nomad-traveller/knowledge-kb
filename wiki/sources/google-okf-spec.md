---
type: Source Summary
title: Google OKF SPEC.md
description: Canonical specification of the Open Knowledge Format v0.2.
resource: https://github.com/GoogleCloudPlatform/knowledge-catalog/blob/main/okf/SPEC.md
tags: [okf, format, specification, seed-source]
status: stable
generated: { by: human:user, at: 2026-08-26T00:00:00Z }
sources:
  - id: original
    resource: https://github.com/GoogleCloudPlatform/knowledge-catalog/blob/main/okf/SPEC.md
    title: Open Knowledge Format (OKF) SPEC.md
    author: team:google-cloud
    last_modified: 2026-01-01T00:00:00Z
---

# Google OKF SPEC.md

Canonical spec of **Open Knowledge Format v0.2** from GoogleCloudPlatform's
`knowledge-catalog` repo. Full text retained in `raw/google-okf-spec.md`.

## Key takeaways

- A bundle = directory tree of markdown files; no central authority, no required
  tooling. If you can `cat` it, you can read it; if you can `git clone`, you can
  ship it.
- `type` is the only required frontmatter key; unknown keys are preserved, not
  rejected (§4.1, §11).
- Provenance/trust/lifecycle are first-class (§5): `sources`, `generated`,
  `verified`, `status`, `stale_after`.
- `index.md` (§8) and `log.md` (§9) are reserved filenames for progressive
  disclosure and change history.

See [Open Knowledge Format (OKF)](/concepts/open-knowledge-format.md) for the
synthesized concept.
