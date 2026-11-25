# company-zoom-in

A Claude skill made at Elihome. Give it a company name and it produces a two-page PDF that shows what the company means for Elihome:

1. **One-pager** (A4 portrait): why we zoom in on this company, three key findings, two charts of checked numbers, its role in AI commerce, four actions for Elihome, a fact check and tiered sources.
2. **System map** (A4 landscape): the company in the centre, the groups it deals with around it, flows of money, goods and information, and where Elihome sits.

Every fact has a source and a tier: **A** official, **B** independent, **C** has something to sell, **D** cannot be verified. At least five key facts are opened and checked against their source before they are used.

## Install

### ⬇️ [Download the skill (company-zoom-in.zip)](https://kkindasara.github.io/company-zoom-in/company-zoom-in.zip)

**In the Claude app** (code execution must be on):
1. Click the download link above. Don't unzip it.
2. Open [Claude > Customize > Skills](https://claude.ai/customize/skills), click **+**, then **+ Create skill**, then **Upload a skill**, and upload the ZIP.
3. Start a new chat and type: *Zoom in on Wayfair for Elihome.*

**Colleagues on the same Claude Team or Enterprise plan:** you don't need the ZIP. Ask the owner of the skill to share it with you (or publish it to the organization), then turn it on under **Shared with you** in [Customize > Skills](https://claude.ai/customize/skills).

([Use Skills in Claude](https://support.claude.com/en/articles/12512180-use-skills-in-claude))

**In Claude Code:** save [SKILL.md](https://raw.githubusercontent.com/kkindasara/company-zoom-in/main/company-zoom-in/SKILL.md) as `~/.claude/skills/company-zoom-in/SKILL.md`.

## Use

Ask Claude in plain words, for example:

> Zoom in on Wayfair for Elihome.

> What does Shopify mean for Elihome? Map it.

Claude researches the company on the web, checks the key facts, then builds the PDF. Expect it to take several minutes.

## What it needs

- Web search, for the research and the fact check.
- Python with `reportlab`, and `rsvg-convert`, to draw the map and the PDF. Both generators (`build_map.py` and `build_onepager.py`) are written out inside `SKILL.md`, and Claude saves and runs them itself.

## Limits

- It knows only Elihome's sales channels (Shopify store, Amazon, Walmart, Wayfair, a Japanese website). It does not know Elihome's revenue, best-sellers or marketplace programmes, so any implication that depends on them is written as "if".
- Facts are as of the day you run it. AI commerce changes quickly, so check the dates before reusing an old PDF.
- When it cannot open a source, the fact is marked as not confirmed rather than left out silently. Read the "Caution" lines before you make decisions with it.
