# ISO Week-Year Handling in Obsidian Periodic Notes

## The Problem

When a week spans two calendar years (e.g., December 29, 2025 to January 4, 2026), 
there's a mismatch between:
- **Calendar year**: The year on the calendar (2025 when you create the note)
- **ISO week-year**: The year the ISO week belongs to (2026 for this week)

## The Solution

### Periodic Notes Configuration
Use `GGGG-[W]WW` format for weekly notes:
- `GGGG` = ISO week-year (not calendar year)
- `WW` = ISO week number, zero-padded (01-53)

### Template Parsing

Always parse filenames with `GGGG-[W]WW`:
```javascript
const week = moment(tp.file.title, "GGGG-[W]WW");
```

### Token Reference

| Token | Example | Use Case |
|-------|---------|----------|
| `GGGG` | `2026` | ISO week-year for week identity |
| `YYYY` | `2025` | Calendar year for date-based links |
| `WW` | `01` | ISO week number (preferred) |
| `ww` | `01` | Locale week number (works in most cases) |

## Real Example: Week Starting Dec 29, 2025

**Correct filename:** `2026-W01`  
**Week belongs to:** ISO year 2026  
**Actual dates:** Dec 29, 2025 – Jan 4, 2026  

**Breadcrumb should show:**  
`[[2025]]  /  [[2025-12|December]]  –  [[2026]]  /  [[2026-01|January]]`

## Common Mistakes

❌ Using `YYYY-[W]WW` → Creates `2025-W01` (wrong year)  
❌ Using `moment(filename, "YYYY-[W]WW")` → Parses as calendar year  
✓ Using `GGGG-[W]WW` everywhere → Correct ISO week-year handling
