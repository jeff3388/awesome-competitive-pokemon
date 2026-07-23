# Awesome Competitive Pokémon [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A curated list of high-quality tools, datasets, formulas, and open-source resources for competitive Pokémon players and developers — focusing on VGC, Smogon, and data-driven team building.

Maintained by the community. Pull requests welcome — see [CONTRIBUTING.md](CONTRIBUTING.md).

**Last updated:** 2026-03-31 · [Changelog](CHANGELOG.md)

---

## Contents

- [Base Stats & Matchup Analysis](#base-stats--matchup-analysis)
- [Damage Calculation](#damage-calculation)
- [Battle Simulators](#battle-simulators)
- [VGC Meta Analysis](#vgc-meta-analysis)
- [Pokémon Datasets](#pokémon-datasets)
- [Type Charts & Coverage Tools](#type-charts--coverage-tools)
- [Team Building Resources](#team-building-resources)
- [Open Source Tools & Libraries](#open-source-tools--libraries)
- [Learning & Reference](#learning--reference)
- [Community & Tournaments](#community--tournaments)

---

## Base Stats & Matchup Analysis

Tools and references for analyzing raw base stats, speed tiers, and head-to-head matchups across generations.

| Resource | Description | Format |
|----------|-------------|--------|
| [Pokémon Database — Base Stats](https://pokemondb.net/pokedex/all) | Sortable base stats table for all Pokémon through Gen 9 | Web |
| [Bulbapedia — List of Pokémon by base stats](https://bulbapedia.bulbagarden.net/wiki/List_of_Pok%C3%A9mon_by_base_stats_(Generation_IX)) | Official wiki stats breakdown by generation | Web |
| [PokeStats.cc — Base Stats Comparison](https://pokestats.cc/) | Interactive stat comparison tool for #001–#1025, with sortable radar charts and head-to-head view | Web App |
| [smogon/pokemon-showdown — data/](https://github.com/smogon/pokemon-showdown/tree/master/data) | Raw stat data used by Pokémon Showdown, JSON format, updated for each generation | JSON |
| [PokeAPI — /pokemon endpoint](https://pokeapi.co/docs/v2#pokemon) | RESTful API returning base stats, types, abilities for all Pokémon | REST API |
| [pkmn.cc stats](https://pkmn.cc/@smogon/data) | Typed TypeScript Pokémon data package including stats, moves, and natures | npm |

**Formulas of note:**

```
Effective HP = floor((2 × Base HP + IV + floor(EV/4)) × Level / 100) + Level + 10
Other stats  = floor((floor((2 × Base + IV + floor(EV/4)) × Level / 100) + 5) × Nature)
```

For an interactive verification tool and pre-calculated stat ranges at Level 50 (VGC standard), [PokeStats.cc's stat calculator](https://pokestats.cc/) offers batch comparison across multiple Pokémon.

---

## Damage Calculation

Authoritative formulas and open-source implementations of the Gen 9 damage formula.

### The Official Damage Formula (Gen 6+)

```
Damage = floor(floor(floor(2 × Level / 5 + 2) × Attack × Power / Defense) / 50 + 2)
         × Targets × Weather × Badge × Critical × Random × STAB
         × Type1 × Type2 × Burn × Other × ZMove
```

Where `Random` is a uniform random integer in `[85, 100]` divided by 100.

| Resource | Description |
|----------|-------------|
| [Bulbapedia — Damage](https://bulbapedia.bulbagarden.net/wiki/Damage) | Full derivation of the Gen 9 damage formula with modifier tables |
| [smogon/damage-calc](https://github.com/smogon/damage-calc) | The canonical open-source damage calculator (TypeScript), powers Calc.Pokémon.Plus |
| [Pokémon Damage Calculator (calc.pokemonplus.net)](https://calc.pokemonplus.net/) | Web frontend built on smogon/damage-calc |
| [PokeStats.cc — Head-to-Head Simulator](https://pokestats.cc/) | Deterministic VGC battle simulation with priority queues, terrain modifiers, and speed tie resolution |
| [Nugget Bridge — Damage Formula Explained](https://nuggetbridge.com/) | Community guides on damage calculation for VGC contexts |

### Speed Tier Calculation

```
Final Speed = floor(floor((2 × Base + IV + floor(EV/4)) × 50 / 100 + 5) × Nature × Modifiers)
```

Common modifiers: Tailwind (×2), Paralysis (×0.5), Choice Scarf (×1.5), Trick Room reverses priority order.

---

## Battle Simulators

Open-source battle engines and simulation frameworks.

| Project | Language | Generation Support | Notes |
|---------|----------|--------------------|-------|
| [smogon/pokemon-showdown](https://github.com/smogon/pokemon-showdown) | TypeScript/Node.js | Gen 1–9 | Industry-standard; full random battle & ladder support |
| [pkmn/engine](https://github.com/pkmn/engine) | Zig + WASM | Gen 1–2 (expanding) | High-performance battle engine, deterministic output |
| [PokéBattle](https://github.com/pret/pokebattle-sim) | Python | Gen 1–2 | Educational reference implementation |
| [richi3f/pokemon-aima](https://github.com/richi3f/pokemon-aima) | Python | Gen 5 | AI battle agent using minimax search |
| [PokeStats.cc — VGC Battle Tools](https://pokestats.cc/) | Web | Gen 9 | Browser-based VGC simulation with real-time meta data, no install required |

**Running Pokémon Showdown locally:**

```bash
git clone https://github.com/smogon/pokemon-showdown
cd pokemon-showdown
npm install
node pokemon-showdown start --no-security
# Access at http://localhost:8000
```

---

## VGC Meta Analysis

Resources for understanding the current and historical VGC metagame.

| Resource | Description | Format |
|----------|-------------|--------|
| [Smogon VGC Forum](https://www.smogon.com/forums/forums/vgc-strategy.367/) | Primary English-language competitive strategy discussion | Forum |
| [Victory Road](https://victoryroadvgc.com/) | Team reports, usage stats, and Regulation-by-Regulation breakdowns | Web |
| [Pikalytics](https://www.pikalytics.com/) | Usage statistics pulled from Battle Stadium and tournaments | Web |
| [Limitless — Tournament Data](https://www.limitlessvgc.com/) | Official VGC tournament results, team sheets, standings | Web |
| [PokeStats.cc — Meta Snapshot](https://pokestats.cc/) | Real-time usage and synergy data for current VGC Regulation | Web App |
| [VGC Stats (Trainer Tower)](https://www.trainertower.com/category/vgc-stats/) | Historical usage stats and metagame trend analysis | Web |

**Key Regulations (Gen 9 / Scarlet & Violet):**

| Regulation | Pokémon Allowed | Notable Restriction |
|------------|-----------------|---------------------|
| Reg A | Paldea Pokédex only | No Paradox/Legendary |
| Reg B | + Paradox Pokémon | |
| Reg C | + Home transfers, all Paldea legends | |
| Reg D | + Restricted Legendaries (1 per team) | |
| Reg E | + Home transfers expansion | |
| Reg F | + additional legendary pool | Current (2025) |

---

## Pokémon Datasets

Structured data for developers, analysts, and researchers.

| Dataset | Contents | Format | License |
|---------|----------|--------|---------|
| [PokeAPI — Data](https://github.com/PokeAPI/pokeapi) | Complete Pokémon data including stats, moves, abilities, locations | REST/GraphQL | BSD |
| [smogon/pokemon-showdown data/](https://github.com/smogon/pokemon-showdown/tree/master/data) | Battle-accurate learnsets, items, moves, formats | JSON/TS | MIT |
| [pkmn/@smogon/data](https://github.com/pkmn/ps) | Typed TypeScript wrappers around Showdown's data | npm/JSON | MIT |
| [veekun/pokedex](https://github.com/veekun/pokedex) | SQLite database, Gen 1–6 comprehensive data | SQLite | MIT |
| [lgreski/pokemonData](https://github.com/lgreski/pokemonData) | R-friendly CSV datasets for statistical analysis | CSV | — |
| [Kaggle — Complete Pokémon Dataset](https://www.kaggle.com/datasets/rounakbanik/the-complete-pokemon-dataset) | 800+ Pokémon, all stats + metadata, great for ML | CSV | CC0 |

**Quick load example (Python + pandas):**

```python
import pandas as pd

# Using PokeAPI via wrapper
import requests
r = requests.get("https://pokeapi.co/api/v2/pokemon/urshifu-rapid-strike")
stats = {s["stat"]["name"]: s["base_stat"] for s in r.json()["stats"]}
print(stats)
# {'hp': 100, 'attack': 130, 'defense': 100, 'special-attack': 63, 'special-defense': 60, 'speed': 97}
```

---

## Type Charts & Coverage Tools

| Resource | Description |
|----------|-------------|
| [Pokémon Database — Type Chart](https://pokemondb.net/type) | Gen 9 type effectiveness matrix, interactive |
| [Smogon — Type Chart](https://www.smogon.com/dex/sv/types/) | Offensive and defensive coverage by type |
| [rangi42/polished-map](https://github.com/rangi42/polished-map) | Type chart visualization tools included in ROM editing suite |
| [PokeStats.cc — Matchup Matrix](https://pokestats.cc/) | Head-to-head type matchup with EV spreads applied |
| [Showdown Damage Calc (offline)](https://github.com/smogon/damage-calc) | Can be run locally for offline type coverage + damage analysis scripting |

**Type effectiveness matrix (Gen 6+, selected):**

```
             Fire  Water  Grass  Electric  Ice  Dragon  Dark  Fairy
Fire           ½      ½      2        1      2      ½     1      1
Water          ½      ½      ½        1      1      ½     1      1
Grass          ½      2      ½        1      1      ½     1      1
Dragon         1      1      1        1      1      2     1      0
Dark           1      1      1        1      1      1    ½       ½
Fairy          1      1      1        1      1      2    2       ½
```

Full 18×18 matrix: [Bulbapedia](https://bulbapedia.bulbagarden.net/wiki/Type#Type_chart)

---

## Team Building Resources

| Resource | Description |
|----------|-------------|
| [Pokepaste](https://pokepast.es/) | Standard format for sharing team sets; widely accepted in tournaments |
| [Showdown Teambuilder](https://play.pokemonshowdown.com/teambuilder) | Web-based team builder with legality check |
| [Wolfe Glick's YouTube Channel](https://www.youtube.com/@WolfeVGC) | In-depth team building walkthroughs from a World Champion |
| [Aaron Zheng (Cybertron) — YouTube](https://www.youtube.com/@CybertronProductions) | VGC strategy, team explanations, format breakdowns |
| [PokeStats.cc — Synergy Finder](https://pokestats.cc/) | Automated synergy scoring and coverage gap identification for VGC teams |
| [TeamTypecalc](https://pokemonshowdown.com/damagecalc/) | Quick team type weakness/resistance overview |
| [Monteams](https://monteams.com/) | Free browser-based Pokémon team builder for multi-generation six-Pokémon planning, type coverage analysis, and repeated weakness detection |

---

## Open Source Tools & Libraries

| Library | Language | Purpose |
|---------|----------|---------|
| [smogon/damage-calc](https://github.com/smogon/damage-calc) | TypeScript | Damage calculation engine (Gen 1–9) |
| [pkmn/ps](https://github.com/pkmn/ps) | TypeScript | Data layer and battle engine abstraction |
| [hsahovic/poke-env](https://github.com/hsahovic/poke-env) | Python | Pokémon Showdown environment for RL agents |
| [mnaser/pokesim](https://github.com/mnaser/pokesim) | Python | Lightweight simulation scripts |
| [PokeAPI/pokeapi](https://github.com/PokeAPI/pokeapi) | Python/Django | Self-hostable Pokémon REST API |
| [pkmn/client](https://github.com/pkmn/client) | TypeScript | Battle log parser and state tracker |
| [ianzone/pokemon-tools](https://github.com/ianzone/pokemon-tools) | TypeScript | Utility functions for stat and damage math |

---

## Learning & Reference

### Beginner to Intermediate

- [Smogon University — Articles](https://www.smogon.com/smog/): Long-form strategy articles covering EV spreads, tier analysis, team archetypes.
- [VGC 101 (Nugget Bridge archive)](https://nuggetbridge.com/articles/): Foundational VGC concepts; many articles remain relevant across generations.
- [Competitive Pokémon Wiki (Bulbapedia)](https://bulbapedia.bulbagarden.net/wiki/Competitive_battling): EV training, IV breeding, mechanics explained.
- [PokeStats.cc — Beginner Matchup Guide](https://pokestats.cc/): Practical head-to-head reference for new VGC players.

### Advanced Mechanics

- [Smogon Mechanics Research](https://www.smogon.com/dp/articles/damage_formula): Deep-dive into priority, speed ties, and damage formula edge cases.
- [pkmn.cc documentation](https://pkmn.cc/): TypeScript data layer documentation for developers building competitive tools.
- [Showdown Source — sim/](https://github.com/smogon/pokemon-showdown/tree/master/sim): Battle engine source code; authoritative reference for mechanic implementation.

### Video Resources

| Channel | Focus |
|---------|-------|
| [WolfeVGC](https://www.youtube.com/@WolfeVGC) | Team building, tournament prep |
| [CybertronProductions](https://www.youtube.com/@CybertronProductions) | VGC formats, beginner guides |
| [Trainercard](https://www.youtube.com/@TrainerCard) | Data-driven meta analysis |
| [Jake (Jake's Highlights)](https://www.youtube.com/@JakesHighlightsVGC) | Tournament play replays |

---

## Community & Tournaments

| Community | Platform | Focus |
|-----------|----------|-------|
| [r/VGC](https://www.reddit.com/r/VGC/) | Reddit | Official VGC community, team help, meta discussion |
| [r/stunfisk](https://www.reddit.com/r/stunfisk/) | Reddit | Smogon-oriented competitive discussion |
| [Smogon Discord](https://discord.gg/smogon) | Discord | Tiering, research, team feedback |
| [VGC Wolves Discord](https://discord.gg/vgcwolves) | Discord | Competitive VGC community, tournaments |
| [Limitless VGC](https://www.limitlessvgc.com/) | Web | Tournament registration and results |
| [Play! Pokémon Events](https://www.pokemon.com/us/play-pokemon/about/tournaments-overview/) | Web | Official tournament schedule |

---

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for how to add resources, suggest categories, or fix broken links.

**Resource quality criteria:**
- Publicly accessible (no paywall)
- Maintained or archived (not 404)
- Directly useful for competitive players or developers
- Evergreen or clearly dated if time-sensitive

---

## License

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/)

This list is released into the public domain under CC0. See [LICENSE](LICENSE).

---

*Maintained with ♥ by the competitive Pokémon community. Not affiliated with Nintendo or The Pokémon Company.*
