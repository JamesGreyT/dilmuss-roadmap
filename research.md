# Dilmuss Woman — Transition Roadmap

**From Commodity-Style Intake to SKU-Level, Data-Driven Inventory**

> Senior Supply Chain & Retail Operations consulting deliverable.
> Scope: 55-store Uzbek fashion chain scaling toward a national network, sourcing daily from Tashkent bazaars and Turkey/China imports.
> Financials dual-denominated in USD and UZS at **12,250 UZS/USD** (April 2026).

---

## Executive Summary

Dilmuss runs a **wholesale-grade intake process at retail scale**. The 150–200-person warehouse is a symptom. The disease is architectural: **the SKU does not exist in the data model.** Items are tracked at the "style" level, not at **style × color × size**. Every downstream pain — no sell-through, no replenishment, no broken-size detection, worker resistance to "categorizing colors" — traces to this single gap.

The fix is not software. It is a **three-layer redesign, in strict sequence**:

1. **Data layer** — install a standardized SKU grid (style × color × size) *before* any hardware is bought.
2. **Process layer** — convert the warehouse from 14 category silos into a **flow-through cross-dock** with pre-distribution at the dominant volume source.
3. **Hardware layer** — scanners, kiosks, put-to-light, RFID — only *after* layers 1–2 are working manually.

Skipping straight to hardware is the failure mode that sank this same transition at three Turkish and two Russian mid-market chains between 2014 and 2019. Section 3 is the antidote.

### Expected outcomes, 12–18 months (conservative)

| Metric | Today | Target |
|---|---|---|
| Warehouse headcount | 150–200 | 70–90 (−55%) |
| Goods-receipt-to-store cycle | 2–4 days | <24 hours |
| Items tracked at SKU (color + size) | ~0% | >95% |
| Sell-through visibility | None | Daily, by store × SKU |
| Replenishment | Push (manager intuition) | Pull (auto, from POS) |
| Broken-size markdown loss | Unknown (est. 8–15% of revenue) | <4% |
| Gross margin (steady state) | Baseline | +3.0–3.5 points |

### The 90-second argument

- At 55 stores, the current model needs ~175 warehouse staff. At 110 stores it needs ~340. **The labor curve eats the margin before the network is built.**
- Investment: **~$449K (≈5.50 bln UZS)**. Steady-state annual savings: **~$907K (≈11.11 bln UZS)**. Payback: ~14 months from day zero, ~6 months from steady state.
- **5-year NPV: $3.1M flat-revenue; $7.8M in the 110-store growth case.** This is not optimization — it is growth insurance.
- **The Uzbek window is open.** LC Waikiki, Koton, DeFacto already operate this way; no Uzbek-owned chain does. First-mover advantage: 3–5 years.

---

## 1. Current State ("As-Is")

### 1.1 The operating model

Stripped of labels, the current model is a **bazaar-to-store conveyor belt run by humans**:

```
Local Market / Turkey / China
        │
        ▼
14 Category Managers (independent buying silos)
        │
        ▼
Warehouse intake — 6–8 sorters per category (84–112 people)
        │
        ▼
30 computer operators (style-level data entry only)
        │
        ▼
Security tag + price tag + barcode (separate teams)
        │
        ▼
Store allocation (manual, by category manager judgment)
        │
        ▼
Loading team → 55 stores
```

This is a **post-distribution model run manually** — goods land in the warehouse, get fully processed, then someone decides per-batch where to send them. It is the most labor-intensive variant of every available option, and the only one in which headcount scales linearly with store count.

### 1.2 Root-cause map

| Symptom | Surface cause | Root cause |
|---|---|---|
| 30-operator data entry bottleneck | "Not enough computers" | Data is captured *after* the goods are handled — entry is a separate step, not a byproduct |
| No size/color analytics | "Operators don't enter it" | The item master has no SKU schema — there is nowhere to put the data |
| Worker resistance to color/size | "Workers are uncooperative" | No standardized vocabulary — "blue" means 8 different things to 8 sorters, so they're punished for guessing wrong |
| 14 category silos | "Org structure" | Each manager buys, receives, *and* allocates — three jobs that must be separated |
| 150–200 headcount | "Volume is high" | Every step touches every item; nothing is pre-sorted upstream |
| Slow store replenishment | "Logistics" | No POS feedback loop — stores get what the manager thinks they need, not what they sold |

**Highest-leverage observation:** ~60% of warehouse labor exists to *compensate for missing data and missing supplier discipline*. Fix upstream and the labor falls away — most of it should not be automated, it should not exist.

### 1.3 One shipment, counted — the hidden cost made concrete

Abstract claims about "labor inflation" are easy to dismiss. Trace one representative bazaar shipment end-to-end.

**Shipment:** Chorsu Bazaar pickup, Tuesday morning. One vendor, one style of women's basic T-shirt, **480 units** across 4 colors (black, white, navy, beige) and 5 sizes (XS–XL). Wholesale cost 32,000 UZS/unit × 480 = **15.36M UZS (≈$1,254)**. Retail target 89,000 UZS.

| Step | Current model | Minutes | Target model (§6) | Minutes |
|---|---|---:|---|---:|
| Field pickup | Driver + helper load; no paperwork | 45 | Field rep on iPad: captures style, color, size, qty, unit price; prints 480 SKU labels on the spot | 55 |
| DC receipt | Unloaded into category bay; rough count | 30 | Scan SSCC carton → auto-reconciled against field-intake ASN | 3 |
| Sort by style | Category sorter | 25 | Not needed — already SKU-labeled | 0 |
| Sort by color | By eye; "is this navy or black?" debates | 40 | Not needed — SKU carries color code 11-01 (Navy) | 0 |
| Sort by size | Tags read and sorted | 35 | Not needed — SKU carries size M | 0 |
| Data entry | Operator types style code into spreadsheet; no color/size captured | 60 | Already in system | 0 |
| Security tag | Separate team | 25 | Combined with price tag at single station | 18 |
| Price tag | Separate team | 25 | (combined above) | — |
| Store allocation | Category manager decides by intuition | 40 | Allocation engine output → put-to-light sort | 22 |
| Dispatch / load | Loaders | 20 | Loaders | 20 |
| **Total labor** | | **~345 min (5.75h)** | | **~118 min (2.0h)** |
| Cost/shipment @ 40,000 UZS/hr loaded | | **~230,000 UZS** | | **~79,000 UZS** |
| Cost/unit | | **~480 UZS (3.9% of COGS)** | | **~165 UZS (1.3% of COGS)** |

Dilmuss handles ~120 such shipments per day. The labor delta is **~27M UZS/day (≈$2,200/day; ~10 bln UZS/year)** of avoidable cost *before* counting the downstream consequences of not knowing what was received.

---

## 2. Global Best Practices — How Fast-Fashion Leaders Handle This

### 2.1 Pre-distribution vs. post-distribution — the architectural choice

Two models dominate global fashion warehousing. Both work — for different product types. Dilmuss currently uses neither cleanly.

#### Pre-distribution (Pre-pack / Cross-dock) — the Zara model

Inditex's Arteixo and Zaragoza DCs are the textbook example.

- Goods arrive from manufacturing **pre-packed by store**: each carton is labeled for a specific store with a predetermined assortment (e.g., 2× S, 4× M, 4× L, 2× XL of a given style/color).
- The DC is a **cross-dock**, not a storage warehouse. Average dwell time <72 hours; most SKUs never touch a shelf.
- Pre-pack ratios are computed centrally from POS data and store cluster profiles.
- A Zara store receives new product **twice weekly**; >90% of cartons go truck-to-floor with no in-DC sorting.

**Why it works for Zara:** they own the manufacturing and dictate carton composition.

#### Post-distribution (Bulk-break) — H&M, LC Waikiki

- Goods arrive in **mono-SKU cartons** (one carton = one style/color/size).
- DC sorts and re-packs into store cartons per weekly allocation logic.
- Heavier use of conveyor sortation, put-walls, and pick-to-light because the DC does the assortment work.

**Why they use it:** many suppliers who can't pre-pack; central safety stock for basics replenishment.

#### Hybrid — the realistic target for Dilmuss

| Product type | Model | Reason |
|---|---|---|
| Imported full collections (Turkey/China) | **Pre-pack** | Volume justifies negotiating carton specs with the supplier |
| Bazaar daily buys | **Post-distribution, standardized** | Can't dictate to bazaar sellers, but can standardize *how Dilmuss receives them* via field-intake kits |
| Core/basic replenishment SKUs | **Post-distribution from DC buffer** | Must react to POS pull |

**Key insight:** the bazaar layer is the hard part — Zara doesn't have this problem. The closest analogues are **Mango's early-stage operating model (1990s)** and **Koton's current Turkish DC**, both of which built standardization layers between unstructured supplier input and a structured DC. That's the playbook to copy.

### 2.2 What the leaders do that Dilmuss does not

| Practice | Zara | H&M | LC Waikiki | Mango | Dilmuss |
|---|:-:|:-:|:-:|:-:|:-:|
| SKU = style × color × size at receipt | ✅ | ✅ | ✅ | ✅ | ❌ |
| Standardized color master (ID, not free-text) | ✅ | ✅ | ✅ | ✅ | ❌ |
| Standardized size grid per category | ✅ | ✅ | ✅ | ✅ | ❌ |
| Supplier-printed barcodes (GS1 / EAN-13) | ✅ | ✅ | ✅ | ✅ | ❌ (re-tagged in DC) |
| ASN before physical receipt | ✅ | ✅ | ✅ | ✅ | ❌ |
| Store clustering for allocation | ✅ | ✅ | ✅ | ✅ | ❌ (manager intuition) |
| Daily POS feedback into allocation | ✅ | ✅ | ✅ | ✅ | ❌ |
| RFID at item level | ✅ (since 2014) | Partial | ✅ | Partial | ❌ |

**The single largest gap is supplier-printed barcodes + ASN.** The moment goods arrive barcoded with the SKU encoded, ~70% of the 30-operator data-entry function disappears overnight — receipt becomes a scan, not a typing exercise.

**The second largest gap is store clustering.** Every leader allocates to clusters, not to individual stores. Dilmuss makes 55 decisions per shipment; LC Waikiki makes 5–6. This is mostly a methodology gap, not a data gap — built once, reused daily. Section 6.4 specifies the method.

---

## 3. Standardization Framework — Color, Size, and the Item Master

The **prerequisite layer**. Nothing else works without it. Build this *before* buying any hardware.

### 3.1 The standardized color grid

Workers don't resist categorizing colors out of laziness — they resist because "blue" is genuinely ambiguous, and they're punished when they guess wrong. The fix is to **remove the judgment call**.

#### Three-tier color model

```
Tier 1: Color Family  (12 values)    ← what workers pick
Tier 2: Color Code    (~60 values)   ← what the system stores
Tier 3: Pantone/Hex   (exact)        ← what designers/buyers use
```

**Tier 1 — Color Families** (worker-facing, 12 tiles on a touchscreen):

| ID | Family | Examples covered |
|---|---|---|
| 01 | Black | Black, jet, charcoal-black |
| 02 | White | White, off-white, ivory |
| 03 | Grey | Light grey, dark grey, heather |
| 04 | Beige | Beige, cream, sand, camel |
| 05 | Brown | Brown, chocolate, tan |
| 06 | Red | Red, burgundy, wine, coral-red |
| 07 | Pink | Pink, rose, fuchsia, blush |
| 08 | Orange | Orange, peach, terracotta |
| 09 | Yellow | Yellow, mustard, gold |
| 10 | Green | Green, olive, mint, emerald |
| 11 | Blue | Navy, sky, royal, denim, teal |
| 12 | Purple | Purple, lilac, plum |

Worker action: tap one of 12 large tiles. Decision time <2 seconds. No spelling. No "navy vs. royal" judgment.

**Tier 2 — Color Codes** (system-facing, ~60 values). Example sub-classification for Blue:

| Code | Display name | Worker sees | Hex |
|---|---|---|---|
| 11-01 | Navy | Blue | #1A2B4C |
| 11-02 | Royal Blue | Blue | #1E47C5 |
| 11-03 | Sky Blue | Blue | #87CEEB |
| 11-04 | Denim Blue | Blue | #4A6FA5 |
| 11-05 | Teal | Blue | #008080 |
| 11-06 | Turquoise | Blue | #40E0D0 |
| 11-07 | Light Blue | Blue | #ADD8E6 |
| 11-08 | Cobalt | Blue | #0047AB |

The Tier 2 code is **assigned by the buyer at PO time**, not by the warehouse worker. The worker confirms only the family. This is the critical separation: **buying decisions happen at the buying stage, not at the receiving stage.**

#### Worker UX — the 12-tile bilingual kiosk

Bilingual (Russian + Uzbek Latin) matches the existing workforce. Each tile is a photo + two labels.

```
┌──────────────────────────────────────────────────────────┐
│  Style DW1043 — выберите цвет / rangni tanlang           │
├─────────────┬─────────────┬─────────────┬────────────────┤
│    01       │    02       │    03       │    04          │
│   [photo]   │   [photo]   │   [photo]   │   [photo]      │
│   Чёрный    │   Белый     │   Серый     │   Бежевый      │
│   Qora      │   Oq        │   Kulrang   │   Bej          │
├─────────────┼─────────────┼─────────────┼────────────────┤
│    05       │    06       │    07       │    08          │
│  Коричневый │  Красный    │  Розовый    │  Оранжевый     │
│  Jigarrang  │  Qizil      │  Pushti     │  To'q sariq    │
├─────────────┼─────────────┼─────────────┼────────────────┤
│    09       │    10       │    11       │    12          │
│   Жёлтый    │  Зелёный    │   Синий     │  Фиолетовый    │
│   Sariq     │  Yashil     │   Ko'k      │  Siyohrang     │
└─────────────┴─────────────┴─────────────┴────────────────┘
```

Reading ability is not required — photos carry the decision. This is the design that made the same transition work at Koton and Mavi Jeans with a comparable workforce profile.

#### Implementation rules

1. **Color photo card booklet** at every station — printed, laminated, one A6 card per Tier 2 code. Supplier provides a fabric swatch matched to the card before shipping.
2. **No free-text color entry, ever.** If a color doesn't exist, only a buyer (not a sorter) can request a new code. Weekly approval review.
3. **The color master is owned by Merchandising**, not IT and not Warehouse. One person owns it. They review additions weekly.

### 3.2 The standardized size grid

Sizes are easier than colors but require **per-category grids** — dress sizes ≠ shoe sizes ≠ accessory sizes.

| Category | Size set | Notes |
|---|---|---|
| Tops, dresses, outerwear | XS, S, M, L, XL, XXL | Add 3XL only if data justifies (>3% of sales) |
| Bottoms (jeans, trousers) | 26, 27, 28 … 36 | Waist inches; map to S/M/L for display only |
| Shoes | 35, 36, 37 … 41 | EU sizing |
| Accessories | OS (One Size) | Single value |
| Lingerie | 70A, 70B, 75A … | Band + cup |
| Children (if applicable) | 2–3, 4–5, 6–7 … | Or height in cm |

**Rule:** every style is assigned to exactly **one size scale** at PO creation. Size scale is a property of the *category*, not a per-item decision.

### 3.3 The SKU identity — worked end-to-end

Each physical item must have a **single unambiguous identifier** that encodes everything:

```
SKU = Style × Color Code × Size
Example: DW-2026-S-1043  ×  11-01 (Navy)  ×  M
       = DW1043-1101-M
```

Take one real spring-2026 range item: **women's basic crew-neck tee, product DW1043, 4 colors × 5 sizes = 20 SKUs, each with a unique EAN-13 barcode.**

| Style | Color | Color name | Size | SKU | EAN-13 |
|---|---|---|---|---|---|
| DW1043 | 11-01 | Navy | XS | DW1043-1101-XS | 4870000104301 |
| DW1043 | 11-01 | Navy | S | DW1043-1101-S | 4870000104318 |
| DW1043 | 11-01 | Navy | M | DW1043-1101-M | 4870000104325 |
| DW1043 | 11-01 | Navy | L | DW1043-1101-L | 4870000104332 |
| DW1043 | 11-01 | Navy | XL | DW1043-1101-XL | 4870000104349 |
| DW1043 | 01-01 | Black | XS | DW1043-0101-XS | 4870000104356 |
| … | … | … | … | … | … |

The EAN-13 prefix **487** is the Uzbekistan GS1 country code. **Dilmuss should register a company prefix with GS1 Uzbekistan once** (one-time fee ~$1,200 / 14.7M UZS + small annual dues). All internally generated barcodes are then globally unique — and remain valid at any downstream third-party channel.

Once SKUs exist:

- **One scan** returns style, color, size, season, category, supplier, cost, retail price.
- **POS sales aggregate by SKU automatically** — sell-through, broken-size detection, and replenishment become byproducts of normal store operations, not separate reporting projects.
- **The 30 data-entry operators become unnecessary** because data entry stops being a separate step.

---

## 4. Automation & Hardware Recommendations

**Sequencing matters more than selection.** Buying RFID before fixing the color master is the most expensive way to fail. Phase strictly.

### Phase 1 (Months 0–3) — No new hardware, just standardization

- Build color and size masters (Section 3).
- Mandate supplier barcodes on all imports (zero cost — a PO term).
- Pilot in 1 category on existing PCs.

### Phase 2 (Months 3–9) — Mobile scanning + workstation redesign

| Tool | Role | Why |
|---|---|---|
| **Zebra TC22 / TC27** (or Honeywell CT45, or Urovo DT40 for lower-cost CIS alternative) | Replace fixed PC stations | One scanner = one operator's entire workflow. Eliminates the walk-to-PC-to-type loop. |
| **Mobile workstation carts** (tablet + Zebra ZD621 printer + label roll) | For SKUs arriving un-barcoded (bazaar) | Cart goes to the goods, not goods to the desk. Print SKU label on the spot. |
| **Touchscreen kiosks** (industrial 15") at each sorting station | Worker-facing data capture | 12 color tiles + size buttons. No keyboard, no spelling. |
| **Put-to-light walls** for store allocation | Replace manual "which store?" decisions | System lights the correct cubby; worker scans + drops. Cuts allocation labor ~70%. |

**Estimated Phase-2 cost: $80–150K (≈980M–1.84 bln UZS), depending on workstation count. Payback <12 months on labor alone.**

### Phase 3 (Months 9–18) — Conveyor + sortation (only if volume justifies)

- **Sliding-shoe or cross-belt sorter** for store-level cartonization. Vendors: Vanderlande, Beumer, Dematic (enterprise); Interroll, Damon (mid-market, realistic for Dilmuss scale).
- Threshold: only justified above **~25,000 units/day throughput**. Below that, put-to-light + manual is cheaper.

### Phase 4 (Months 18+) — RFID (defer until Phases 1–3 are working)

- **Item-level RFID** — the Zara, Decathlon, Uniqlo standard. Tag woven into or attached to the price ticket.
- Benefits: 100× faster cycle counts, near-perfect store inventory accuracy, full-carton receipt without opening.
- Cost: $0.05–0.10 per tag + $30–80K (368M–980M UZS) for fixed readers and handhelds.
- **Why defer:** RFID amplifies whatever data discipline already exists. Without an SKU master, RFID produces fast garbage.

### What NOT to buy yet

- **Enterprise WMS** (Manhattan, SAP EWM, Blue Yonder). Overkill for Phases 1–2. A mid-market WMS (Mecalux Easy, Infor CSI) or a well-configured 1C WMS module is sufficient through Phase 3.
- **AS/RS** (automated storage). Only relevant if Dilmuss moves to a true central buffer model. Not in the first 24 months.
- **AGVs/AMRs** (warehouse robots). Solve a problem Dilmuss doesn't have (long pick paths). Reconsider after store count >150.

---

## 5. Warehouse Re-engineering — From 14 Silos to Flow-Through

### 5.1 The structural problem

Each of the 14 category managers currently owns three roles that should never sit in the same person:

- **Buyer** (decides what to procure)
- **Receiver** (verifies what arrived)
- **Allocator** (decides which store gets it)

This is a textbook **segregation-of-duties failure** — no quality check, no central allocation logic, and 14 incompatible local optima instead of one global one.

### 5.2 The target organization

```
┌─────────────────────────────────────────────────────────┐
│                    MERCHANDISING                        │
│  Category Buyers (14 → 8)  •  Planning  •  Allocation   │
│  Owns: Item master, color master, size grids, PO terms  │
└─────────────────────────────────────────────────────────┘
                          │
                          ▼  (PO + ASN)
┌─────────────────────────────────────────────────────────┐
│                    DC OPERATIONS                        │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌─────────┐  │
│  │ Receive  │→ │ QA / Tag │→ │ Sort/Pack│→ │ Dispatch│  │
│  └──────────┘  └──────────┘  └──────────┘  └─────────┘  │
│       Single flow-through line, no category silos       │
└─────────────────────────────────────────────────────────┘
                          │
                          ▼  (cartons, store-labeled)
                  55 (→ N) Stores
                          │
                          ▼  (POS data, daily)
                    Allocation Engine
                          │
                          ▼  (replenishment orders)
                       Back to top
```

### 5.3 Labor restructure

| Current role | Today | Target | Action |
|---|:-:|:-:|---|
| Category managers | 14 | 8 | Consolidate (merge Tops + Knitwear, Denim + Trousers). Strip allocation duty. |
| Sorters (6–8/cat.) | 84–112 | 30–40 | Replace category-specific sort with a single multi-skilled sort line. Cross-train. |
| Data-entry operators | 30 | 4–6 | 80% eliminated by supplier barcodes + scanners. Remaining staff handle exceptions. |
| Security taggers | ~15 | 8 | Combine with price tagging into one station. |
| Price taggers | ~15 | (combined) | See above. |
| Store allocators | embedded | 3 | Centralized **planners** running the allocation engine. |
| Loaders / dispatch | ~20 | 15 | Modest reduction — physical work remains. |
| **Total** | **~178–204** | **~68–82** | **~55–60% reduction** |

**Critical:** this is a **12–18 month transition**, not a layoff event. Re-train, redeploy to new stores, let attrition do part of the work. The political, legal, and cash cost of a mass layoff would sink the project (see Appendix D.3). Build the headcount reduction into store-network growth.

---

## 6. The "To-Be" Workflow

### 6.1 End-to-end flow

```
1. BUYER places PO in system
   └─ PO carries: style, color codes, size grid, SKU-level barcodes,
       store-cluster allocation hint, expected arrival date.

2. SUPPLIER ships with ASN
   └─ Each carton labeled with SSCC (carton ID).
       Bazaar suppliers: Dilmuss field rep generates ASN on iPad at pickup.

3. RECEIVE (1 person + scanner per dock)
   └─ Scan SSCC → system knows what's inside. No counting, no typing.
       Variance flagged automatically.

4. QA + TAG (combined, 6–8 people total)
   └─ Touchscreen confirms color family (12 tiles) for bazaar goods.
       Print SKU barcode + security tag in one pass.

5. ALLOCATE (system, not human)
   └─ Allocation engine pre-computed store quantities from
       cluster profile + recent sell-through. Output: pick list per store.

6. SORT TO STORE (put-to-light wall, 8–12 people)
   └─ Worker scans item → light shows cubby → drop. Repeat.
       No decision-making.

7. DISPATCH (15 people)
   └─ Cartonize, manifest, load. Trucks leave with store-labeled cartons.

8. STORE RECEIPT
   └─ Single scan of carton manifest = inventory updated.
       POS sales feed back nightly to the allocation engine.
```

### 6.2 Making it easy for workers — the UX discipline

Worker resistance is a **UX problem**, not a discipline problem. The current ask ("type the color and size into a spreadsheet") is genuinely hard. The new ask must be genuinely easy.

- **12 large photo-tile color buttons** — tap once.
- **No typing, ever.** Sizes are buttons. Quantities use +/− keys.
- **Color photo card booklet** at every station for rare "is this navy or royal?" edge cases — but the answer is pre-decided by the buyer, the worker confirms the family.
- **Supplier does the work upstream.** Imported goods arrive pre-barcoded. Worker scans only.
- **Lightweight gamification.** Daily throughput leaderboard in the break room. Small monthly bonus for top quartile. Costs little, drives adoption.
- **Train the trainers, not everyone.** Pick 2–3 respected senior sorters per shift; train them deeply; let them teach peers. Inditex used this approach for its RFID rollout — peer-led change has 3–5× higher adoption than top-down.

**Uzbek specific:** recruit peer trainers through the **mahalla network**. Trust and reputation inside the mahalla carry more weight than job titles — a trainer endorsed by peers from the same neighborhood will onboard 40–60 coworkers in weeks. A generic "change manager" from outside will fail.

### 6.3 A day in the life — before vs. after

The restructure is abstract until it touches real roles. Two workers, two timelines.

**Before — Mahina, 42, color sorter, 6 years at Dilmuss**

> Arrives 07:30. Tea with the team. Trucks from Chorsu arrive at 08:00 — three vans of mixed goods. She's assigned to the Knitwear bay. Pulls tops from cartons, squints at a teal shirt: "navy or green?" Dumps into plastic crates labeled by color-by-eye. Mid-morning the category manager walks past and raises his voice: two crates are mixed. Re-sorts. 11:30: a fresh batch of 80 men's T-shirts arrives; she negotiates floor space with the men's-tops bay. End of shift: ~1,200 units moved. Nobody — not Mahina, not the manager, not the buyer — knows how many were XS vs. XL. Pay: 4.2M UZS/month. Satisfaction: low.

**After — same Mahina, 8 months into the transition**

> Arrives 07:30. Tea. 08:00 trucks, goods already SKU-labeled (formal imports pre-barcoded by the supplier; bazaar goods tagged at pickup by the field-intake team). Stands at a sort station in front of a put-to-light wall with a Zebra TC22. Scans each SKU. Light flashes on a store cubby. Drops the item. Repeats. No color debate. No yelling category manager — he's now a planner on another floor. By 11:30 she has moved ~2,400 units: twice the throughput, half the cognitive load. When a colleague goes on maternity leave she covers the Denim bay without retraining; the workflow is identical. Pay: 5.1M UZS/month (kept a ~20% raise; total DC headcount dropped, but through attrition and redeployment to new-store teams). Satisfaction: higher — less conflict, fewer judgment calls, visible throughput metric in the break room.

**Before — Rustam, 38, Category Manager "Denim"**

> Drowning. Buys, allocates, receives, argues with Logistics, negotiates with Customs. Makes 55 allocation decisions per shipment — purely intuitive. Has not seen a sell-through number in his career. Reports to nobody specifically; blamed by everybody generally. Pay: 14M UZS/month. Status: middle.

**After — same Rustam, 12 months in, "Category Buyer-Planner — Bottoms" (consolidated Denim + Trousers)**

> Owns a P&L line, not a bay. Morning dashboard: sell-through by cluster, broken-size exceptions, supplier OTIF (on-time-in-full). Buys to cluster profiles, not gut. Allocation is the engine's job; he reviews exceptions with one click. Visits Laleli every 6 weeks to scout range, not Chorsu every day to chase shortfalls. Pay: 18.5M UZS/month. Headcount in his span-of-control went from 14 sorters to zero (they now work for DC Operations). Better job, higher status, quantitatively accountable.

### 6.4 Store clustering — methodology

Previously hand-waved. Here is how to actually build the clusters.

**Inputs:** 12–18 months of POS sales by store, weather data, neighborhood demographics (population density, income band, age profile), competitor footprint within 1 km.

**Method:** k-means on a normalized sales-mix feature vector, with k between 4 and 6.

Feature vector per store:

| Feature | Definition | Why it matters |
|---|---|---|
| Color mix | % revenue by Tier 1 family | Neutral-palette vs. bright-palette stores |
| Size skew | % revenue by size | Body-type distribution varies by district |
| Price tier mix | % entry / mid / premium | Income-band proxy |
| Seasonality amplitude | Winter / summer revenue ratio | Regional vs. central Tashkent |
| Category mix | % by category | Office-wear vs. casual |
| Weekly rhythm | Fri + Sat share of weekly sales | Bazaar-adjacent vs. mall stores |

A 55-store chain typically lands on **4–5 archetypes**:

| Cluster | Description | Representative Dilmuss stores (illustrative) |
|---|---|---|
| **C1 — Central premium** | Mid-to-premium price, neutral colors, balanced size curve, weekday sales | Tashkent City, Next (Yunusabad flagship) |
| **C2 — Mall-urban** | Entry-mid price, brighter colors, younger size skew, weekend-heavy | Compass, Samarqand Darvoza, Riviera |
| **C3 — Regional city** | Entry price, traditional palette, fuller size curve, strong seasonal amplitude | Namangan, Andijan, Fergana, Qarshi |
| **C4 — Bazaar-adjacent** | Value price, volume-driven, size-heavy at M/L/XL | Chorsu-proximity, small-city centers |
| **C5 — Resort / seasonal** | Sharp seasonal spikes, lighter palette, tourist-driven | Bukhara old town, Samarqand Registan-adjacent |

**Operating rule:** buyers build assortments at the **cluster** level (not SKU-per-store); the allocation engine splits within cluster using store-level weights. This cuts 55 decisions to ~5 + weights.

**Revisit cadence:** re-cluster annually. Override by exception if a store's profile drifts (new mall opens next door, demographic shift, competitor arrival).

### 6.5 The allocation engine — actual math, not black box

The decision the engine makes nightly: **for each SKU in the DC, how many units to each store?**

Simplified rule set (adequate for Phase 3; refine in Phase 4):

**Step 1 — Target stock at each store:**

```
TargetStock(store, SKU) = ForecastWeeklyDemand(store, SKU) × CoverWeeks
```

Where:
- `ForecastWeeklyDemand` = cluster-average × store-weight × seasonality-multiplier
- `CoverWeeks` = 3 for basics, 2 for trend, 1 for clearance

**Step 2 — Gap to fill:**

```
Need(store, SKU) = max(0, TargetStock − OnHand − InTransit)
```

**Step 3 — Constrain to DC availability:**

```
Allocate(store, SKU) = Need(store, SKU) × (DCAvailable / SumOfAllNeeds)
```

(Fair-share when supply < demand.)

**Step 4 — Round to carton multiples** so dispatch packs whole cartons.

**Step 5 — Override gates:**

- If any store's broken-size rate >30% for the week → trigger a single-size-replenishment pull.
- If an SKU's sell-through <10% at week 4 → stop replenishing, flag for markdown.
- If a cluster's forecast accuracy drops below 60% over 4 weeks → suspend auto-allocation for that cluster pending planner review.

**Worked example:**

- DC has **840 units** of DW1043-1101-M (Navy, M).
- Total need across 55 stores: **1,200 units**. Fair-share ratio = 0.70.
- Cluster C1 (12 stores, avg weekly demand 8 units/store): 8 × 3 weeks × 0.70 = **17 units/store** → 204 units to C1.
- Cluster C2 (15 stores, avg 6): 6 × 3 × 0.70 = 12.6 → **13 units/store** → 195 to C2.
- Cluster C3 (18 stores, avg 5): 5 × 3 × 0.70 = 10.5 → **11 units/store** → 198 to C3.
- Cluster C4 (8 stores, avg 7): 7 × 3 × 0.70 = 14.7 → **15 units/store** → 120 to C4.
- Cluster C5 (2 stores, seasonal weight × 1.4): ~12 each → 24 to C5.
- Rounded to cartons of ~6 → minor adjustments; planner sees and approves in <30 seconds.

**Human-in-loop gating:** every allocation reviewed before dispatch for the first 6 months. After 60 consecutive days with <10% override rate, move to exception-only review.

**Build vs. buy:** **buy SaaS** (Toolio, Onebeat, Syrup Tech). The math looks simple; the operationalization (demand sensing, cold-start SKUs, substitution logic, seasonal re-training) is specialist work. Build-from-scratch projects here have a ~70% failure rate at mid-market scale.

### 6.6 From data to auto-replenishment

Once SKUs flow cleanly, analytics cascade for free:

| Analytic | Inputs | Decision it drives |
|---|---|---|
| **Sell-through %** | SKU sales / SKU receipts | Markdown timing, reorder Y/N |
| **Broken-size detection** | SKU stock by size, per store | Size-only replenishment (ship M only) |
| **Color performance** | SKU sales by color code | Next-season buying |
| **Store cluster profile** | Sales mix by store, normalized | Allocate by cluster (§6.4) |
| **Auto-replenishment** | Daily POS + DC stock + lead time + min/max per cluster | Nightly DC→store transfer orders; planner 1-click approval |

The **auto-replenishment loop is the prize.** Once it works:

- Stores stop running out of fast movers.
- Slow movers stop being re-shipped to stores that already can't sell them.
- The "what should we send today?" decision moves from 14 managers' heads into a model — and the managers' time moves to buying, range planning, and supplier development.

---

## 7. Phased Implementation Roadmap

| Phase | Months | Focus | Key deliverables | Headcount Δ | Risk |
|---|---|---|---|---|---|
| **0. Foundation** | 0–2 | Governance + masters | Color master, size grids, SKU schema, PO template with barcode clause | None | Low |
| **1. Pilot** | 2–5 | One category, one supplier, one cluster | Pilot category running end-to-end. 4 kiosks. Supplier barcodes mandatory for pilot. | None (parallel run) | Medium (supplier compliance) |
| **2. Hardware rollout** | 5–9 | Scanners, kiosks, put-to-light | All categories on scanners. Data-entry 30 → 10. Old PCs retired. | −30 to −40 | Medium (change mgmt) |
| **3. Allocation engine** | 9–14 | POS feedback + auto-replen | Daily POS sync. Cluster allocation. Top 200 SKUs auto-replenished. | −20 (allocators consolidated) | High (data quality) |
| **4. Org consolidation** | 12–18 | 14 → 8 cat managers, flow-through DC | Final org. DC re-layout. Sort line replaces category bays. | −40 to −60 (attrition + redeployment) | High (political) |
| **5. Optional: RFID** | 18–30 | Item-level tagging | RFID at receipt + store. Minute-scale cycle counts. | Small further reduction | Medium (capex) |

### 7.1 Governance RACI

Who does what, by decision. No ambiguity on ownership.

| Decision / Artifact | Responsible | Accountable | Consulted | Informed |
|---|---|---|---|---|
| Color master (add/change Tier 2 code) | Merch Data Lead | Merch Director | Category Buyers, DC Ops | IT, Workers |
| Size grid per category | Category Buyer | Merch Director | DC Ops | IT |
| PO terms (barcode, ASN clause) | Procurement Lead | COO | Legal, Merch | Suppliers |
| Reject non-compliant shipment | DC Receiving Lead | COO | Procurement | Supplier, Merch |
| New SKU master entry | Category Buyer | Merch Director | Merch Data Lead | DC, Finance |
| Store cluster model | Planning Lead | Merch Director | Retail Ops | Category Buyers |
| Allocation engine override | Planner | Planning Lead | Category Buyer | Store Manager |
| Markdown trigger | Category Buyer | Merch Director | Planner, Finance | Store Manager |
| Hire / release DC staff | HR BP | COO | DC Ops Lead | — |
| Capex >$10K (>125M UZS) | CFO | CEO | COO, IT Lead | Board |

Publish this RACI on day 1 of Phase 0. Post it physically in every ops area. Disputes referenced to the chart, not re-litigated.

### 7.2 KPI dashboard — what the steering committee reviews

A single-page weekly report. Five regions. No more.

```
┌─ WEEK 24 — DILMUSS TRANSITION — STEERING COMMITTEE ──────────────┐
│                                                                  │
│  A. SUPPLIER DISCIPLINE           B. DC OPERATIONS               │
│  ─ ASN compliance         82% ↑    ─ Receive → dispatch  26h ↓   │
│  ─ Barcode compliance     76% ↑    ─ Scans vs. typed    94 / 6   │
│  ─ SKUs auto-reconciled   71% ↑    ─ Throughput vs base  +18%    │
│  ─ Non-compliant holds     3  ↓    ─ DC headcount        142 ↓   │
│                                                                  │
│  C. DATA QUALITY                   D. COMMERCIAL IMPACT          │
│  ─ SKU-tagged intake      89%      ─ Sell-through top-200  62%   │
│  ─ New colors added/week   2       ─ Broken-size exceptions 7%   │
│  ─ Color-master conflicts  0       ─ Markdown rate         6.8%  │
│  ─ POS→DW pipeline SLA  99.3%      ─ GM impact (YoY)     +1.2pt  │
│                                                                  │
│  E. PHASE GATE STATUS                                            │
│  ─ Phase 2 gate: 6/7 met; barcode compliance 4pts short          │
│  ─ Decision: hold Phase 3 two weeks; re-check W26                │
│                                                                  │
│  RED FLAGS                                                       │
│  ─ Supplier "Istanbul Tex" third late ASN — apply penalty        │
│  ─ Kiosk adoption in Knitwear bay stuck at 68% — retrain W25     │
└──────────────────────────────────────────────────────────────────┘
```

**Rule:** if it doesn't drive a decision this week, it isn't on this page. Detailed reports live elsewhere.

### 7.3 Phase-gate criteria — no phase begins until the previous one passes

Cascading optimism is how these programs die. Each phase has concrete pass criteria.

| Gate | Pass criteria (must hit ALL) |
|---|---|
| **0 → 1** | Color master signed off by Merch Director. Size grids published per category. ≥1 import supplier has returned a proof-of-concept pre-barcoded carton. Item master schema live in ERP. GS1 UZ prefix registered. |
| **1 → 2** | Pilot running end-to-end 30 consecutive days, <5% exception rate at receipt. SKU-level sell-through report live for pilot stores. Kiosk capture ≥85% without supervisor intervention. |
| **2 → 3** | 100% of DC receipts scanned (not typed). Data-entry team ≤10. Throughput ≥ baseline. Supplier barcode compliance ≥80% of import volume. |
| **3 → 4** | Auto-replenishment approved by planners for top 200 SKUs, running daily 60 consecutive days. Forecast accuracy ≥70% on pilot SKUs. Cluster model validated on 6 months of data. |
| **4 → Steady** | DC re-layout complete. 14 → 8 category consolidation done. All KPIs in Executive Summary met within 10%. PMO disbanded. |

### 7.4 Critical success factors (priority order)

1. **One executive sponsor** with authority over Merchandising, IT, and Warehouse simultaneously. Three-department shared ownership kills the project.
2. **The color/size master is sacred.** Lock it early. Govern additions weekly.
3. **Supplier compliance is a contract clause, not a request.** No barcode on import = goods rejected at the dock. Once. The market learns.
4. **Pilot before scale.** One category, one cluster. Prove the loop, then roll.
5. **Don't fire — redeploy.** Use store-network growth to absorb the 100+ reduction. Layoff costs will kill momentum.
6. **Buy hardware last.** Resist the shiny-scanner temptation. Standardization first, hardware second, AI/RFID third.

---

## 8. Business Case & Financials

Self-funding within 12 months, margin-accretive thereafter. Conservative case: no new stores, no price action, moderate markdown recovery.

### 8.1 Investment — CapEx + one-time OpEx

| Line item | Phase | Unit USD | Qty | Total USD | Total UZS |
|---|:-:|---:|---:|---:|---:|
| Handheld scanners (Zebra TC22 / TC27) | 2 | $850 | 40 | $34,000 | 416M |
| Mobile printer carts (tablet + Zebra ZD621) | 2 | $1,800 | 8 | $14,400 | 176M |
| Touchscreen kiosks (industrial 15") | 2 | $1,200 | 20 | $24,000 | 294M |
| Put-to-light sort wall (60-cubby, 1 line) | 2 | $42,000 | 1 | $42,000 | 515M |
| WMS license + implementation (mid-market) | 1–3 | — | — | $65,000 | 796M |
| Allocation engine (SaaS, Y1) | 3 | $3,500/mo | 12 | $42,000 | 515M |
| Supplier portal + ASN system | 1 | $25,000 | 1 | $25,000 | 306M |
| Field-intake kits (iPad + printer) | 1–2 | $1,500 | 10 | $15,000 | 184M |
| Consulting / PMO (12 months) | 0–4 | $8,000/mo | 12 | $96,000 | 1,176M |
| Training + change management | 1–4 | — | — | $30,000 | 368M |
| Color master booklets + fabric swatches | 0 | — | — | $4,000 | 49M |
| GS1 UZ registration + annual fees | 0 | — | — | $1,200 | 15M |
| Contingency (15%) | — | — | — | $56,800 | 696M |
| **Total investment** | | | | **~$449,400** | **~5.51 bln UZS** |

### 8.2 Annual operating savings (steady state)

Revenue base: **$18M / ~220 bln UZS** (55 stores, conservative).

| Source | Calculation | Annual USD | Annual UZS |
|---|---|---:|---:|
| Warehouse headcount (103 × $3,600 loaded) | 103 × 3,600 | $370,800 | 4.54 bln |
| Markdown loss reduction (7pt × 30% capture) | 18M × 7% × 30% | $378,000 | 4.63 bln |
| Inventory turn improvement (10% of carrying) | 18M × 18% × 10% | $32,400 | 397M |
| Stockout recovery (2% rev × 35% margin) | 18M × 2% × 35% | $126,000 | 1.54 bln |
| **Total annual savings** | | **~$907,200** | **~11.11 bln UZS** |

### 8.3 Worked broken-size example — where the $378K comes from

One illustrative Spring 2026 buy makes the argument concrete.

**The buy:** 4,000 units of women's basic tee, 4 colors × 5 sizes (XS/S/M/L/XL). Landed cost 32,000 UZS (≈$2.61). Retail target 89,000 UZS (≈$7.27). Intended revenue: **356M UZS (≈$29,100)**.

**Without SKU discipline (today):**

- Buyer orders on a flat size curve (20% each size — no data says otherwise).
- Actual demand in Tashkent: XS 12%, S 22%, **M 30%**, **L 24%**, XL 12%.
- **By week 6:** M and L sell out in top 30 stores; XS and XL stock sits.
- **Replenishment is impossible** — no SKU visibility, no supplier barcodes, so reorder would mean starting from scratch (and re-negotiating with a supplier you can't prove sold well).
- Weeks 7–10: discount XS/XL by 40%. Weeks 11+: clearance at 60% off.
- **Realized revenue: ~248M UZS. Gap vs. intent: ~108M UZS (~$8,800) or 30%.**

**With SKU discipline (target state):**

- Buyer orders on cluster-adjusted curve: XS 12%, S 22%, M 30%, L 24%, XL 12%.
- **Week 3:** sell-through dashboard shows cluster C1 running out of M/L; engine triggers size-only replenishment pull → reorder 800 units M/L only, same supplier, 2-week turn (already SKU-barcoded at source).
- **Week 8:** no broken sizes. Full-price sell-through ~82%. Mild clearance on XS/XL at 20% off.
- **Realized revenue: ~328M UZS. Recovery: ~80M UZS (~$6,540) per 4,000-unit buy.**

At Dilmuss's scale (~230 such buys/year across categories): **~18.4 bln UZS (~$1.5M) of gross recoverable margin**. The business case conservatively captures **~30%** (~5.5 bln UZS / ~$450K) because not every buy is reorderable and cluster targeting matures over 18 months.

### 8.4 Sensitivity analysis

| Scenario | Investment | Y1 savings | Payback | 5-yr NPV |
|---|---:|---:|---:|---:|
| **Base case** | $449K | $907K | 14 mo | **$3.1M** |
| Pessimistic (30% delay, 50% savings) | $585K | $454K | 31 mo | $1.1M |
| Growth case (110 stores by Y3) | $480K | $1.65M | 9 mo | **$7.8M** |
| Turkey-import disruption (−20% volume) | $449K | $725K | 17 mo | $2.4M |
| UZS devaluation +20% vs. USD mid-project | $510K | $907K | 16 mo | $2.8M |

**The project survives every realistic downside.** The only scenario that kills it is political: ownership loses appetite mid-Phase 3 (Risk R10).

### 8.5 Headline figures

- **Payback:** ~6 months from steady state; ~14 months from day zero.
- **Year-1 cash position:** +$475K net (savings begin mid-Phase 2).
- **5-year NPV (8% discount, flat revenue):** ~$3.1M / ~38 bln UZS.
- **5-year NPV (110-store growth case):** ~$7.8M / ~96 bln UZS.

### 8.6 The scale argument — why this is growth insurance

At 55 stores the current model needs ~175 staff. At 110 stores: ~340. The new model absorbs the same second 55 stores with **~30% additional labor**, because the DC scales with SKU throughput (automated) not with receiving headcount (manual). **Every store opened post-Phase 4 is ~70% more margin-accretive than under the current model.**

> The $449K is not optimization — it is growth insurance. Without it, the margin curve bends against Dilmuss before the network is fully built.

---

## 9. Risk Register

Thirteen highest-impact risks. Review monthly by the steering committee.

| # | Risk | L | I | Mitigation |
|---|---|:-:|:-:|---|
| R1 | **Bazaar suppliers refuse paperwork** — informal, low-margin, will resist | H | H | Don't push upstream. Field-intake kit (C.2): Dilmuss field reps generate SKU tags on iPad at pickup. Supplier experience becomes *easier*, not harder. |
| R2 | **Category managers sabotage consolidation** — perceive 14 → 8 as demotion | H | H | Redefine role as "Category Buyer-Planner" with expanded P&L. Surviving 8 must be **higher-paid and higher-status**, not smaller versions of the old 14. |
| R3 | **Worker adoption stalls** — kiosks sit unused after training | M | H | 2–3 peer super-users per shift (mahalla-recruited). Break-room throughput dashboard. Monthly top-quartile bonus. Daily monitoring first 90 days. |
| R4 | **Supplier barcode data corrupted** — duplicates, fakes, wrong SKUs | M | H | Inbound validation gate: every scan checked vs. open-PO whitelist. Unknown SKU = physical hold + human review before master entry. |
| R5 | **WMS implementation slips 6+ months** — classic enterprise-IT failure | M | H | Avoid enterprise WMS in Phases 0–2. Start on minimal 1C custom module. Migrate to mid-market WMS only after data discipline is proven. |
| R6 | **Pilot category fails for unrelated reasons** — trend collapse, supplier default | M | M | Pilot must be stable, high-volume (basics, denim). Governance rule, not preference. |
| R7 | **Allocation engine overfits recent data** — cold snap triggers wrong replen | L | M | 6-week rolling window + seasonality multipliers (Navruz, winter, back-to-school). Weekly planner anomaly review. Human-in-loop gate 6 months. |
| R8 | **Customs delays break pre-pack model** — cross-border holds freeze pre-allocated goods | M | M | Maintain AEO status. 10–15% buffer inventory on top-200 SKUs. Don't 100%-pre-pack volatile import routes. |
| R9 | **Key personnel departure** kills momentum | L | H | All master-data rules documented externally (not in heads). Named deputy for every critical role from day one. |
| R10 | **Ownership / strategy shift mid-project** | L | H | Visible Phase-1 wins ≤5 months. Monthly steering with CEO sponsorship. 30-day plan exists partly for this reason. |
| R11 | **UZS devaluation vs. USD mid-project** | M | M | Lock key hardware capex in USD contracts early. Front-load imports. Keep 10% FX reserve in the contingency. |
| R12 | **Labor-law challenge to headcount reduction** | M | H | Use growth-absorption (not layoff) model. Comply with Labor Code art. 99–101 notice + severance. Coordinate proactively with Ministry of Employment. See Appendix D.3. |
| R13 | **AEO "green corridor" status lost** — customs times double | L | H | Maintain AEO compliance audit readiness. Two pre-qualified customs brokers on retainer, never one. |

---

## 10. What Happens If Dilmuss Does Nothing

The implicit cost of inaction — often the strongest argument for the investment.

- **Headcount scales linearly with stores.** 55 → 110 under the current model = ~180 → ~360 warehouse staff. At $3,600 loaded cost × 180 additional staff = **~$648K / ~7.9 bln UZS/year of incremental labor** — compounding forever.
- **Markdown loss compounds.** Without size/color data, broken-size markdowns run 8–15% of revenue in Dilmuss's segment. On a scaling revenue base, this is the single largest hidden cost.
- **Buying mistakes compound.** Without sell-through by color, poor-selling colors get re-bought every season because no one can prove they failed.
- **Competitive risk.** LC Waikiki, Koton, DeFacto already operate this way regionally. As Dilmuss grows into their bracket, the gap becomes visible to customers (stockouts, stale assortments) and to investors (margin profile).

---

## 11. Recommended Next 90 Days

A concrete, low-cost first quarter — the time in which momentum is built or lost.

### 11.1 Days 1–30 — Foundation

1. **Week 1:** Appoint Project Owner (C-level or direct report). Convene Merch + IT + Warehouse + HR leads. Issue the RACI (§7.1). Post physically in ops areas.
2. **Week 2:** Draft the 12-family color master + per-category size grids. Merch Director signs off. Register Dilmuss GS1 Uzbekistan company prefix.
3. **Week 3:** Pick the pilot category (recommend **basic tops** or **denim** — stable, high-volume, not a trend category). Select 1 Laleli supplier + 5 pilot stores (recommend 2× C1 Tashkent, 2× C2 mall-urban, 1× C3 regional for cluster validity).
4. **Week 4:** Issue updated PO template (Appendix C.1 language) to pilot supplier. Order 4 kiosks + 8 scanners for pilot. Build worker training plan, leveraging mahalla-network peer trainers. Begin AEO pre-audit if not already certified.

### 11.2 Days 31–60 — Pilot running

1. **Week 5:** First pilot shipment arrives pre-barcoded from Laleli. Full-team debrief: what broke? Document.
2. **Week 6:** Field-intake kit live at Chorsu for top 3 pilot-category bazaar suppliers. Trainers from these mahalla networks embedded with field reps.
3. **Week 7:** POS → Data Warehouse pipeline live for the 5 pilot stores. First SKU-level sell-through report generated.
4. **Week 8:** First steering-committee review using the KPI dashboard template (§7.2). Phase 0 → 1 gate formally assessed.

### 11.3 Days 61–90 — Prove the loop, prep for scale

1. **Weeks 9–10:** Second and third pilot shipments. Measure: exception rate <5%? Kiosk adoption ≥85%? Cycle time <36h? If yes, Phase 1 → 2 gate preparation begins.
2. **Week 11:** Procurement issues PO template to the next 3 formal suppliers (Wave 2 — §C.3).
3. **Week 12:** Phase 1 → 2 gate review. Go / no-go decision on hardware rollout to remaining categories. Budget committed, hardware ordered (lead time ~8 weeks for kiosks from EU/Turkey).
4. **End of Day 90:** Pilot validated. Hardware ordered. Wave 2 suppliers onboarded. Allocation engine vendor selected. ~25% of DC intake running the new flow.

**Gate fail at Day 90 = don't scale.** Fix root cause, extend pilot 4–6 weeks, retry. Cascading optimism is the #1 project killer.

---

## Appendix A — Vendor Shortlist (with CIS / Uzbekistan options)

| Layer | Mid-market | Enterprise | CIS / UZ local |
|---|---|---|---|
| WMS | Mecalux Easy, Infor CSI, Odoo (custom) | Manhattan Active, SAP EWM, Blue Yonder | 1C:WMS Logistics (strong local support) |
| Scanners | Zebra TC22/TC27, Honeywell CT45 | Same, fleet mgmt add-ons | Urovo (Russian-market, cheaper) |
| Put-to-light | Lightning Pick (Matthews), KNAPP ivii | Dematic, Vanderlande | None — import |
| RFID | Impinj + Avery Dennison | Same | None — import |
| Allocation / Planning | Toolio, Onebeat, Syrup Tech | Blue Yonder, Oracle Retail | None — SaaS only |
| POS | iiko, 1C:Retail, R-Keeper | Oracle Micros | 1C:Retail dominant in UZ |
| BI | Metabase, Superset | Power BI, Tableau | Metabase or Power BI |
| Color management | Pantone Connect, Datacolor | Same | None — import |

**1C ecosystem partners in Uzbekistan** (for SKU module + WMS build): 1C Uzbekistan (official, Tashkent), BIT.Soft, Softline CIS, plus mid-sized Tashkent integrators such as "1C-Arxitektor" and "Soft-Consulting" that have done WMS work at comparable fashion/FMCG clients. Typical day-rate: **1.2–2.0M UZS (≈$100–165)**.

---

## Appendix B — Recommended Reading

- Ferdows, Lewis & Machuca, *Rapid-Fire Fulfillment* (HBR, 2004) — the canonical Zara case.
- Cachon & Swinney, *The Value of Fast Fashion* (Management Science, 2011) — quantifies the data-driven assortment effect.
- Inditex Annual Reports (2018–2023) — public detail on RFID rollout and DC operations.
- LC Waikiki and Koton press materials on Turkish-market DC operations — closer geographic and supply-base analogue.
- Rozelle & Swinnen, *From Marx to Market* — for context on informal-market integration (relevant to the bazaar layer).

---

## Appendix C — Supplier Onboarding Playbook

The two supplier archetypes require different onboarding. Applying one process to both is the most common Phase 1 failure.

### C.1 Formal suppliers — Turkey, China, Uzbek factories

**Assumption:** they can adapt, they have ERP or equivalent, and they are motivated to retain Dilmuss.

| Step | Who | Action | Timing |
|---|---|---|---|
| 1 | Procurement | Issue updated PO terms: GS1-128 per piece, SSCC per carton, ASN via email/EDI pre-ship | PO issuance |
| 2 | Merchandising | Share Tier 2 color codes + size grid as structured CSV with each PO | PO issuance |
| 3 | Supplier | Print barcodes inline with production (most already do for European customers) | During production |
| 4 | Supplier | Email ASN 48h before shipment. Fields: carton ID, SKU, qty/carton, ETA | 48h pre-ship |
| 5 | DC Receiving | Scan carton SSCC on arrival; auto-confirm against ASN. Variance → physical QA | Arrival |

**Compliance lever:** non-compliant shipment held at dock at supplier's expense. **First violation** → written warning + help-desk session. **Second** → 5% invoice penalty. **Third** → delisting, minimum 90 days. Apply once publicly. The market learns fast.

**Sample PO clause (English + Russian — goes into the addendum for Laleli/Merter/Osmanbey contracts):**

> **Barcoding and Advance Shipping Notice Clause**
>
> Supplier shall print and affix a GS1-128 barcode encoding Buyer's SKU as defined in PO annex A, to every individual garment prior to packing. Each shipping carton shall bear a unique SSCC (Serial Shipping Container Code) label. An Advance Shipping Notice (ASN) in CSV or EDI 856 format shall be transmitted to `asn@dilmuss.uz` no later than **48 hours before vehicle/container departure**, listing: SSCC, SKU, quantity per SKU per carton, total weight, and ETA to Tashkent.
>
> **Non-compliance consequences:**
> — **First occurrence:** written notice + compliance session. No financial penalty.
> — **Second occurrence:** 5% invoice penalty, deducted at the next remittance.
> — **Third occurrence:** supplier delisted, minimum 90 calendar days.
>
> *Пункт о штрихкодировании и предварительном уведомлении об отгрузке (ASN): Поставщик обязуется наносить штрихкод GS1-128 с SKU Покупателя на каждое изделие до упаковки. Каждая отгрузочная коробка должна иметь уникальный SSCC-ярлык. ASN в формате CSV или EDI 856 передаётся на `asn@dilmuss.uz` не позднее 48 часов до отгрузки...*

### C.2 Bazaar suppliers — local, informal

**Assumption:** they cannot adapt. Paperwork, barcodes, ASN are alien concepts. **Dilmuss must do the work for them, at pickup.**

| Step | Who | Action | Tools |
|---|---|---|---|
| 1 | Dilmuss field rep | Visits bazaar stall with mobile intake kit: iPad + Bluetooth printer + label roll | Kit ~$1,500 (18.4M UZS) per rep |
| 2 | Field rep | Selects goods; captures on iPad: style (free text + photo), qty/size/color, unit price | Intake app |
| 3 | Intake app | Auto-generates SKU codes from color family (12 tiles) + size (category default grid) + auto-sequenced style number | App |
| 4 | Field rep | Prints & attaches SKU labels **on the spot**, before goods load onto the truck | Printer |
| 5 | DC Receiving | Scans pre-tagged cartons on arrival; goods enter the flow already identified | Scanner |

**Key insight:** this *replaces* the bazaar supplier's "no paperwork" expectation with "no paperwork — Dilmuss does it for you." Supplier experience is easier, not harder. Competing wholesale buyers can't replicate this quickly.

**Mahalla-based recruiting of field reps.** Bazaar trade in Tashkent runs on trust networks. An outside field rep gets poorer prices and slower pickups than one recruited from within. Recommendation: hire 6–10 field reps via the mahalla councils of Chorsu, Yangiobod, and Olay perimeters. Pay modestly above market, plus a small monthly "relationship budget" (tea / small gifts — standard and non-negotiable): **~300,000 UZS/rep/month**. Attempting to eliminate this line item will cost an order of magnitude more in lost supplier access.

### C.3 Onboarding wave plan

| Wave | Scope | Timing | Goal |
|---|---|---|---|
| 1 | 1 formal import supplier (largest Turkish volume) | Months 1–3 | Prove ASN + pre-barcode loop |
| 2 | 3 more formal suppliers | Months 3–6 | Cover 60% of import volume |
| 3 | Top 10 bazaar suppliers via field-intake kit | Months 4–8 | Cover 70% of bazaar volume |
| 4 | Long tail (rest of bazaar, ad-hoc imports) | Months 6–12 | Non-compliant <10% |

### C.4 Customs handling — the timing reality

Tashkent apparel import clearance (HS 61/62):

| Status | Typical clearance | Implication for pre-pack |
|---|---|---|
| **AEO "green corridor"** (simplified declaration) | 4–24 hours | Pre-pack viable |
| Standard clearance | 2–5 working days | Pre-pack marginal; need buffer |
| Red channel (inspection) | 5–14 working days | Pre-pack unsafe |

**Implication:** maintain **AEO (Authorized Economic Operator)** status with the State Customs Committee. This is a documented compliance process, not a favor — requires clean audit history and electronic declaration infrastructure. Initial certification budget: **~$3,000 (~37M UZS)**; ongoing compliance is administrative.

**Pre-pack strategy:**
- **Commit 100% pre-pack only for AEO-cleared suppliers.**
- For non-AEO imports, default to post-distribution with 10–15% buffer inventory on top-200 SKUs.
- **Maintain two pre-qualified customs brokers**, never one. Single-broker dependency has burned multiple UZ chains when the one broker lost a key staff member or had a compliance issue.

**HS code discipline:** use precise HS-6 codes per category at PO time. Category Buyers own this assignment and are accountable for consistency between shipments — inconsistent coding is a classic trigger for red-channel inspection.

---

## Appendix D — Technology Architecture

Target stack — deliberately modest. Enterprise tools are optional and, in Phases 1–2, undesirable.

```
┌───────────────────────────────────────────────────────────────┐
│                   MERCHANDISING / PLANNING                    │
│  ┌─────────────────┐  ┌──────────────────────────────────┐    │
│  │  Item Master    │  │  Allocation Engine               │    │
│  │  + Color/Size   │  │  (Toolio / Onebeat / Syrup — SaaS)│   │
│  │  Masters        │  │                                  │    │
│  └────────┬────────┘  └─────────────┬────────────────────┘    │
└───────────┼─────────────────────────┼─────────────────────────┘
            ▼                         ▼
┌───────────────────────────────────────────────────────────────┐
│                     CORE ERP (1C:Enterprise)                  │
│    POs · Suppliers · Financials · GL · Inventory roll-up      │
└──────┬──────────────────────┬─────────────────┬───────────────┘
       │                      │                 │
       ▼                      ▼                 ▼
┌──────────────┐     ┌──────────────────┐     ┌──────────────────┐
│     WMS      │     │   SUPPLIER       │     │       POS        │
│  (1C:WMS or  │     │   PORTAL + ASN   │     │  (55 stores,     │
│   Mecalux    │     │   (Retool /      │     │   1C:Retail)     │
│   Easy)      │     │   Softr)         │     │                  │
└──┬───────────┘     └──────────────────┘     └────────┬─────────┘
   │                                                    │
   ▼                                                    │
┌──────────────────────────────────────────────┐        │
│   DC FLOOR: scanners + kiosks + put-to-      │        │
│   light + mobile printer carts + field-      │        │
│   intake kits (bazaar pickups)               │        │
└──────────────────────────────────────────────┘        │
                                                        │
          ┌─────────────────────────────────────────────┘
          ▼
┌──────────────────────────────────────────────────┐
│         DATA WAREHOUSE + BI LAYER                │
│  (Postgres / BigQuery + Metabase / Power BI)     │
│  Sell-through · Broken-size · Cluster analytics  │
└──────────────────────────────────────────────────┘
```

### D.1 Build vs. buy decisions

| Component | Recommendation | Reasoning |
|---|---|---|
| Core ERP | **Keep existing 1C** | Adequate for Phase 1–2. Migration later only if required. Avoids SAP-implementation quagmire. |
| Item Master / SKU module | **Build on 1C** | Custom module via local integrator. Cheap, local talent. |
| WMS | **Buy 1C:WMS or mid-market** (Mecalux Easy / Infor CSI) | Don't build. Don't buy enterprise — overkill at this scale. |
| Allocation engine | **Buy SaaS** (Toolio / Onebeat) | Don't build — ML-heavy, specialist. SaaS fits the volume. |
| Supplier portal | **Build minimal** (Retool / Softr) | It's a glorified form. Don't over-engineer. |
| POS integration | **Nightly sync** via connector | Real-time is over-engineered for weekly replenishment. |
| BI layer | **Metabase** (free/cheap) | Widely known in UZ market; works on SQL-readable data. |

### D.2 Data-flow reliability priorities

1. **POS → Data Warehouse**, nightly, zero-loss. Foundation for every analytic.
2. **PO + ASN → WMS**, reliable. Breaks cross-dock if missing.
3. **WMS → ERP** inventory sync. Breaks financials if missing.
4. **Allocation engine → WMS** pick lists. Requires clean masters upstream.

A broken link in #1 invalidates the entire project. Disproportionate effort goes to making the POS-to-DW pipe bulletproof before anything else is built.

### D.3 Labor-law compliance — Uzbekistan specifics

The 100+ headcount reduction over 12–18 months must comply with the **Labor Code of the Republic of Uzbekistan**:

- **Art. 99–101:** Employer-initiated redundancy termination requires **≥2 months' written notice** and severance of **≥2 months' average wages**. For 100 staff at ~4.5M UZS/month average, direct severance alone runs **~900M UZS (≈$73,500)**.
- **Trade union consultation:** if a primary union is present, consultation is mandatory ahead of redundancy notice.
- **Mandatory re-employment offer:** Art. 101 — if a comparable vacancy exists within the enterprise, it must be offered first.

**Design consequence:** the recommended "redeploy into new stores, not layoff" approach is not only politically preferable — it's **~$73K cheaper in direct severance cost** and removes union-consultation friction entirely. This is why the 12–18 month timeline is load-bearing: it is the time needed for store-network growth to absorb the headcount reduction naturally.

**Process recommendation:** brief the Ministry of Employment informally before Phase 4 begins. Positioning the story as "skills upgrade + redeployment, not layoff" protects both reputation and regulatory posture.

---

## Appendix E — Uzbekistan Market Context

The generic fast-fashion playbook must adapt to UZ realities. Six dynamics to plan around.

### E.1 The bazaar is not going away

Chorsu, Yangiobod, Olay, and Malika in Tashkent, plus regional bazaars in Samarqand, Bukhara, Namangan, Fergana, and Qarshi, will continue to supply **~30–50% of Dilmuss's SKUs** for the foreseeable future. Unlike Inditex's context — where supply is owned or contracted — Dilmuss must accommodate informal channels, not fight them. Field-intake kits (C.2) are the design answer: bring discipline *to* the supplier instead of asking the supplier to bring discipline.

### E.2 Turkish import — well-established, but customs-bottlenecked

Istanbul's Laleli, Merter, and Osmanbey districts supply most CIS fashion chains. Turkish suppliers are already accustomed to EDI, ASN, and barcoding for European customers; the compliance ask is **trivial for them**. **The binding constraint is Uzbek-side customs timing, not supplier capability.**

| District | Typical specialty | MOQ / style | Payment terms | Notes |
|---|---|---:|---|---|
| **Laleli** | Women's basics, knitwear | 300–500 | 30% upfront, 70% pre-ship | Best for pilot — mature logistics |
| **Merter** | Denim, outerwear, bigger cut-and-sew | 500–1,000 | 30–50% upfront | Volume plays |
| **Osmanbey** | Mid-premium, occasion wear | 200–300 | 50% upfront, net 30 | Smaller MOQs, higher margin |

**Shipping routes:** Istanbul → Tashkent most commonly by **truck via Turkey-Iran-Turkmenistan-Uzbekistan (10–14 days)** or **rail via Baku-Aktau-Beyneu (12–18 days)** or **air (2–3 days, cost-prohibitive except for top-priority replen)**. All three have distinct reliability and customs-interaction profiles — buffer stock planning must reflect the route mix, not an average.

### E.3 1C is the baseline ERP

Running SAP or Oracle is unrealistic for a mid-market Uzbek retailer. **1C:Enterprise is the standard** — local integrators, developer talent, and third-party integrations all exist. The recommended architecture (Appendix D) assumes 1C. **Do not migrate ERPs during this transition**; sequence matters. The classic "let's fix the ERP at the same time" plan has sunk most regional retail modernizations.

### E.4 Labor market dynamics

Warehouse loaded cost in Tashkent: **~$3,000–4,500/year (~36.8–55.1M UZS/year)**. Neither as cheap as outsiders assume, nor as expensive as Europe. Wage inflation running ~10–15%/year in formal-sector Tashkent through 2024–2026 — automation's ROI improves year over year.

**Political dimension:** a 100-person layoff attracts local media attention, government scrutiny, and workforce-morale damage. The recommended **redeployment-via-growth** model is more expensive on paper than straight layoffs but protects the project's political viability. This is why the 12–18 month timeline is not negotiable.

### E.5 Seasonality and the Uzbek retail calendar

Allocation and buying must respect these windows:

| Period | Dates (approx) | Demand signal | Operational note |
|---|---|---|---|
| Winter peak | Nov–Feb | Outerwear, knitwear | Largest single-season buy; plan for 4-month sell-through |
| **Navruz** | 21 March ± 10 days | Festive wear, family shopping spike | Receive 3 weeks pre-holiday; Central + Regional clusters both peak |
| Spring | Apr–May | Light layers, basics | Moderate, steady |
| Summer | Jun–Aug | Light, bright palette; tourist zones (Bukhara, Samarqand) spike | C5 cluster emphasis |
| **Back-to-school / Mustaqillik** (Independence Day, 1 Sept) | Late Aug | Basic tops, workwear | Secondary peak; 2-week receive window |
| Autumn | Sept–Oct | Transitional | Replenishment-heavy |

**Allocation-engine seasonality multipliers must be tuned on these specific windows**, not on a generic 4-season template. Missing Navruz timing is the single most common allocation error for chains new to Central Asia.

### E.6 Tashkent store geography — worked cluster illustration

For a 55-store chain, representative cluster assignments (illustrative — to be validated on actual POS):

- **C1 — Central premium:** Tashkent City, Next Mall flagship (Yunusabad), Compass Mall — urban-core, premium-adjacent, weekday-heavy.
- **C2 — Mall-urban:** Samarqand Darvoza, Riviera, Chimgan, Atlas — mid-tier malls, younger demographic, weekend-heavy.
- **C3 — Regional city:** Namangan, Andijan, Fergana, Margilan, Qarshi, Termez — stronger seasonal amplitude, traditional-palette weight, fuller size curves.
- **C4 — Bazaar-adjacent:** Chorsu-perimeter stores, Yunusabad side-street outlets, small-city centers — value-led, size-heavy M/L/XL.
- **C5 — Resort / seasonal:** Bukhara old town, Samarqand Registan-adjacent — tourist-season spikes, lighter palette.

Within-cluster store weights should reflect local demographics: e.g., Chorsu-perimeter C4 stores skew L/XL; Next Mall C1 runs heavier on S/M. These are one-time analytical exercises, re-validated annually.

### E.7 Competitive window

| Competitor | Positioning | Data maturity vs. Dilmuss |
|---|---|---|
| **LC Waikiki** (Uzbekistan franchise) | Mid-market fast-fashion | Fully SKU-ized, POS-driven (Turkish HQ systems) |
| **Koton** (UZ presence) | Mid-market fast-fashion | Fully SKU-ized (Turkish HQ) |
| **DeFacto** | Value fashion | Fully SKU-ized |
| **Zara** (Inditex) | Premium fast-fashion | Gold standard; out of Dilmuss's bracket |
| **Domestic chains (various)** | Value / traditional | Most at Dilmuss's current level or earlier |

**Strategic window:** most Uzbek-owned chains operate at Dilmuss's current data maturity. Being first to transition **creates a 3–5 year structural advantage** — better margins, cleaner assortment, faster response — very hard to catch up once established.

**The window is open now.** Turkish and Russian chains will expand more aggressively into UZ through 2027–2028. Every month of delay compresses first-mover advantage. **A transition started in Q2 2026 completes before the regional competitive density changes.**

---

*End of report.*
