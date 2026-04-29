# ToDo List

[中文](README.md) / [English](README.en.md) / [日本語](README.ja.md)

---

## 概要

シングルファイルHTMLのToDoアプリケーション（中国語UI）。ビルドシステムやフレームワークの依存なし。

**デモ**: `ToDoList.html` をブラウザで直接開いてください。

## 機能

- 優先度レベル（十分紧急 / 较为紧急 / 一般）付きCRUD操作
- カスタムカテゴリ
- 期間統計（日、週、月、四半期、年）
- フィルタ：すべて、アクティブ、完了、作成時間順、完了時間順、カテゴリ別
- リアルタイム検索
- DOCX / Excelエクスポート
- Excelインポート
- 作業レポート生成
- 音效
- レスポンシブデザイン

## 使い方

```bash
# ブラウザで直接開く
open ToDoList.html
# または
start ToDoList.html
```

## データ保存

- すべてのデータはブラウザのlocalStorageに保存
- キー: `todos`, `todoCategories`

## 技術スタック

- Vanilla JavaScript
- docx@8.5.0 (DOCXエクスポート)
- xlsx@0.18.5 (Excelインポート/エクスポート)
- Google Fonts: Outfit, JetBrains Mono

## ライセンス

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
