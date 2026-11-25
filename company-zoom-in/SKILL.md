---
name: "company-zoom-in"
description: "Zoom in on one company for Elihome. From just a company name, produce a sourced one-page profile (what it does, dated key numbers, role in AI commerce, what it means for Elihome) with A-D source tiers and a fact-check table, plus a system map in the house style. Use whenever the user names a company and asks to zoom in, profile it, map it, size it up, or asks what it means for Elihome or AI commerce, even if they give only the name."
---

# Company zoom-in

**Input:** a company name.
**Output:** one PDF of two pages, read together:
1. **One-pager** (A4 portrait), in the format of Leo's Amazon one-pager: zoom path, key findings, two charts, the AI commerce sub-ecosystem table, what it means for Elihome, a fact check and tiered sources.
2. **System map** (A4 landscape): the company in the centre, the groups it deals with around it, colour-coded flows, Elihome's position, and sources with tiers in the footer.

The reader uses this to make decisions for Elihome, so a wrong number or an unflagged rumour costs more than a missing one. When something can't be confirmed, say so plainly instead of smoothing it over.

## Elihome (the lens for everything)

- Kitchenware brand.
- Sells through its own Shopify store (DTC), Amazon, Walmart, Wayfair, and a Japanese website.
- That list is all that is known about Elihome here. Don't invent its revenue, best-sellers, which platform runs the Japanese site, or which marketplace programmes it uses (FBA, WFS, CastleGate, etc.). If an implication depends on one of those, say so: "if Elihome uses FBA, ...".
- On the map and in the fact table, Elihome's channel list is source [0]: "Elihome channel list (internal brief)", tier A, no link.

## Source tiers

Tier each fact by the source it actually comes from:

| Tier | Meaning | Typical sources |
|---|---|---|
| A | Official / original | Annual report, 10-K/20-F, earnings release, investor deck, company press release, official product/help/developer docs, regulator filings and decisions, court records, the original study |
| B | Independent | Reputable outlets doing their own reporting (Reuters, Bloomberg, FT, WSJ, Nikkei, trade press), academic work, independent analysts |
| C | Has something to sell | Vendors, agencies, consultancies' marketing reports, SaaS blogs, affiliate "best of" lists, sponsored content, partner case studies, a competitor's claims |
| D | Cannot be verified | No traceable origin, anonymous sources, figure not on the linked page, page won't open and nothing else confirms it, leaks, social posts |

Edge cases:
- A news article repeating the company's own number: find and cite the original (A). If you can't, cite the article (B) and write "company-reported".
- Company marketing figures ("millions of merchants", "2x conversion"): tier A, because the company is the origin, but write "company says". The company is selling itself too.
- Estimates (market share, a private company's revenue): tier by whoever made the estimate, and write "estimate".
- A reputable outlet citing unnamed sources: tier D, written as "reported by X citing unnamed sources; not confirmed".
- When sources disagree, show both and say which one you used.

Prefer A, use B to confirm or fill gaps, use C only when nothing better exists (and say so), and never let a D fact carry a conclusion on its own.

## Workflow

### 1. Pin down the company
Make sure which entity the name means (parent or subsidiary, similarly named firms, regional entities). If it's genuinely ambiguous and the user is around, ask one question; otherwise pick the most likely one and state it on the profile's first line. Everything is "as of" today's date.

### 2. Research
Work from the original outward: investor relations (annual report, latest quarter) → newsroom → official product, help and developer docs → independent press → everything else. Search for each topic separately, because one combined search returns shallow results. Look up anything that describes the company *now* (role, size, products, partnerships, availability) instead of relying on what you already know: AI commerce changes month to month.

Cover:
- **What it does**: business model, main segments, how it makes money, where it operates (including Japan).
- **Key numbers** (4-6): revenue and growth, profit or loss, the volume metric that matters for this business (GMV, GPV, orders, active buyers, merchants, users), headcount, market cap or last valuation and funding. Each number needs the period it covers (FY2025, Q3 2026) and the date it was published. Use the latest available; if the newest is more than ~12 months old, say so. Private companies may have few A numbers: say that rather than filling the gap with C or D figures.
- **Role in AI commerce**: anywhere AI sits between a shopper and a purchase, or between a seller and a sale. For example:
  - AI shopping assistants or agents it runs or powers;
  - agentic checkout, and the protocols or standards it builds, backs or joins (names to check, not assume: Agentic Commerce Protocol, Agent Payments Protocol, Universal Commerce Protocol, Visa Intelligent Commerce, Mastercard Agent Pay);
  - product catalogues or feeds it exposes to AI agents, or ingests from merchants;
  - payments, tokenised credentials, fraud or identity checks for agents;
  - ads or sponsored placements inside AI answers;
  - AI tools for merchants (listings, pricing, customer service, ads);
  - blocking or restricting outside AI agents (terms, robots rules, lawsuits).
  For each one, find its status and reach: "announced", "in pilot" and "live in the US" are different facts, and Japan availability matters for Elihome's Japanese site.
- **Elihome touchpoints**: is the company one of Elihome's channels, the owner or partner of a channel, a payments/logistics/ads layer under a channel, a competitor for the same shoppers, a tool supplier, or a gatekeeper of AI discovery?

Keep a working list as you go (fact, number/date, URL, tier). Everything in both outputs comes from that list.

### 3. Check at least 5 key facts against their sources
Pick the facts that matter most: all key numbers first, then the AI-commerce claims the Elihome section relies on. For each, open the actual page (fetch it; a search snippet is not a check) and confirm that the number, period and date appear there as you wrote them.
- **Checked = yes** only if you opened the page and saw it.
- **Checked = no** otherwise, with the reason ("no: paywalled", "no: figure not on page"). The fact then appears in the one-pager only under Caution, as not confirmed.
- If the page says something different, correct the fact. If the link is a homepage or a search page, replace it with the specific document.
- **Claims that something is missing** ("not available in Japan", "no channel lists X", "not yet") need their own check: open the page that would list it. Country and feature lists are often on each channel's own page, not on the overview. If that page can't be found or opened, write "not confirmed", never "not available".
- **Copy numbers as the source states them**, with their context: who measured what, where and when. "3x the wafers" is not "300% more"; a survey of US consumers about AI search is not a figure about all AI apps.
Five is the minimum; check more when you can.

### 4. Write the one-pager
The one-pager follows the format of Leo's Amazon one-pager (Week 4). Write its content as a JSON spec for `build_onepager.py`, the second generator at the end of this file. Sections, in order:

- **Title**: "Zooming In: [Company], [what it is to Elihome, in a few words]".
- **Checked line**: "Data checked [the date or dates of Step 3]".
- **Byline**: "AI Ecosystem Research | Prepared for Elihome by [the user's name, if known]".
- **Zoom path**: "AI ecosystem → [layer] → [sub-ecosystem] → [Company]", then one sentence on why we zoom in on this company, with citations.
- **Key findings** (3): each starts with a bold one-sentence finding, then one or two sentences of evidence with citations.
- **Charts** (2): small bar charts of checked numbers, 2-4 bars each, with the unit and period in the title and a source note with the tier ("Source: Example Co (2026a), Q3 2026 results, published 3 Nov 2026 [A]"). Never chart an unchecked or tier-D number; if the numbers support only one chart, use one.
- **Inside the AI commerce sub-ecosystem** (3-5 rows): Sub-category | Main players | Where [Company] stands, with its status (live, pilot, announced) and where | Why it matters for Elihome.
- **What this means for Elihome** (4 numbered actions): a bold lead ("Check which AI channels are active.") and one sentence resting on a cited fact. This is our read, so keep it apart from the facts; when it depends on something unknown about Elihome, say "if".
- **Fact check** (3-5 lines), each labelled:
  - *Confirmed*: a key fact opened and seen in Step 3;
  - *Update*: something newer than the team's earlier work or than what the user had;
  - *Correction*: an earlier claim (ours or a source's) that the check proved wrong;
  - *Caution*: anything not confirmed, company-reported only, resting on B sources only, or older than about 12 months. This replaces a separate "Not confirmed" list.
- **Sources**: author-year style, sorted by author, with letters for the same author and year (2026a, 2026b), italic title, date, a short link and the tier, e.g. `Example Co (2026a) <i>Q3 2026 results</i>, 3 Nov 2026. <link href="https://...">example.com</link> [A]`. Include the Elihome brief as `Elihome (2026) <i>Channel list</i>, internal brief. [A]`.
- **Footer**: "Tiers: [A] official or original source; [B] independent source. All accessed [dates]. Drafted with Claude using the company-zoom-in skill; facts checked against the linked sources."

Spec format (illustrative values):

```json
{
  "company": "Example Co",
  "title": "Zooming In: Example Co, the Marketplace Behind ...",
  "checked": "Data checked 19 November 2026",
  "byline": "AI Ecosystem Research | Prepared for Elihome by ...",
  "author": "...",
  "zoom": "AI ecosystem → application layer → AI commerce sub-ecosystem → Example Co. We zoom in because ... (Example Co, 2026a).",
  "findings": ["<b>One-sentence finding.</b> Evidence (Example Co, 2026a).", "...", "..."],
  "charts": [
    {"title": "Q3 2026 revenue by segment ($m)", "labels": ["Segment 1", "Segment 2"], "values": [836, 2906],
     "fmt": "%d", "note": "Source: Example Co (2026a), Q3 2026 results, published 3 Nov 2026 [A]"}
  ],
  "table": [["AI assistants", "ChatGPT, Gemini", "Live in the US (Example Co, 2026b)", "Elihome's listings can appear there"]],
  "actions": ["<b>Lead.</b> One sentence (Example Co, 2026b).", "...", "...", "..."],
  "check": [["Confirmed", "..."], ["Update", "..."], ["Caution", "..."]],
  "sources": ["Elihome (2026) <i>Channel list</i>, internal brief. [A]", "..."],
  "foot": "Tiers: [A] official or original source; [B] independent source. All accessed 19 Nov 2026. Drafted with Claude using the company-zoom-in skill; facts checked against the linked sources."
}
```

Writing rules:
- **One page.** The generator warns when the one-pager runs past page 1; cut words, don't shrink the type or the margins.
- **Citations** are (Author, Year) in the text; the tier and the link sit in Sources.
- **Dates are explicit**: "FY2025 (year to 31 Jan 2026)", "announced 14 Oct 2026". Never "recently" or "last year".
- **Uncertainty goes in the sentence itself**: "company says", "estimate", "reported, not confirmed". Not in a footnote.
- **Statistics are not slogans**: a line like "100% of the bottleneck" is rhetoric; drop it or quote it as such.
- **Facts and analysis stay apart**: facts carry sources; the actions for Elihome point back to the facts they rest on.

### 5. Build the system map
Use the generator at the end of this file. It fixes the house style (layout, colours, arrow styles, fonts) so every map looks the same. Save it as `build_map.py`, write a spec JSON, and run:

```bash
python3 build_map.py spec.json <slug>-map.html <slug>-map.svg
```

What goes on the map:
- **Centre**: the company, with a subtitle of 6 words or fewer.
- **Groups** (5-8): the kinds of parties the company deals with, each with 1-3 named examples: shoppers, merchants/brands, AI assistants and LLM platforms, payment networks, marketplaces, logistics, suppliers, advertisers, investors, regulators. Pick the ones that matter for *this* company; a group with no arrows doesn't belong on the map. Slots: `top`, `top-right`, `right`, `bottom-right`, `bottom`, `bottom-left`, `left`, `top-left`. Use `x`/`y` instead of a slot only if you need a ninth position.
- **Arrows** (8-14): one flow each, labelled in 4 words or fewer, pointing the way the money, goods or information travels:
  - `money`: green solid (fees, payments, revenue share, investment)
  - `materials`: purple dashed (physical goods only: inventory, shipments, returns). Reports, papers, data, rules and model outputs are information, even when they are sold.
  - `information`: orange dotted (data, product feeds, recommendations, rules, APIs)
  Every arrow lists its source numbers in `src`. An arrow without a source is either marked `"unconfirmed": true` (with a tier-D source) or left off.
  Keep arrows to and from the centre, or between Elihome and a group next to it. An arrow between two outer groups crosses the map and its label lands on other arrows; leave it off or mention it in Relationships to notice instead.
  Draw at most 2 arrows between Elihome and the company: merge flows of the same type ("plan + payment fees") and move the rest to Relationships to notice.
  A label names what moves ("referral fees", "product feed"), never a description of a node ("foundational layer for all"); that belongs in the group's examples.
  Show where the money comes from: at least one paying customer or buyer group sends money into the map.
- **Elihome**: always on the map, in a free slot next to the group it belongs to, with its real flows to and from the company (fees, stock, listings and data, orders). Flows it doesn't have yet but could have are added with `"possible": true` and drawn faded.
- **Left panel**: `headline` is the one sentence a busy reader should take away, ideally about Elihome, in 20 words or fewer (about 140 characters). `notice` holds 3-5 "Relationships to notice", each one sentence naming the two parties and why the flow matters. Give the matching arrow `"notice": n` so a gold number badge ties the two together.
- **No placeholders**: no "----" or "TBD" in the panel or anywhere else. Numbers in the headline and notices are copied as the source states them, with their context, as on the one-pager.
- **Footer**: sources numbered from 0 (the Elihome brief) upward, with tier, short title, date and URL; 15 at most. Arrow labels use the same numbers, and the sources are the same ones the profile uses.

Spec format (illustrative values):

```json
{
  "company": "Example Co",
  "subtitle": "Online marketplace",
  "as_of": "19 Nov 2026",
  "headline": "One sentence the reader should take away, ideally about Elihome.",
  "notice": ["First relationship to notice.", "Second.", "Third."],
  "groups": [
    {"id": "shoppers", "slot": "top", "title": "Shoppers", "examples": "US and Japanese consumers"},
    {"id": "ai", "slot": "top-right", "title": "AI assistants", "examples": "Named assistants"},
    {"id": "logistics", "slot": "bottom-right", "title": "Logistics", "examples": "Fulfilment centres"}
  ],
  "elihome": {"slot": "bottom-left", "note": "Kitchenware · Shopify, Amazon, Walmart, Wayfair, JP site"},
  "edges": [
    {"from": "shoppers", "to": "core", "type": "money", "label": "purchases", "src": [1]},
    {"from": "core", "to": "ai", "type": "information", "label": "catalogue feed", "src": [2], "notice": 1},
    {"from": "core", "to": "logistics", "type": "materials", "label": "inventory", "src": [1]},
    {"from": "elihome", "to": "core", "type": "money", "label": "referral fees", "src": [0, 1], "notice": 2},
    {"from": "elihome", "to": "ai", "type": "information", "label": "product feed", "possible": true},
    {"from": "ai", "to": "core", "type": "information", "label": "agent orders", "src": [3], "unconfirmed": true, "notice": 3}
  ],
  "sources": [
    {"n": 0, "tier": "A", "title": "Elihome channel list (internal brief)", "url": ""},
    {"n": 1, "tier": "A", "title": "Example Co annual report FY2025", "date": "Feb 2026", "url": "https://..."},
    {"n": 2, "tier": "A", "title": "Example Co press release", "date": "Sep 2026", "url": "https://..."},
    {"n": 3, "tier": "D", "title": "Blog citing unnamed sources", "date": "Nov 2026", "url": "https://..."}
  ]
}
```

Edge endpoints are a group `id`, `"core"` (the company) or `"elihome"`. Optional per-arrow fields: `pos` (0.15-0.85, slides the label along the arrow) and `bend` (set on the first arrow between two boxes; curves every arrow between them).

After running, fix every `WARNING` line (shorten a label, move a group to another slot, or set `pos` or `bend`). Then render and look at the result: `rsvg-convert -w 1600 <slug>-map.svg -o <slug>-map.png` (or a headless-browser screenshot) and view the PNG. Check that no label sits on a box, another label or another arrow, each arrow points the right way, and the left panel doesn't run off the bottom. Colours and fonts are constants at the top of the script; change them there if the house style changes.

### 6. Deliver
Render the map, then build one PDF with the one-pager on page 1 and the map on page 2:

```bash
rsvg-convert -w 3200 <slug>-map.svg -o <slug>-map.png
python3 build_onepager.py onepager.json <Company>_Zoom_In.pdf <slug>-map.png
```

Fix any `WARNING` (cut words until the one-pager fits), then render both pages of the PDF and look at them.
- **PDF**: send `<Company>_Zoom_In.pdf`; this is the deliverable.
- **Map**: also send the PNG if the user wants an image for slides, and publish `<slug>-map.html` as an artifact if they want a link.
- **Reply**: one line with the takeaway for Elihome, plus any important Caution item. Don't restate the one-pager.

### 7. Final check
- Every fact on both pages has a source and a tier (the Elihome brief has no link), and the map's sources are the same ones the one-pager lists.
- At least 5 key facts were opened and checked; every fact that wasn't is under Caution, with the reason.
- No claim that something is missing or unavailable unless the page that would list it was opened.
- Every number has a period and a publication date and matches the source's wording and context; no slogan is presented as data.
- Sources are primary where one exists: no forum, Reddit or vendor blog for a figure that an official report or the original study gives.
- The map has no placeholder text, every arrow's colour matches what moves, and there are at most 2 arrows between Elihome and the company.
- The PDF has exactly 2 pages: the one-pager fits page 1 and the map renders cleanly on page 2, with Elihome easy to spot.

## Map generator: build_map.py

```python
#!/usr/bin/env python3
"""build_map.py: turn a JSON spec into a company system map in the house style.

Usage:  python3 build_map.py spec.json map.html [map.svg]
The HTML page wraps one inline SVG (1600x1000). Warnings about overflow go to stderr.
"""
import json, math, sys, textwrap
from html import escape as esc
from urllib.parse import urlparse

W, H, PANEL, FOOT = 1600, 1000, 440, 860   # canvas, left-panel width, footer top
CORE = (1020, 430, 290, 140)               # x, y (centre), w, h of the company node
GW, GH = 250, 96                           # group box size
SLOTS = {"top": (1020, 105), "top-right": (1395, 205), "right": (1460, 430),
         "bottom-right": (1395, 655), "bottom": (1020, 760), "bottom-left": (645, 655),
         "left": (580, 430), "top-left": (645, 205)}
INK, PAPER, GOLD = "#1C2230", "#FAFAF7", "#F2C14E"
LINE = {"money": "#2E8B57", "materials": "#7B3FC4", "information": "#E07B1A"}
LABEL = {"money": "#1F6B41", "materials": "#5E2E9E", "information": "#A9560C"}
DASH = {"money": "", "materials": ' stroke-dasharray="10 6"',
        "information": ' stroke-dasharray="1 6" stroke-linecap="round"'}
warnings = []


def wrap(text, width, max_lines=None):
    lines = textwrap.wrap(str(text), width) or [""]
    if max_lines and len(lines) > max_lines:
        warnings.append(f"text cut to {max_lines} lines: {text[:50]}...")
        lines = lines[:max_lines]
        lines[-1] = lines[-1][: width - 1] + "…"
    return lines


def tspans(lines, x, lh):
    return "".join(f'<tspan x="{x}" dy="{0 if i == 0 else lh}">{esc(l)}</tspan>'
                   for i, l in enumerate(lines))


def box_text(x, y, title, sub, tcls, scls, tw=24, sw=34, tlh=20, slh=17):
    t, s = wrap(title, tw, 2), (wrap(sub, sw, 2) if sub else [])
    total = len(t) * tlh + len(s) * slh
    y0 = y - total / 2 + tlh * 0.75
    out = f'<text class="{tcls}" x="{x}" y="{y0:.0f}" text-anchor="middle">{tspans(t, x, tlh)}</text>'
    if s:
        out += (f'<text class="{scls}" x="{x}" y="{y0 + len(t) * tlh + 2:.0f}" '
                f'text-anchor="middle">{tspans(s, x, slh)}</text>')
    return out


def border(node, px, py, dx, dy):
    """From a point inside the node's box, walk along (dx, dy) to the box edge."""
    x, y, w, h = node
    ts = []
    if abs(dx) > 1e-9:
        ts.append((x + math.copysign(w / 2, dx) - px) / dx)
    if abs(dy) > 1e-9:
        ts.append((y + math.copysign(h / 2, dy) - py) / dy)
    t = min(t for t in ts if t > 0)
    return px + dx * t, py + dy * t


def main(spec_path, html_path, svg_path=None):
    s = json.load(open(spec_path, encoding="utf-8"))
    nodes = {"core": CORE}
    parts_nodes = []

    def place(item):
        if "x" in item and "y" in item:
            return item["x"], item["y"]
        if item.get("slot") not in SLOTS:
            sys.exit(f"node {item.get('id')} needs a slot ({', '.join(SLOTS)}) or x/y")
        return SLOTS[item["slot"]]

    # company in the centre
    cx, cy, cw, ch = CORE
    parts_nodes.append(f'<rect x="{cx - cw/2}" y="{cy - ch/2}" width="{cw}" height="{ch}" rx="18" fill="{INK}"/>'
                       + box_text(cx, cy, s["company"], s.get("subtitle", ""), "core-t", "core-s", 18, 32, 30))
    # related groups
    for g in s["groups"]:
        x, y = place(g)
        nodes[g["id"]] = (x, y, GW, GH)
        parts_nodes.append(f'<rect x="{x - GW/2}" y="{y - GH/2}" width="{GW}" height="{GH}" rx="12" class="g-box"/>'
                           + box_text(x, y, g["title"], g.get("examples", ""), "g-t", "g-s"))
    # Elihome
    e = s["elihome"]
    x, y = place(e)
    nodes["elihome"] = (x, y, GW, GH)
    parts_nodes.append(f'<rect x="{x - GW/2}" y="{y - GH/2}" width="{GW}" height="{GH}" rx="12" class="eli-box"/>'
                       f'<text class="eli-tag" x="{x}" y="{y - GH/2 - 9}" text-anchor="middle">ELIHOME\'S POSITION</text>'
                       + box_text(x, y, "Elihome", e.get("note", ""), "g-t", "g-s"))

    # arrows. Parallel arrows between the same two nodes are spread apart; an arrow whose
    # straight path would cross another box is bent; labels are nudged until they sit clear.
    boxes = {k: (v[0] - v[2] / 2 - 6, v[1] - v[3] / 2 - (26 if k == "elihome" else 6),
                 v[0] + v[2] / 2 + 6, v[1] + v[3] / 2 + 6) for k, v in nodes.items()}

    def hits(b, others):
        return any(not (b[2] < o[0] or b[0] > o[2] or b[3] < o[1] or b[1] > o[3]) for o in others)

    def bez(S, C, E, t):
        u = 1 - t
        return (u*u*S[0] + 2*u*t*C[0] + t*t*E[0], u*u*S[1] + 2*u*t*C[1] + t*t*E[1],
                2*u*(C[0]-S[0]) + 2*t*(E[0]-C[0]), 2*u*(C[1]-S[1]) + 2*t*(E[1]-C[1]))

    pairs = {}
    for ed in s["edges"]:
        for end in (ed["from"], ed["to"]):
            if end not in nodes:
                sys.exit(f"edge refers to unknown node '{end}'")
        if ed["type"] not in LINE:
            sys.exit(f"edge type must be one of {list(LINE)}")
        pairs.setdefault(tuple(sorted((ed["from"], ed["to"]))), []).append(ed)
    lines_svg, labels_svg, placed = [], [], []
    for (a, b), eds in pairs.items():
        ax, ay = nodes[a][:2]; bx, by = nodes[b][:2]
        L = math.hypot(bx - ax, by - ay)
        nx, ny = -(by - ay) / L, (bx - ax) / L            # one normal per pair
        others = [v for k, v in boxes.items() if k not in (a, b)]
        bend = eds[0].get("bend")
        if bend is None:                                  # smallest bend that clears other boxes
            for bend in (0, 140, -140, 220, -220, 300, -300):
                C = ((ax + bx) / 2 + nx * bend, (ay + by) / 2 + ny * bend)
                if not any(hits((p[0] - 2, p[1] - 2, p[0] + 2, p[1] + 2), others)
                           for p in (bez((ax, ay), C, (bx, by), k / 24) for k in range(3, 22))):
                    break
            else:
                warnings.append(f"arrow {a}-{b} crosses another box: move a node or set 'bend'")
        n = len(eds)
        for i, ed in enumerate(eds):
            off = (i - (n - 1) / 2) * 30
            f, t = nodes[ed["from"]], nodes[ed["to"]]
            sgn = 1 if ed["from"] == a else -1
            C = ((ax + bx) / 2 + nx * (bend + off), (ay + by) / 2 + ny * (bend + off))
            fo, to_ = (f[0] + nx * off, f[1] + ny * off), (t[0] + nx * off, t[1] + ny * off)
            d1 = (C[0] - fo[0], C[1] - fo[1]); d2 = (C[0] - to_[0], C[1] - to_[1])
            S = border(f, *fo, *d1); E = border(t, *to_, *d2)
            n1, n2 = math.hypot(*d1), math.hypot(*d2)
            S = (S[0] + d1[0] / n1 * 4, S[1] + d1[1] / n1 * 4)
            E = (E[0] + d2[0] / n2 * 7, E[1] + d2[1] / n2 * 7)
            typ = ed["type"]
            op = ' opacity="0.45"' if ed.get("possible") else ""
            path = (f"M{S[0]:.1f},{S[1]:.1f} L{E[0]:.1f},{E[1]:.1f}" if bend == 0 else
                    f"M{S[0]:.1f},{S[1]:.1f} Q{C[0]:.1f},{C[1]:.1f} {E[0]:.1f},{E[1]:.1f}")
            lines_svg.append(f'<path d="{path}" fill="none" stroke="{LINE[typ]}" stroke-width="2.6"'
                             f'{DASH[typ]} marker-end="url(#ah-{typ})"{op}/>')
            if bend == 0:
                C = ((S[0] + E[0]) / 2, (S[1] + E[1]) / 2)
            # label: try positions along the arrow, then sides, until it clears boxes and labels
            text = ed["label"]
            if ed.get("src"):
                text += " [" + ",".join(str(r) for r in ed["src"]) + "]"
            if ed.get("unconfirmed"):
                text += " · unconfirmed"
            if ed.get("possible"):
                text += " · possible"
            base = ed.get("pos", 0.5 if n == 1 else 0.3 + 0.4 * i / (n - 1))
            sides = [1 if off > 0 else -1] if off else [0, 1, -1]
            choice = None
            for width in (22, 14):
                ls = wrap(text, width, 3)
                w = max(len(l) for l in ls) * 7.2 + (30 if ed.get("notice") else 0)
                h = len(ls) * 16 + 4
                for dp in (0, .12, -.12, .24, -.24, .34, -.34):
                    for side in sides:
                        tt = min(max(base + dp * sgn, .15), .85)
                        px, py, tx, ty = bez(S, C, E, tt)
                        tl = math.hypot(tx, ty) or 1
                        qx, qy = -ty / tl * sgn, tx / tl * sgn
                        push = side * (abs(qx) * w / 2 + abs(qy) * h / 2 + 6)
                        cx_, cy_ = px + qx * push, py + qy * push
                        bb = (cx_ - w / 2, cy_ - h / 2, cx_ + w / 2, cy_ + h / 2)
                        inside = bb[0] > PANEL + 6 and bb[2] < W - 6 and bb[1] > 6 and bb[3] < FOOT - 6
                        if choice is None:
                            choice = (cx_, cy_, bb, ls)
                        if inside and not hits(bb, placed + list(boxes.values())):
                            choice = (cx_, cy_, bb, ls)
                            break
                    else:
                        continue
                    break
                else:
                    continue
                break
            else:
                warnings.append(f"label '{ed['label']}' overlaps something: shorten it, set 'pos' or move a node")
            cx_, cy_, bb, ls = choice
            placed.append(bb)
            tx0 = cx_ + (15 if ed.get("notice") else 0)
            y0 = cy_ - (len(ls) - 1) * 8 + 4
            labels_svg.append(f'<text class="lbl" x="{tx0:.1f}" y="{y0:.1f}" fill="{LABEL[typ]}" '
                              f'text-anchor="middle"{op}>{tspans(ls, round(tx0, 1), 16)}</text>')
            if ed.get("notice"):
                bxp = bb[0] + 11
                labels_svg.append(f'<circle cx="{bxp:.1f}" cy="{cy_:.1f}" r="11" fill="{GOLD}" stroke="{INK}" '
                                  f'stroke-width="1.5"/><text class="badge-t" x="{bxp:.1f}" y="{cy_ + 4:.1f}" '
                                  f'text-anchor="middle">{ed["notice"]}</text>')

    # left panel
    P = [f'<rect x="0" y="0" width="{PANEL}" height="{H}" fill="{INK}"/>',
         f'<text class="eyebrow" x="36" y="54">COMPANY ZOOM-IN · AS OF {esc(s["as_of"].upper())}</text>']
    tl = wrap(s["company"], 18, 2)
    P.append(f'<text class="title" x="36" y="104">{tspans(tl, 36, 44)}</text>')
    y = 104 + (len(tl) - 1) * 44 + 52
    hl = wrap(s["headline"], 30, 5)
    P.append(f'<text class="headline" x="36" y="{y}">{tspans(hl, 36, 30)}</text>')
    y += (len(hl) - 1) * 30 + 62
    P.append(f'<text class="p-h" x="36" y="{y}">RELATIONSHIPS TO NOTICE</text>')
    y += 38
    for k, item in enumerate(s["notice"], 1):
        il = wrap(item, 38, 5)
        P.append(f'<circle cx="48" cy="{y - 5}" r="12" fill="{GOLD}"/>'
                 f'<text class="p-num" x="48" y="{y - 1}" text-anchor="middle">{k}</text>'
                 f'<text class="p-txt" x="72" y="{y}">{tspans(il, 72, 21)}</text>')
        y += (len(il) - 1) * 21 + 38
    if y > H - 20:
        warnings.append(f"left panel overflows ({y:.0f}px > {H - 20}px): shorten headline or notices")

    # footer: key + sources
    F = [f'<rect x="{PANEL}" y="{FOOT}" width="{W - PANEL}" height="{H - FOOT}" fill="#ECEAE4"/>',
         f'<line x1="{PANEL}" y1="{FOOT}" x2="{W}" y2="{FOOT}" stroke="#C9C6BC"/>',
         f'<text class="f-h" x="466" y="886">KEY</text>']
    for j, (typ, name) in enumerate([("money", "Money"), ("materials", "Materials / goods"),
                                     ("information", "Information / data")]):
        yy = 908 + j * 22
        F.append(f'<line x1="466" y1="{yy}" x2="516" y2="{yy}" stroke="{LINE[typ]}" stroke-width="2.6"{DASH[typ]} '
                 f'marker-end="url(#ah-{typ})"/><text class="f-txt" x="528" y="{yy + 4}">{name}</text>')
    F.append(f'<rect x="466" y="966" width="50" height="18" rx="5" class="eli-box"/>'
             f'<text class="f-txt" x="528" y="980">Elihome · faded = possible</text>')
    srcs = s["sources"]
    F.append('<text class="f-h" x="700" y="886">SOURCES <tspan class="f-note">· tier A official/original · '
             'B independent · C has something to sell · D cannot be verified</tspan></text>')
    ncol = 2 if len(srcs) <= 10 else 3
    rows = max(1, math.ceil(len(srcs) / ncol))
    if rows > 5:
        warnings.append(f"{len(srcs)} sources do not fit the footer (max 15): merge or drop minor ones")
    colw = (W - 700 - 20) / ncol
    maxc = int(colw / 6.3)
    for k, src in enumerate(srcs):
        col, row = divmod(k, rows)
        xx, yy = 700 + col * colw, 908 + row * 18
        dom = urlparse(src.get("url", "")).netloc.replace("www.", "")
        body = src["title"] + (f", {src['date']}" if src.get("date") else "") + (f" — {dom}" if dom else "")
        lead = f'[{src["n"]}] {src["tier"]} · '
        if len(lead) + len(body) > maxc:
            body = body[: maxc - len(lead) - 1] + "…"
        t = (f'<text class="f-txt" x="{xx:.0f}" y="{yy}"><tspan class="f-ref">[{src["n"]}] '
             f'{esc(src["tier"])}</tspan> · {esc(body)}</text>')
        F.append(f'<a href="{esc(src["url"])}" target="_blank">{t}</a>' if src.get("url") else t)

    css = f"""
  .eyebrow{{font:600 12px Inter,'Helvetica Neue',Arial,sans-serif;letter-spacing:.12em;fill:#9AA3B5}}
  .title{{font:700 40px Inter,'Helvetica Neue',Arial,sans-serif;fill:#fff}}
  .headline{{font:600 22px Inter,'Helvetica Neue',Arial,sans-serif;fill:#F2F2F2}}
  .p-h{{font:700 13px Inter,'Helvetica Neue',Arial,sans-serif;letter-spacing:.12em;fill:{GOLD}}}
  .p-txt{{font:400 15px Inter,'Helvetica Neue',Arial,sans-serif;fill:#D9DCE3}}
  .p-num,.badge-t{{font:700 13px Inter,'Helvetica Neue',Arial,sans-serif;fill:{INK}}}
  .core-t{{font:700 26px Inter,'Helvetica Neue',Arial,sans-serif;fill:#fff}}
  .core-s{{font:400 14px Inter,'Helvetica Neue',Arial,sans-serif;fill:#C9CEDA}}
  .g-box{{fill:#fff;stroke:#B9BDC7;stroke-width:1.5}}
  .eli-box{{fill:#FFE08A;stroke:{INK};stroke-width:3}}
  .eli-tag{{font:700 11px Inter,'Helvetica Neue',Arial,sans-serif;letter-spacing:.12em;fill:{INK}}}
  .g-t{{font:700 17px Inter,'Helvetica Neue',Arial,sans-serif;fill:{INK}}}
  .g-s{{font:400 13px Inter,'Helvetica Neue',Arial,sans-serif;fill:#5A6170}}
  .lbl{{font:600 13px Inter,'Helvetica Neue',Arial,sans-serif;paint-order:stroke;stroke:{PAPER};stroke-width:5px;stroke-linejoin:round}}
  .f-h{{font:700 12px Inter,'Helvetica Neue',Arial,sans-serif;letter-spacing:.1em;fill:{INK}}}
  .f-note{{font-weight:400;letter-spacing:0;fill:#5A6170}}
  .f-txt{{font:400 12px Inter,'Helvetica Neue',Arial,sans-serif;fill:#3B4252}}
  .f-ref{{font-weight:700;fill:{INK}}}
  a .f-txt:hover{{text-decoration:underline}}"""
    markers = "".join(
        f'<marker id="ah-{t}" viewBox="0 0 10 10" refX="8" refY="5" markerWidth="7" markerHeight="7" '
        f'orient="auto-start-reverse"><path d="M0,0 L10,5 L0,10 z" fill="{c}"/></marker>' for t, c in LINE.items())
    svg = (f'<svg viewBox="0 0 {W} {H}" width="{W}" height="{H}" xmlns="http://www.w3.org/2000/svg" role="img" '
           f'aria-labelledby="mt md"><title id="mt">{esc(s["company"])}: system map</title>'
           f'<desc id="md">{esc(s["headline"])}</desc><style>{css}</style><defs>{markers}</defs>'
           f'<rect x="{PANEL}" y="0" width="{W - PANEL}" height="{FOOT}" fill="{PAPER}"/>'
           + "".join(lines_svg) + "".join(parts_nodes) + "".join(labels_svg) + "".join(P) + "".join(F) + "</svg>")
    html = (f'<!DOCTYPE html>\n<html lang="en"><head><meta charset="utf-8">'
            f'<meta name="viewport" content="width=device-width, initial-scale=1">'
            f'<title>{esc(s["company"])}: system map</title><style>body{{margin:0;background:#ECEAE4}}'
            f'svg{{display:block;width:100%;height:auto;max-width:{W}px;margin:0 auto}}</style></head>'
            f'<body>{svg}</body></html>\n')
    open(html_path, "w", encoding="utf-8").write(html)
    if svg_path:
        open(svg_path, "w", encoding="utf-8").write(svg)
    for w_ in warnings:
        print("WARNING:", w_, file=sys.stderr)
    print(f"wrote {html_path}" + (f" and {svg_path}" if svg_path else ""))


if __name__ == "__main__":
    if len(sys.argv) < 3:
        sys.exit(__doc__)
    main(*sys.argv[1:4])
```

## One-pager generator: build_onepager.py

```python
#!/usr/bin/env python3
"""build_onepager.py: turn a JSON spec into the one-page zoom-in (A4) in the house style,
with the system map as page 2.

Usage:  python3 build_onepager.py onepager.json Company_Zoom_In.pdf [company-map.png]
Text fields accept ReportLab mini-HTML: <b>, <i>, <link href="...">. Warnings go to stderr.
"""
import json, os, sys
from reportlab.lib import colors
from reportlab.lib.fonts import addMapping
from reportlab.lib.pagesizes import A4, landscape
from reportlab.lib.styles import ParagraphStyle
from reportlab.lib.units import cm
from reportlab.pdfbase import pdfmetrics
from reportlab.pdfbase.ttfonts import TTFont
from reportlab.platypus import (BaseDocTemplate, Frame, Image, NextPageTemplate, PageBreak,
                                PageTemplate, Paragraph, Spacer, Table, TableStyle)
from reportlab.graphics.charts.barcharts import VerticalBarChart
from reportlab.graphics.shapes import Drawing, String

# Fonts: DejaVu if present (it has the → arrow); otherwise Helvetica, with → written as ->.
FONT, BOLD, ARROW = "Helvetica", "Helvetica-Bold", "->"
for d in ("/usr/share/fonts/truetype/dejavu", "/Library/Fonts", os.path.expanduser("~/Library/Fonts")):
    if os.path.exists(f"{d}/DejaVuSans.ttf") and os.path.exists(f"{d}/DejaVuSans-Bold.ttf"):
        pdfmetrics.registerFont(TTFont("DV", f"{d}/DejaVuSans.ttf"))
        pdfmetrics.registerFont(TTFont("DVB", f"{d}/DejaVuSans-Bold.ttf"))
        for b, i, f in ((0, 0, "DV"), (1, 0, "DVB"), (0, 1, "DV"), (1, 1, "DVB")):
            addMapping("DV", b, i, f)
        FONT, BOLD, ARROW = "DV", "DVB", "→"
        break

INK, GREY, ACC = colors.HexColor("#1C2230"), colors.HexColor("#555B66"), colors.HexColor("#2E5E8C")
MARGIN = 1.4 * cm


def S(name, **k):
    return ParagraphStyle(name, **{**dict(fontName=FONT, fontSize=7.6, leading=9.6, textColor=INK), **k})


def P(text, style):
    return Paragraph(str(text).replace("→", ARROW), style)


H2 = S("h2", fontSize=9, leading=11, fontName=BOLD, textColor=ACC, spaceBefore=4, spaceAfter=2)
CELL, CELLH = S("c", fontSize=6.9, leading=8.4), S("ch", fontSize=6.9, leading=8.4, fontName=BOLD, textColor=colors.white)


def chart(c):
    d = Drawing(250, 118)
    d.add(String(0, 106, c["title"], fontName=BOLD, fontSize=7.6, fillColor=INK))
    b = VerticalBarChart()
    b.x, b.y, b.width, b.height = 28, 22, 205, 70
    b.data = [c["values"]]
    b.categoryAxis.categoryNames = c["labels"]
    b.categoryAxis.labels.fontName = b.valueAxis.labels.fontName = FONT
    b.categoryAxis.labels.fontSize, b.valueAxis.labels.fontSize = 6.6, 6
    b.valueAxis.valueMin = 0
    b.bars[0].fillColor, b.bars[0].strokeColor = ACC, None
    b.barLabelFormat = c.get("fmt", "%s")
    b.barLabels.fontName, b.barLabels.fontSize, b.barLabels.nudge = FONT, 6.6, 6
    d.add(b)
    d.add(String(0, 2, c["note"], fontName=FONT, fontSize=5.8, fillColor=GREY))
    return d


def main(spec_path, out, map_png=None):
    s = json.load(open(spec_path, encoding="utf-8"))
    W = A4[0] - 2 * MARGIN
    doc = BaseDocTemplate(out, pagesize=A4, title=s["title"], author=s.get("author", ""))
    LW, LH = landscape(A4)
    doc.addPageTemplates([
        PageTemplate("portrait", [Frame(MARGIN, 1.0 * cm, W, A4[1] - 2.1 * cm, id="p")], pagesize=A4),
        PageTemplate("landscape", [Frame(0.7 * cm, 0.7 * cm, LW - 1.4 * cm, LH - 1.4 * cm, id="l")], pagesize=(LW, LH)),
    ])
    st = [P(s["title"], S("t", fontSize=13.5, leading=16, fontName=BOLD)),
          P(s["checked"], S("dc", fontSize=7.4, fontName=BOLD, textColor=ACC)),
          P(s["byline"], S("by", fontSize=7.4, textColor=GREY)), Spacer(1, 4),
          P("<b>Zoom path:</b> " + s["zoom"], S("z")), P("Key findings", H2)]
    st += [P("• " + f, S("f", leftIndent=8, firstLineIndent=-8, spaceAfter=1.5)) for f in s["findings"]]
    if s.get("charts"):
        ct = Table([[chart(c) for c in s["charts"][:2]]], colWidths=[W / 2] * len(s["charts"][:2]))
        ct.setStyle(TableStyle([("LEFTPADDING", (0, 0), (-1, -1), 0), ("TOPPADDING", (0, 0), (-1, -1), 3)]))
        st.append(ct)
    st.append(P("Inside the AI commerce sub-ecosystem", H2))
    hdr = ["Sub-category", "Main players", f"Where {s['company']} stands", "Why it matters for Elihome"]
    rows = [[P(h, CELLH) for h in hdr]] + [[P(x, CELL) for x in r] for r in s["table"]]
    t = Table(rows, colWidths=[W * 0.17, W * 0.25, W * 0.28, W * 0.30])
    t.setStyle(TableStyle([("BACKGROUND", (0, 0), (-1, 0), INK), ("VALIGN", (0, 0), (-1, -1), "TOP"),
                           ("ROWBACKGROUNDS", (0, 1), (-1, -1), [colors.white, colors.HexColor("#F2F3F5")]),
                           ("LINEBELOW", (0, 0), (-1, -1), 0.3, colors.HexColor("#D5D8DD")),
                           ("TOPPADDING", (0, 0), (-1, -1), 2.5), ("BOTTOMPADDING", (0, 0), (-1, -1), 2.5)]))
    st += [t, P("What this means for Elihome", H2)]
    st += [P(f"{i}. {a}", S("a", leftIndent=10, firstLineIndent=-10, spaceAfter=1.5)) for i, a in enumerate(s["actions"], 1)]
    st.append(P("Fact check", H2))
    st += [P(f"<b>{lab}:</b> {txt}", S("k", spaceAfter=1)) for lab, txt in s["check"]]
    st.append(P("Sources", H2))
    st += [P(x, S("src", fontSize=6.5, leading=8, leftIndent=8, firstLineIndent=-8)) for x in s["sources"]]
    st += [Spacer(1, 3), P(s["foot"], S("ft", fontSize=6.4, leading=8, textColor=GREY))]
    if map_png:
        from reportlab.lib.utils import ImageReader
        iw, ih = ImageReader(map_png).getSize()
        k = min((LW - 1.6 * cm) / iw, (LH - 1.6 * cm) / ih)
        st += [NextPageTemplate("landscape"), PageBreak(), Image(map_png, iw * k, ih * k)]
    doc.build(st)
    want = 2 if map_png else 1
    if doc.page != want:
        print(f"WARNING: {doc.page} pages, expected {want}: the one-pager runs past one page; cut words.", file=sys.stderr)


if __name__ == "__main__":
    if len(sys.argv) < 3:
        sys.exit(__doc__)
    main(*sys.argv[1:4])
```
