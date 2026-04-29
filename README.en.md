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

MIT License

```
MIT License

Copyright (c) 2024

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```
