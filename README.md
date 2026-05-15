# 待办事项 ToDo List

[中文](README.md) / [English](README.en.md) / [日本語](README.ja.md)

---

## 简介

单文件 HTML 待办事项应用，支持多语言（中文 / English / 日本語）。无需构建系统，无框架依赖。

**在线演示**：直接在浏览器中打开 `ToDoList.html`

## 功能特点

- CRUD 操作，支持优先级（十分紧急 / 较为紧急 / 一般）
- **事项内容可编辑** - 点击事项文本即可编辑，失焦自动保存
- **置顶功能** - 重要事项置顶显示，支持多个置顶
- 自定义分类
- 周期统计（今日、过去n日、灵活的周度/月度/季度/年度选择）
- 多维度筛选：全部、待完成、已完成、按创建时间、按完成时间、按分类
- 实时搜索
- 导出 DOCX / Excel
- 从 Excel 导入
- 工作汇报生成
- 音效反馈
- **回收站** - 误删可恢复，支持永久删除
- 响应式设计
- **多语言支持** - 中文 / English / 日本語

## 快速开始

```bash
# macOS
open ToDoList.html

# Windows
start ToDoList.html

# Linux
xdg-open ToDoList.html
```

## 数据存储

- 数据存储在浏览器 localStorage
- 存储键名：`todos`、`todoCategories`

## 技术栈

- 原生 JavaScript
- docx@8.5.0（DOCX 导出）
- xlsx@0.18.5（Excel 导入/导出）
- Google Fonts：Outfit、JetBrains Mono

## 开源协议

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
