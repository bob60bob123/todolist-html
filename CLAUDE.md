# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Single-file HTML ToDo application (`ToDoList.html`) - a vanilla JS productivity app with Chinese UI. No build system, no framework dependencies.

## Architecture

- **Single HTML file** (~2400 lines) containing all CSS and JavaScript
- **Data persistence**: localStorage (`todos`, `todoCategories` keys)
- **External dependencies** (loaded via CDN):
  - `docx@8.5.0` - DOCX export
  - `xlsx@0.18.5` - Excel import/export
  - Google Fonts: Outfit (UI), JetBrains Mono (monospace)

## Key Features

- CRUD operations for todos with priority levels (十分紧急/较为紧急/一般)
- **Categories** - custom categories with default "工作", click to edit
- Statistics: total, completed, remaining counts
- Period summaries: past 1/2/3 days, past week, day, week, month, quarter, year
- Filter by: all, active, completed, byCreateTime, byCompletedTime, byCategory
- **Search** - real-time keyword filtering across all views
- Export: DOCX and Excel (with filter options: all/active/completed/byCreateTime/byCompletedTime)
- Import from Excel files
- Work report generation with copy and DOCX export
- Priority and category editing via click-to-dropdown on todo items
- Responsive design (desktop, tablet, mobile breakpoints)

## Development

This is a static HTML file - no build, no test, no lint commands. Open directly in browser for development:

```
ToDoList.html
```

## Data Model

```javascript
todo = {
  id: number,        // Date.now()
  text: string,      // todo content
  priority: string,  // 'high' | 'medium' | 'low'
  category: string,  // category name, default '工作'
  completed: boolean,
  createTime: string, // ISO date string
  completedAt: string // ISO date string, set on completion
}

categories = ['工作', ...] // stored in localStorage
```

## Important Implementation Notes

- All todos share a single `localStorage` key - no per-user separation
- Categories stored separately in `todoCategories`
- Import skips rows where column A contains: 统计, 总计, 十分紧急, 较为紧急, 一般
- Period calculations use local timezone
- XSS prevention via `escapeHtml()` helper before rendering user content
- Priority and category editors use hidden `<select>` elements that show on click
- Summary stats use `filterTodosByPeriod()` which considers `completedAt` for completed items
- Sound effects via Web Audio API (sine wave oscillators) for: add, complete, delete, error events
- Period tabs "past1d/past2d/past3d/pastweek" filter by `completedAt` for completed items; regular periods (day/week/month/etc.) filter by `createTime`
- Export/DOCX functions use async `Packer.toBlob()` with click-triggered download
