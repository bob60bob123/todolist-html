# Aufgabenliste ToDo List

[中文](README.md) / [English](README.en.md) / [日本語](README.ja.md) / [한국어](README.ko.md) / [Deutsch](README.de.md) / [Français](README.fr.md)

---

## Übersicht

Eine einseitige HTML-Aufgabenlisten-Anwendung mit chinesischer UI. Kein Build-System, keine Framework-Abhängigkeiten.

**Demo**: Öffnen Sie `ToDoList.html` direkt in Ihrem Browser.

## Funktionen

- CRUD-Operationen mit Prioritätsstufen (十分紧急 / 较为紧急 / 一般)
- Benutzerdefinierte Kategorien
- Periodenstatistik (heute, diese Woche, dieser Monat, dieses Quartal, dieses Jahr)
- Filter: Alle, Aktiv, Erledigt, Nach Erstellungszeit, Nach Erledigungszeit, Nach Kategorie
- Echtzeit-Suche
- Export nach DOCX / Excel
- Import aus Excel
- Arbeitsberichterstellung
- Toneffekte
- Responsive Design
- **Mehrsprachige UI** (Chinesisch, Englisch, Japanisch, Koreanisch, Deutsch, Französisch)

## Schnellstart

```bash
# macOS
open ToDoList.html

# Windows
start ToDoList.html

# Linux
xdg-open ToDoList.html
```

## Datenspeicherung

- Alle Daten werden im Browser localStorage gespeichert
- Schlüssel: `todos`, `todoCategories`

## Technologie-Stack

- Vanilla JavaScript
- docx@8.5.0 (DOCX-Export)
- xlsx@0.18.5 (Excel-Import/Export)
- Google Fonts: Outfit, JetBrains Mono

## Lizenz

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
