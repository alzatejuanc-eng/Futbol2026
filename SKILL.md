---
name: mundial2026-predictor-design
description: Use this skill to generate well-branded interfaces and assets for the Predictor Mundial 2026 web app (Transformación ExO), either for production or throwaway prototypes/mocks. Contains essential design guidelines — colors, type, fonts, assets, and a UI kit of React components — for prototyping in this brand.
user-invocable: true
---

Read the README.md file within this skill, and explore the other available files.

If creating visual artifacts (slides, mocks, throwaway prototypes, etc.), copy
assets out and create static HTML files for the user to view. The canonical
tokens live in `colors_and_type.css`; the canonical components live in
`ui_kits/predictor/`. The original product is preserved verbatim under
`source/index.html`.

If working on production code, you can copy assets and read the rules here to
become an expert in designing with this brand.

If the user invokes this skill without any other guidance, ask them what they
want to build or design, ask some questions, and act as an expert designer who
outputs HTML artifacts _or_ production code, depending on the need.

Key invariants to preserve when designing with this brand:
- **Voice** is Spanish (Latin America), informal `tú` form.
- **Emoji is the icon system** — heavy and categorically-mapped (see README).
- **Navy primary + teal accent** dominates; cyan / coral / purple are reserved.
- **Hover lift** (cards `-4px`, buttons `-2px`) is the signature interaction.
- The product is **flat with light gradient accents** — no photos, no patterns,
  no inner shadows, no backdrop-filter.
