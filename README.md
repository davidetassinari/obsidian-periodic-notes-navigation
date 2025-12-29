# Obsidian Periodic Notes Templates

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Minimal working templates for Obsidian periodic notes with proper ISO 8601 
week-year handling for weeks that span calendar year boundaries.

## Key Features

- ISO 8601 compliant weekly notes
- Automatic year-spanning week detection
- Consistent date formatting across all periodic note types

## Setup

1. Install Periodic Notes plugin
2. Copy templates to your vault
3. Configure Periodic Notes settings (see [Periodic Notes Settings](configs/periodic-notes-data.json))

## Documentation

- [ISO Week-Year Handling](docs/iso-week-year-handling.md) — Specifics of year-spanning weeks

## Examples

### Standard Breadcrumbs for Monthly, Weekly and Daily Notes

**November 2025:**

```
[[2025]]  /  ❮  [[2025-10|October]]  |  November  |  [[2025-12|December]]  ❯
```

**Week 51 of 2025:**

```
[[2025]]  /  [[2025-12|December]]
❮  [[2025-W50|Week 50]]  |  Week 51  |  [[2025-W52|Week 52]]  ❯
```

**28th December 2025:**

```
[[2025]]  /  [[2025-12|December]]  /  [[2025-W52|Week 52]]
❮  [[2025-12-27]]  |  2025-12-28  |  [[2025-12-29]]  ❯
```

### Edge Cases for Months, Weeks and Days Spanning Year Boundary

**December 2025 and January 2026:**

```
2025  /  ❮ [[2025-11|November]]  |  December  |  [[2026-01|January]] ❯  /  2026

2025  /  ❮ [[2025-12|December]]  |  January  |  [[2026-02|February]] ❯  /  2026
```

**Week 01 of 2026** (29th December 2025 – 4th January 2026):

```
[[2025]]  /  [[2025-12|December]]  –  [[2026]]  /  [[2026-01|January]]
❮  [[2025-W52|Week 52]]  |  Week 01  |  [[2026-W02|Week 02]]  ❯
```

**29th December 2025:**

```
[[2025]]  /  [[2025-12|December]]  /  [[2026-W01|Week 1]]
❮  [[2025-12-28]]  |  2025-12-29  |  [[2025-12-30]]  ❯
```

## Credits

Developed throughout 2025; fimal troubleshooting of ISO week-year edge cases in December 2025.

The insipiration definitely came from some Obsidian forum post that I did not think of noting. To further complicate matters, most of the coding was done by Claude, so it's hard to know where my own digging starts and where LLM pre-training begins. If you feel like you deserve credit, reach out and I'll be happy to oblige.