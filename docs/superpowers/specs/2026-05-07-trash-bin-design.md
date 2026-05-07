# 回收站功能设计

**日期：** 2026-05-07
**功能：** 为待办事项添加回收站功能，防止误删

## 概述

为 ToDoList.html 添加回收站功能，删除的待办事项先进入回收站，可恢复或永久删除。

## 交互设计

### 用户流程

1. 工具栏显示回收站图标按钮 🗑️，带 badge 显示回收站数量
2. 点击按钮 → 显示回收站弹窗列表
3. 每项显示：事项内容、删除时间、"恢复"按钮、"永久删除"按钮
4. 恢复 → 事项回到主列表；永久删除 → 二次确认后彻底清除
5. 点击弹窗外部关闭

### 交互细节

- 点击回收站图标 → 调用 `toggleTrashBin()`
- 点击"恢复" → 调用 `restoreFromTrash(id)`
- 点击"永久删除" → 调用 `permanentDelete(id)`（需确认）
- 弹窗外点击 → 关闭弹窗

### 键盘支持

- `Esc`：关闭回收站弹窗

## 数据设计

### localStorage

- 键名：`trashBin`
- 数据结构：
```javascript
trashBin = [{
  id: number,
  text: string,
  priority: string,
  category: string,
  completed: boolean,
  createTime: string,
  deletedAt: string  // ISO date string，删除时间
}]
```

### 数据操作

- **deleteTodo(id)**：改为移入回收站
  - 从 `todos` 中移除
  - 添加到 `trashBin`（带 `deletedAt` 时间戳）
  - 保存到 localStorage

- **restoreFromTrash(id)**：
  - 从 `trashBin` 中移除
  - 添加回 `todos`
  - 保存两个 localStorage

- **permanentDelete(id)**：
  - 从 `trashBin` 中移除
  - 保存 localStorage

## UI 设计

### 回收站按钮

- 位于工具栏操作区
- 🗑️ 图标 + 数量 badge（如 "3"）
- 无内容时 badge 隐藏

### 回收站弹窗

- 居中显示，带遮罩层
- 标题："回收站"
- 空状态："回收站为空"
- 列表每项：
  - 事项文本（截断显示）
  - 删除时间
  - "恢复"按钮（主要）
  - "永久删除"按钮（危险/次要样式）
- 关闭按钮（右上角 X）

### 永久删除确认

- 浏览器 confirm 对话框
- 文本："确定要永久删除此事项吗？此操作不可恢复。"

## 函数设计

### toggleTrashBin()

- 显示/隐藏回收站弹窗
- 切换工具栏图标 active 状态

### moveToTrashBin(id)

- 将 todo 从 `todos` 移至 `trashBin`
- 添加 `deletedAt` 时间戳
- 保存两个 localStorage
- 播放删除音效
- 重新渲染

### restoreFromTrash(id)

- 从 `trashBin` 移回 `todos`
- 移除 `deletedAt` 字段
- 保存两个 localStorage
- 重新渲染

### permanentDelete(id)

- 从 `trashBin` 中移除
- 保存 localStorage
- 重新渲染

### renderTrashBin()

- 读取 `trashBin`
- 生成弹窗 HTML
- 更新 badge 数量

## 实现位置

`ToDoList.html` - 单文件应用

- CSS：工具栏按钮和弹窗样式
- JS：`toggleTrashBin`、`moveToTrashBin`、`restoreFromTrash`、`permanentDelete`、`renderTrashBin`
- 修改：`deleteTodo` 改为调用 `moveToTrashBin`

## 边界处理

- 回收站列表按删除时间倒序（最新在前）
- 恢复后事项保持原 completed 状态
- 工具栏 badge 仅显示数量，0 时隐藏
