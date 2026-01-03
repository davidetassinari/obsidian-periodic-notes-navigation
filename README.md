# Obsidian Periodic Notes Breadcrumb Navigation Templates

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Templater code for Obsidian periodic notes that creates automated breadcrumb navigation with proper ISO 8601 week-year handling for weeks that span calendar year boundaries.

## Key Features

- Automatic generation of title, creation date and breadcrumb navigation when creating a new note
- ISO 8601 compliant week numbers
- Automatic year-spanning week detection
- Consistent look and date formatting across monthly, weekly and daily notes

## Dependencies

This project relies on the Periodic Notes and Templater community plugins:

- [Periodic Notes](https://github.com/liamcain/obsidian-periodic-notes)
- [Templater](https://github.com/SilentVoid13/Templater)

## Setup

1. Install and enable Periodic Notes and Templater community plugins
2. Copy templates to your `Templates` folder
3. Configure Periodic Notes settings (see [Periodic Notes Settings](configs/periodic-notes-data.json))

## Documentation

- [ISO Week-Year Handling](docs/iso-week-year-handling.md) — Specifics of year-spanning weeks

## Examples

### Standard Breadcrumbs for Monthly, Weekly and Daily Notes

**November 2025**

```
[[2025]]  /  ❮  [[2025-10|October]]  |  November  |  [[2025-12|December]]  ❯
```

**Week 51 of 2025**

```
[[2025]]  /  [[2025-12|December]]
❮  [[2025-W50|Week 50]]  |  Week 51  |  [[2025-W52|Week 52]]  ❯
```

**28th December 2025**

```
[[2025]]  /  [[2025-12|December]]  /  [[2025-W52|Week 52]]
❮  [[2025-12-27]]  |  2025-12-28  |  [[2025-12-29]]  ❯
```

### Edge Cases for Months, Weeks and Days Crossing Year Boundary

**December 2025 and January 2026** (Final and Initial Months of the Year)

```
[[2025]]  –  [[2026]]  /  ❮ [[2025-11|November]]  |  December  |  [[2026-01|January]] ❯  

[[2025]]  –  [[2026]]  /  ❮ [[2025-12|December]]  |  January  |  [[2026-02|February]] ❯
```

**Week 1 of 2026** (Week Starting on 29th December 2025 and Crossing Over into 2026)

```
[[2025]]  –  [[2026]]  /  [[2025-12|December]]  –  [[2026-01|January]]
❮  [[2025-W52|Week 52]]  |  Week 1  |  [[2026-W02|Week 2]]  ❯
```

**29th December 2025** (Day in December Belonging to Week 1 of 2026)

```
[[2025]]  /  [[2025-12|December]]  /  [[2026-W01|Week 1]]
❮  [[2025-12-28]]  |  2025-12-29  |  [[2025-12-30]]  ❯
```

**31st December 2025 and 1st January 2026** (Final and Initial Day of the Year)

```
[[2025]]  –  [[2026]]  /  [[2025-12|December]]  –  [[2026-01|January]]  /  [[2026-W01|Week 1]]
❮  [[2025-12-30]]  |  2025-12-31  |  [[2026-01-01]]  ❯
```

```
[[2025]]  –  [[2026]]  /  [[2025-12|December]]  –  [[2026-01|January]]  /  [[2026-W01|Week 1]]
❮  [[2025-12-31]]  |  2026-01-01  |  [[2026-01-02]]  ❯
```

## Credits

Developed throughout 2025; final troubleshooting of ISO week-year edge cases in December 2025.

The insipiration definitely came from some Obsidian forum post that I did not think of noting. To further complicate matters, most of the coding was done by Claude, so it's hard to know where my own copy/paste starts and where LLM pre-training begins. If you feel like you deserve credit, reach out and I'll be happy to oblige.
