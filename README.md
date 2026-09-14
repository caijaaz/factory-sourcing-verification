# factory-sourcing-verification

**An AI skill that finds real Chinese factories — and proves they're real.**

Verifies business status, import/export credentials, production licences and whether your product is actually in production. Separates genuine manufacturers from trading companies. Delivers a ranked, inquiry-ready factory pool.

> 通用「找真实生产工厂 + 资质核验」方法论 Skill。中文说明见 **[README.zh-CN.md](./README.zh-CN.md)**。

---

## The problem

If you've sourced from China, you've met these four. The hard part isn't *finding* a factory — it's finding one that **is one**:

| What you see | What's actually there |
|---|---|
| A polished English site saying "manufacturer" | A shell company with **one employee** on the social-insurance roll |
| A "R&D company" holding patents | **No production licence at all** |
| A valid production licence | **Its licensed scope doesn't cover your product** |
| A directory listing showing "active" | Stale data — or a **different company with the same name** |

The last one is the nastiest. Chinese company names collide constantly, and a directory entry that says "active" tells you nothing about whether the entity you're talking to is the entity on the licence.

This skill turns one real export-sourcing engagement into a **category-agnostic, repeatable process**. Rather than trusting any single platform, it **cross-verifies across multiple official sources** and answers two questions:

1. **Is this a real factory?**
2. **Can it legally ship my product?**

---

## You don't need to read Chinese for this

This is the part most foreign buyers get wrong about tools like this.

The skill is written as **instructions for your AI agent** — not as documentation for you. Your agent reads the Chinese-language sources (government disclosure portals, licence registries, recruitment listings, industry directories), runs the cross-checks, and **reports back in your language, with company names given in both Chinese and pinyin/English**.

So the Chinese source material isn't a barrier. It's the whole point: the verification evidence for a Chinese factory lives on Chinese-language official sites, and that's exactly what your agent is there to read.

**What you need:**
- An agent that supports skills (e.g. Claude Code, WorkBuddy, or any agent following the `SKILL.md` convention)
- Nothing else

---

## The five-stage workflow

```
Stage 1  Scope & thresholds   → product ID (CAS / model no.) + order profile
                                 + mandatory qualification thresholds + preferred region

Stage 2  Layered channel sweep → sweep layer / reverse-lookup layer / on-the-ground layer
                                 / shipping-evidence layer (12 core channels)
                                 + optional restricted layer

Stage 3  Four-dimension check  → ① business status
                                 ② import/export credentials
                                 ③ production licence — scope AND validity
                                 ④ target product actually in production

Stage 4  Rank & eliminate      → ★ top pick / Tier 1–3 / excluded
                                 (exclusion reason recorded, to prevent re-harvesting)

Stage 5  Deliver               → Excel qualification table
                                 + PDF factory cards
                                 + inquiry scripts
```

Evidence is graded in four levels — **hard evidence > strong > weak > invalid** — so "it's on their website" never gets mistaken for "it's been verified". See `references/verification-rules.md`.

---

## Install

**With git (user-level):**

```bash
git clone https://github.com/caijaaz/factory-sourcing-verification.git <your-agent-skills-dir>/factory-sourcing-verification
```

Replace `<your-agent-skills-dir>` with your agent's user-level skills directory.

**Without git:** click **`Code` → `Download ZIP`** at the top of this repo page, unzip, and drop the `factory-sourcing-verification/` folder into your agent's skills directory.

Then just ask, in plain English:

> *"Find me factories in China that make [product]"*
>
> *"Is this Chinese supplier a real manufacturer or a trading company?"*
>
> *"Verify this factory's qualifications before I place an order"*
>
> *"Who actually manufactures [brand]'s product?"*

---

## What you get

**Input** — the agent will ask for anything it's missing:

- Product name **+ unique identifier** (CAS number, model number)
- Order profile (quantity, container type, target market)
- Mandatory qualification thresholds, in priority order
- Preferred region
- Preferred deliverable format

**Output:**

1. **Excel qualification table**
   - Sheet 1 — *Verified factory pool*, 9 columns: factory / business status / import-export credentials / production licence / target product in production / positioning / contact / address / production scale
   - Sheet 2 — *Excluded list & reasoning* (so you never re-contact a dead lead)
2. **PDF factory cards** — one card per factory, with risk flags
3. **A ranked verdict in-conversation**, plus recommended next actions

---

## Repository layout

```
factory-sourcing-verification/
├── SKILL.md                        # Main entry: 5-stage pipeline, I/O, decision red lines
├── README.md                       # This file (English)
├── README.zh-CN.md                 # 中文说明
├── LICENSE                         # MIT
├── requirements.txt                # script dependency: openpyxl
├── references/
│   ├── channels.md                 # Layered channel matrix (12 core + optional restricted layer)
│   ├── verification-rules.md       # Four-dimension check details + common failure patterns
│   └── inquiry-template.md         # Inquiry scripts (phone script + RFQ email template)
└── scripts/
    └── gen_factory_xlsx.py         # Excel qualification-table generator
```

## Script dependency

```bash
pip install -r requirements.txt   # openpyxl
python scripts/gen_factory_xlsx.py output.xlsx
```

---

## Compliance & disclaimer

- All information comes from **public sources, cross-verified** — government disclosure, industry directories, public reporting. No unauthorised bulk scraping. **Publicly available ≠ legal to scrape**: this skill does not circumvent, and must not be used to circumvent, any website's technical measures.
- Business-registration and qualification data can be **stale or change without notice**. Before any formal engagement, confirm in writing with the factory and rely on the latest official documents.
- This repository is a **methodology tool**. Output is for reference only and is **not legal, tax or commercial advice**.

---

## Contributing

Issues and pull requests are welcome — especially:

- **Channels that work in your category or region** — the channel matrix is deliberately generic; category-specific channels are the most useful additions.
- **New "it looked like a factory but wasn't" failure patterns.** These are the most valuable contributions of all: every one of them becomes a check that saves the next person a bad order.

---

## License

[MIT](./LICENSE) © 2026 Factory Sourcing Verification contributors
