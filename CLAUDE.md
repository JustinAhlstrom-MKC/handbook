# MKC Restaurants Employee Handbook - Project Context

## Project Overview

Modular employee handbook system for MKC Restaurants (Margie's Kitchen & Cocktails and Grackle). Policies are stored as individual markdown files with YAML front matter, enabling version control at the policy level.

**Primary publication channel:** GitHub Pages site built with MkDocs Material. PDF export is available for occasional use but the website is the canonical version employees access.

## Repository Structure

```
handbook/
├── policies/           # Individual policy markdown files (also MkDocs docs_dir)
│   ├── 01-welcome/
│   ├── 02-employment/
│   ├── 03-conduct/
│   ├── 04-compensation/
│   ├── 05-scheduling/
│   ├── 06-appearance/
│   ├── 07-technology/
│   ├── 08-safety/
│   ├── 09-administrative/
│   ├── 10-acknowledgement/
│   ├── assets/         # Images and CSS for GitHub Pages site
│   └── index.md        # Site homepage
├── overrides/          # MkDocs Material theme overrides
├── mkdocs.yml          # MkDocs config — nav, theme, extensions
├── config.yaml         # Section ordering for Word/PDF build
├── build/              # Word/PDF build script and requirements
├── output/             # Generated documents (gitignored)
├── REVIEW-STATUS.md    # Review tracking
├── COMPLIANCE-REVIEW.md # Compliance review item tracking
└── CLAUDE.md           # This file
```

## Front Matter Schema

Each policy file uses this YAML front matter:

```yaml
---
title: Policy Title
version: 1.0.0
effective_date: 2025-01-01
status: draft | in-review | approved | active
applies_to: all | [full-time, exempt] | [servers, bartenders, etc.]
---
```

## Key Design Decisions

### Information Architecture
- **Single source of truth**: Each piece of information lives in ONE policy only
- **Cross-references**: Policies reference each other rather than duplicating content
- Example: Employee Classifications defines what "full-time" means; the Benefits policy references it for eligibility (hourly PTO is decoupled from classification)

### Employee Classifications (02-employment/employee-classifications.md)
- **Part-Time:** <30 hours/week average
- **Full-Time:** 30+ hours/week average
- **Exempt:** Salaried management
- **Initial qualification:** First 30 days from hire (initial full-time evaluation); classification then follows the quarterly review schedule
- **Ongoing review:** Quarterly (Apr 1, Jul 1, Oct 1, Jan 1) based on prior quarter hours

### Benefits Eligibility
- Health & Dental: Full-time and Exempt only
- EAP (AllOne Health): All employees
- **Probationary quarter:** If FT drops to PT, benefits continue for 1 quarter grace period. Benefits end after 2 consecutive PT quarters.

### PTO Structure (v2.0, effective 2026-09-03)
- All employees: Sick & Safe Time (48 hrs/year, MN law). SST covers illness and other qualifying/unplanned absences.
- **Hourly (any classification):** 24 hrs PTO granted twice a year, on the last payday in June and the last payday in December, if the employee worked **more than 700 clocked hours** in the 13 pay periods ending with the pay period paid on the grant date. No proration, no partial history. Eligibility is decoupled from FT/PT classification.
- **Use-it-or-lose-it:** Hourly grant must be scheduled and used before the next grant date; unused hours forfeit on the next grant date and do not stack. Paid in 4-hour blocks. Must be requested before the payroll that includes the time off.
- **Exempt Management:** Unchanged accrual — 3.08 hrs/pay period, 80 hrs/year cap, 40 hr carryover cap, usable after 90 days.
- **PTO is vacation leave only** (both hourly and exempt) — cannot be used for unplanned absences. This keeps the PTO bank outside MN ESST rules.
- **No payout at separation** for PTO or SST — both are benefits of continued employment, not earned wages. MN has no vacation-payout statute; written policy controls (Lee v. Fresenius).
- **2026 transition:** First hourly grant made retroactively based on the 13 pay periods ending with the last June 2026 payday; usable through the last December 2026 payday.

## Current State

- **Total policies:** 47
- **All policies status:** active
- Full compliance review completed across all sections (see REVIEW-STATUS.md and COMPLIANCE-REVIEW.md for details)
- All former placeholder policies (tips, social-media, cell-phones, emergency-procedures) have full content
- New policies added during review: fmla.md, employee-perks.md, scheduling.md, fire-safety.md, cut-resistant-gloves.md
- Policies consolidated during review: mn-esst folded into pto-policy.md, on-stage folded into appearance-standards.md
- Section ordering applied to config.yaml
- Meal breaks: paid when taken on-premises (no clock-out); employee must clock out only if leaving the premises during a meal break

## When Adding, Removing, or Renaming a Policy

**Both of these files must be updated to stay in sync:**

1. **`mkdocs.yml`** — the `nav:` section controls the GitHub Pages sidebar. This is the primary publication channel.
2. **`config.yaml`** — the `sections:` list controls the Word/PDF build order.

Policy order should match between the two files.

## Publishing (GitHub Pages)

The site is built automatically by GitHub Pages when changes are pushed to `main`. MkDocs Material is the theme.

- **Site config:** `mkdocs.yml`
- **Content source:** `policies/` directory (set as `docs_dir`)
- **Theme overrides:** `overrides/main.html`
- **Assets:** `policies/assets/` (logo, CSS)

To preview locally: `mkdocs serve`

## Word/PDF Export

Occasionally used for printed copies or attorney review. Not the primary distribution method.

```bash
pip install -r build/requirements.txt
python build/build.py
python build/build.py --exclude-draft
python build/build.py --output-name "MKC-Handbook-Final"
```

## Acknowledgement Form

The signed acknowledgement is collected via an Airtable form (base `appVWDqRGdBqhvfEj`, form `pagzgCR2WphrlaxGr`) embedded on `policies/10-acknowledgement/acknowledgement.md`. The form's legal text lives in Airtable; a versioned backup of the full form content is kept at `acknowledgement-form-backup.md` (repo root, not published). **If the acknowledgement language changes in Airtable, update that backup file in the same change.**

## Collaboration Workflow

### For Justin (technical)
- Edit policies directly in VS Code
- Commit and push — GitHub Pages updates automatically

### For Becky/others (non-technical)
- Option 1: GitHub web interface (click file → pencil icon → edit → commit)
- Option 2: Google Drive markdown files (sync manually)

### Google Drive Location
```
G:\Shared drives\03 - Human Resources (Confidential)\Employee Handbook\
```
Mount in WSL: `sudo mount -t drvfs G: /mnt/g`

## Next Steps

1. ~~Apply section reordering to config.yaml (Sections 4 and 8)~~ ✓ Done
2. ~~Complete placeholder policies (tips, social-media, cell-phones, emergency, food-safety)~~ ✓ Done
3. ~~Full compliance review across all policies~~ ✓ Done
4. ~~Batch update all policy statuses to "active"~~ ✓ Done
5. Create GitHub editing guide for Becky
6. Have employment attorney review handbook (see COMPLIANCE-REVIEW.md for checklist)
7. Export PDF version for attorney review

## GitHub Repository

https://github.com/JustinAhlstrom-MKC/handbook
