# Liste de tâches ToDo List

[中文](README.md) / [English](README.en.md) / [日本語](README.ja.md) / [한국어](README.ko.md) / [Deutsch](README.de.md) / [Français](README.fr.md)

---

## Vue d'ensemble

Une application de liste de tâches HTML mono-fichier avec interface chinoise. Pas de système de build, pas de dépendances de framework.

**Démo**: Ouvrez `ToDoList.html` directement dans votre navigateur.

## Fonctionnalités

- Opérations CRUD avec niveaux de priorité (十分紧急 / 较为紧急 / 一般)
- Catégories personnalisées
- Statistiques périodiques (aujourd'hui, cette semaine, ce mois, ce trimestre, cette année)
- Filtres: Tous, Actifs, Terminés, Par date de création, Par date de fin, Par catégorie
- Recherche en temps réel
- Export vers DOCX / Excel
- Import depuis Excel
- Génération de rapports de travail
- Effets sonores
- Design responsive
- **Interface multilingue** (Chinois, Anglais, Japonais, Coréen, Allemand, Français)

## Démarrage rapide

```bash
# macOS
open ToDoList.html

# Windows
start ToDoList.html

# Linux
xdg-open ToDoList.html
```

## Stockage des données

- Toutes les données sont stockées dans le localStorage du navigateur
- Clés: `todos`, `todoCategories`

## Stack technique

- JavaScript vanilla
- docx@8.5.0 (Export DOCX)
- xlsx@0.18.5 (Import/Export Excel)
- Google Fonts: Outfit, JetBrains Mono

## Licence

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
