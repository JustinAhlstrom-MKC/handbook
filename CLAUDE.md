# MKC Restaurants Employee Handbook - Project Context

## Project Overview

Modular employee handbook system for MKC Restaurants (Margie's Kitchen & Cocktails and Grackle). Policies are stored as individual markdown files with YAML front matter, enabling version control at the policy level and automated assembly into Word documents.

## Repository Structure

```
handbook/
├── policies/           # Individual policy markdown files
│   ├── 01-welcome/
│   ├── 02-employment/
│   ├── 03-conduct/
│   ├── 04-compensation/
│   ├── 05-scheduling/
│   ├── 06-appearance/
│   ├── 07-technology/
│   ├── 08-safety/
│   ├── 09-administrative/
│   └── 10-acknowledgement/
├── build/              # Build script and requirements
├── output/             # Generated documents (gitignored)
├── templates/          # Word templates (future)
├── config.yaml         # Section ordering and build settings
├── REVIEW-STATUS.md    # Review tracking (may be stale)
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
- Example: Employee Classifications defines what "full-time" means; PTO and Benefits policies reference it for eligibility

### Employee Classifications (02-employment/employee-classifications.md)
- **Part-Time:** <30 hours/week average
- **Full-Time:** 30+ hours/week average
- **Exempt:** Salaried management
- **Initial qualification:** 90 days from hire
- **Ongoing review:** Quarterly (Apr 1, Jul 1, Oct 1, Jan 1) based on prior quarter hours

### Benefits Eligibility
- Health & Dental: Full-time and Exempt only
- EAP (Sand Creek): All employees
- **Probationary quarter:** If FT drops to PT, benefits continue for 1 quarter grace period. Benefits end after 2 consecutive PT quarters.

### PTO Structure
- Part-Time: Sick & Safe Time only (48 hrs/year, MN law)
- Full-Time Hourly: SST + 40 hrs PTO/year
- Exempt Management: SST + 80 hrs PTO/year (consistent across both locations)

## Current State

- **Total policies:** 44
- **All policies status:** draft
- First pass review completed on some compensation policies
- Google Drive sync attempted but .gdoc format doesn't round-trip well

## Policies Needing Content (Placeholders)

| Policy | What's Needed |
|--------|---------------|
| tips.md | Tip sharing guidance (not tip pool) |
| social-media.md | Full social media guidelines |
| cell-phones.md | Phone usage and storage rules |
| emergency-procedures.md | Fire, weather, medical, robbery procedures |
| food-safety.md | Food safety basics or reference to training |

## Section Ordering (in config.yaml)

Ordering within sections should follow: **Most important/foundational → Supporting details → Standalone/less critical**

**Section 4 suggested order:**
pay-and-timekeeping → work-hours-overtime → tips → pto-policy → mn-esst → mn-paid-leave → benefits → meal-rest-breaks → wage-discussions

**Section 8 suggested order:**
food-safety → injury-reporting → emergency-procedures → building-access → parking

## Collaboration Workflow

### For Justin (technical)
- Edit policies directly in VS Code or GitHub
- Run `python build/build.py` to generate Word doc
- Commit and push changes

### For Becky/others (non-technical)
- Option 1: GitHub web interface (click file → pencil icon → edit → commit)
- Option 2: Google Drive markdown files (sync manually)
- Need to create a simple guide for GitHub web editing

### Google Drive Location
```
G:\Shared drives\03 - Human Resources (Confidential)\Employee Handbook\
```
Mount in WSL: `sudo mount -t drvfs G: /mnt/g`

Note: Editing .md files in Google Drive creates .gdoc copies. For clean workflow, either edit markdown directly or accept manual sync-back.

## Build Commands

```bash
# Install dependencies
pip install -r build/requirements.txt

# Build full handbook
python build/build.py

# Exclude draft policies
python build/build.py --exclude-draft

# Custom output name
python build/build.py --output-name "MKC-Handbook-Final"
```

## Next Steps

1. Apply section reordering to config.yaml (Sections 4 and 8)
2. Complete placeholder policies (tips, social-media, cell-phones, emergency, food-safety)
3. Continue policy-by-policy review
4. Create GitHub editing guide for Becky
5. Once all approved, batch update status to "active"
6. Build final Word document for distribution

## GitHub Repository

https://github.com/JustinAhlstrom-MKC/handbook
