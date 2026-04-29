# ToDo List

[中文](README.md) / [English](README.en.md) / [日本語](README.ja.md)

---

## Overview

A single-file HTML ToDo application with Chinese UI. No build system, no framework dependencies.

**Demo**: Open `ToDoList.html` directly in your browser.

## Features

- CRUD operations with priority levels (十分紧急 / 较为紧急 / 一般)
- Custom categories
- Period statistics (today, this week, this month, this quarter, this year)
- Filter by: all, active, completed, by creation time, by completion time, by category
- Real-time search
- Export to DOCX / Excel
- Import from Excel
- Work report generation
- Sound effects
- Responsive design

## Quick Start

```bash
# macOS
open ToDoList.html

# Windows
start ToDoList.html

# Linux
xdg-open ToDoList.html
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
