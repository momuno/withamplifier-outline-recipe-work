# Session Transcript: withamplifier.com Content Generation System

**Session ID:** `5e8b6e41`  
**Date:** 2026-01-30  

---

## Objective

Create a **content generation and validation system** for the withamplifier.com website that:
1. Pulls content from authoritative source files in the Amplifier ecosystem
2. Generates web-ready content via a recipe
3. Validates accuracy (no fabrication, URLs work, content traces to sources)

---

## What We Did

### Phase 1: Website Analysis

Fetched and analyzed the current withamplifier.com site:
- Pulled HTML, CSS, JavaScript
- Identified all visible written content sections
- Mapped content to potential source files

### Phase 2: Source Identification

Identified where website content SHOULD come from:
- `amplifier/README.md` - Install command, description, quick start
- `amplifier/docs/MODULES.md` - Module types, providers, community content
- `amplifier/docs/USER_ONBOARDING.md` - Onboarding steps, features

### Phase 3: Link Validation

Checked all links on the current website. **Found critical issues:**

| Link | Status | Issue |
|------|--------|-------|
| GitHub | ✓ 200 | Works |
| Issues | ✓ 200 | Works |
| Discussions | ✗ 404 | Does not exist |
| Contributing | ✗ 404 | File doesn't exist at that path |
| 12 Community Bundles | ✗ ALL 404 | **Completely fictional** |

### Phase 4: Recipe Research

Examined existing recipes for inspiration:
- `amplifier/recipes/document-generation.yaml` - Multi-stage doc generation with validation
- `amplifier/outlines/development-hygiene_outline.json` - Source-to-section mapping pattern

### Phase 5: Implementation

Created two artifacts:

**1. Content Outline** (`outlines/withamplifier-content.json`)
- Maps 13 website sections to source files
- Defines generation prompts per section
- Specifies validation rules (URL checks, source traceability, no fabrication)
- Documents known issues

**2. Generation Recipe** (`recipes/website-content-generation.yaml`)
- 4-stage pipeline with approval gates
- Clones source repos, generates content, validates, outputs structured JSON
- Produces validation report highlighting any issues

---

## Files Created

```
working-dir-20260130-withamplifiersite/
├── outlines/
│   └── withamplifier-content.json    # 19.8 KB - Source mapping
└── recipes/
    └── website-content-generation.yaml  # 20.7 KB - Generation recipe
```

---

## Key Findings

### Current Website Problems

1. **Fictional Community Content** - Shows 12 bundles that don't exist (all return 404)
2. **Broken Footer Links** - Discussions and Contributing links are dead
3. **No Source Tracking** - Content can drift from actual ecosystem state

### Real Community Content (from MODULES.md)

| Category | Count | Examples |
|----------|-------|----------|
| Community Applications | 7 | app-voice, app-transcribe, amplifier-playground |
| Community Bundles | 2 | expert-cookbook, memory |
| Community Modules | 10+ | provider-bedrock, tool-youtube-dl |

---

## How to Run the Recipe

```bash
# In an Amplifier session:
"Run the website-content-generation recipe with outline_path=outlines/withamplifier-content.json"

# Or CLI:
amplifier tool invoke recipes \
  operation=execute \
  recipe_path=recipes/website-content-generation.yaml \
  context='{"outline_path": "outlines/withamplifier-content.json", "output_dir": "./generated"}'
```

---

## What's Not Done (Future Work)

1. **Change Detection Recipe** - Monitor source files for changes, trigger regeneration
   - User said "keep it in mind" but not needed now

2. **Actually Running the Recipe** - We built it but haven't executed it yet

3. **Website Integration** - The recipe outputs structured JSON; someone needs to integrate that into the actual website build process

---

## Design Decisions Made

1. **Generation First, Validation Second** - Not a validation-only tool; generates content then validates it
2. **Outline Pattern** - Borrowed from dev-hygiene outline structure (source + prompt per section)
3. **Flat Sections** - No BFS traversal needed since web content is flat, not hierarchical
4. **Separate Change Detection** - Kept as separate concern, not baked into main recipe

---

## Content Sections Mapped (13 total)

| Section | Content Type | Priority | Source |
|---------|--------------|----------|--------|
| `hero-install-command` | code | **critical** | README.md |
| `hero-tagline` | prose | low | README.md |
| `hero-description` | prose | medium | README.md + USER_ONBOARDING.md |
| `features-list` | list | medium | README.md + USER_ONBOARDING.md + MODULES.md |
| `module-types` | structured_list | high | MODULES.md |
| `community-bundles` | structured_list | **critical** | MODULES.md |
| `official-providers` | structured_list | high | MODULES.md |
| `getting-started-steps` | ordered_list | high | README.md + USER_ONBOARDING.md |
| `footer-github-link` | link | **critical** | README.md |
| `footer-docs-link` | link | high | README.md |
| `footer-discussions-link` | link | high | README.md |
| `footer-contributing-link` | link | high | README.md |
| `footer-issues-link` | link | **critical** | README.md |

---

## Questions That Might Come Up

**Q: Why not just fix the website manually?**  
A: This system ensures content stays accurate over time as the ecosystem evolves. Manual fixes drift.

**Q: Where does the generated content go?**  
A: Recipe outputs to `./generated/website-content.json` - structured JSON that can feed into the website build.

**Q: What triggers regeneration?**  
A: Currently manual. Change detection recipe (not yet built) would automate this.

---

## To Resume This Session

```bash
amplifier session resume 5e8b6e41
```

Or start fresh in the same directory - all artifacts are in place.
