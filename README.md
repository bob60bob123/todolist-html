# 待办事项 ToDo List

[中文](README.md) / [English](README.en.md) / [日本語](README.ja.md)

---

## 简介

单文件 HTML 待办事项应用（中文界面）。无需构建系统，无框架依赖。

**在线演示**：直接在浏览器中打开 `ToDoList.html`

## 功能特点

- CRUD 操作，支持优先级（十分紧急 / 较为紧急 / 一般）
- 自定义分类
- 周期统计（今日、本周、本月、本季度、本年）
- 多维度筛选：全部、待完成、已完成、按创建时间、按完成时间、按分类
- 实时搜索
- 导出 DOCX / Excel
- 从 Excel 导入
- 工作汇报生成
- 音效反馈
- 响应式设计

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

MIT
