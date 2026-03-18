# BUNDLE//MASTER

**Daily Vibe Coded Project #2**

A zero-dependency, fully offline bundle and pledge evaluator. Built for crowdfunding campaigns (Kickstarter, Backerkit, Gamefound, Indiegogo) and general product bundle comparisons — beer packs, subscription boxes, collector sets, anything where you need to compare what you actually get across tiers before committing.

---

## What it does

Paste raw campaign copy → parse it into structured tiers → evaluate and score each tier → get a clear recommendation.

The scoring engine weighs content value, item quantity, exclusivity, collector appeal, budget fit, and delivery cost against each other. You control how much each factor matters via sliders. Premium and collector items are tagged per-line and carry higher weight in the score — a Legend metal card counts for more than a standard booster pack.

---

## Features

**Tier Parser**
- Paste any raw campaign text — newline separated, inline ` - ` separated, or `1 x Name` packed format (common in webshop bundles)
- Automatically extracts tier name, price, exclusivity score, collector score, and full item list
- Handles multiplier chains: `6 displays (216 Beta Booster Packs)` → 216 packs
- Handles colon breakdowns: `4 starter decks: 2 of X and 2 of Y` → Starter Decks ×4
- Raw source string preserved alongside parsed rows for cross-checking

**Item Rows**
- Each parsed item is an editable row: name, quantity, and a tag
- Tags cycle through `STANDARD` / `COLLECTOR` / `PREMIUM` on click
- Auto-detected from keywords (`metal`, `legend`, `foil` → premium; `dice`, `playmat`, `exclusive` → collector)
- Add or remove rows manually after parsing
- Tag weights: standard ×1, collector ×2, premium ×4

**Scoring Engine**
- Weighted composite score (0–100) per tier
- Six adjustable sliders: Value for Money, Content Quantity, Exclusivity, Collector Appeal, Budget Fit, Delivery Penalty
- Content value score derived from weighted item sum + items-per-dollar ratio + variety
- Collector/Exclusivity sliders amplified by premium item presence in each tier
- Budget fit compares landed cost (price + delivery) against your budget

**Delivery Costs**
- Per-tier delivery field
- Shown as `+$X (Y%)` — percentage of product price
- `⚠ HIGH SHIP` flag when delivery is ≥15% of product price, or >1.5× average delivery across tiers with a minimum $5 gap
- Total column shows full landed cost, color-coded green/yellow/red

**Group Buy Mode**
- Set number of people splitting the pledge
- Set a per-person price target
- All items divided equally by group size
- Per-person column in results, with ✓ when target is met
- Budget fit scored against per-person target

**Tier Comparison**
- Side-by-side table: score, total items, weighted value, premium item counts, landed cost, ship %, cost per item
- Upgrade breakdown between consecutive tiers: extra cost, extra items, cost per new item, score delta, worth-it verdict

**Export**
- Downloads a plain `.txt` summary of the evaluation
- Includes all tiers with item lists and tags, scored results, best pick, and landed costs

**Save / Restore Session**
- Saves full session state to `localStorage`: campaign info, all tiers, item rows, tags, weights
- Restore brings everything back exactly as left — re-run evaluation to score

**Themes**
- Dark: phosphor green CRT terminal aesthetic
- Light: clean off-white with dark green accents
- Preference persists across sessions

---

## How to use

1. Open `index.html` in any browser — no server, no install, no internet required
2. Paste tier text into the **Tier Parser** box and click **⟳ Parse Tier**
3. Review the parsed item rows — fix quantities, cycle tags to `COLLECTOR` or `PREMIUM` where appropriate
4. Set your budget and delivery costs per tier
5. Adjust scoring sliders to match what matters to you
6. Click **[ EVALUATE PLEDGES ]**
7. Review scores, comparison table, and upgrade breakdown
8. Export or save session as needed

---

## Stack

Single self-contained `index.html` — zero dependencies, no build step, no package manager, no API keys.

- Vanilla JS (ES6)
- CSS custom properties for theming
- `localStorage` for session persistence
- `Blob` + `URL.createObjectURL` for export
- Fonts: Share Tech Mono + VT323 (Google Fonts, loaded on first open only)

Works fully offline after the first load.

---

## Compatibility

Any modern browser (Chrome, Firefox, Safari, Edge). No mobile optimization — designed for desktop use during campaign evaluation.

---

## Limitations

The item parser is regex/heuristic-based — it handles the most common crowdfunding and webshop formats well but unusual formatting may need manual correction via the item rows. The raw source string is always shown alongside parsed rows for exactly this reason.

---

## Daily Vibe Coded

This project is part of a **daily vibe coded** series — one working MVP per day (not really every day), shipped and never touched again. Built in a single session, polished to a usable state, then left as-is.

> Set it. Evaluate it. Move on.
