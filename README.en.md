# ToDo List

[中文](README.md) / [English](README.en.md) / [日本語](README.ja.md)

---

## About

A single-file HTML ToDo application with Chinese UI. No build system, no framework dependencies.

**Online Demo**: Open `ToDoList.html` directly in your browser.

## Features

- CRUD operations with priority levels (十分紧急 / 较为紧急 / 一般)
- Custom categories
- Period statistics (day, week, month, quarter, year)
- Filter by: all, active, completed, create time, completion time, category
- Real-time search
- Export to DOCX / Excel
- Import from Excel
- Work report generation
- Sound effects
- Responsive design

## Quick Start

```bash
# Open directly in browser
open ToDoList.html
# or
start ToDoList.html
```

## Data Storage

- All data stored in browser localStorage
- Keys: `todos`, `todoCategories`

## Tech Stack

- Vanilla JavaScript
- docx@8.5.0 (DOCX export)
- xlsx@0.18.5 (Excel import/export)
- Google Fonts: Outfit, JetBrains Mono

## License

MIT
