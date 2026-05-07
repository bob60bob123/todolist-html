# 待办事项文本编辑功能设计

**日期：** 2026-05-07
**功能：** 待办事项写完后，可修改事项内容

## 概述

为 ToDoList.html 添加事项文本行内编辑功能，用户可以在事项创建后随时修改其内容。

## 交互设计

### 用户流程

1. 用户点击事项文本区域
2. 文本区域变为多行 `<textarea>`，支持换行编辑
3. **保存**：点击 textarea 外部区域（失焦）自动保存
4. **取消**：点击编辑框内的"取消"按钮，恢复原内容

### 交互细节

- 点击事项文本 → 调用 `showTextEditor(id, event)`
- 失焦保存 → 调用 `saveTextEdit(id)`
- 取消按钮 → 调用 `cancelTextEdit(id)`，恢复原 `todo.text`
- 编辑过程中，事项的其他操作（切换完成状态、删除、修改优先级/分类）正常可用

### 键盘支持

- `Ctrl+Enter`：保存编辑（可选增强）
- `Esc`：取消编辑（可选增强）

## 视觉设计

### 编辑状态

- `<textarea>` 替换原 `.todo-text` 元素显示
- 高度自适应内容（rows=1 起始）
- 与输入框样式保持一致：inset box-shadow，无可见边框
- 聚焦时显示 inner shadow + outer glow

### 取消按钮

- 位于 textarea 右下角
- 小型灰色按钮，文字"取消"
- 样式与现有编辑模式保持一致

### 优先级/分类编辑视觉一致性

- 原文本隐藏（display:none）
- 编辑框占据原文本位置
- 编辑完成后恢复原文本显示

## 数据模型

无需变更，复用现有数据结构：

```javascript
todo = {
  id: number,
  text: string,      // 编辑此字段
  priority: string,
  category: string,
  completed: boolean,
  createTime: string,
  completedAt: string
}
```

## 函数设计

### showTextEditor(id, event)

- 参数：`id` - 待办事项ID，`event` - 点击事件
- 查找对应 todo，获取当前文本
- 创建 textarea 元素，替换 `.todo-text` 显示
- 隐藏原文本元素
- 聚焦 textarea
- 绑定 blur 事件用于保存

### saveTextEdit(id)

- 参数：`id` - 待办事项ID
- 获取 textarea 当前值
- 更新 `todos` 中对应 todo 的 `text` 字段
- 调用 `saveTodos()` 持久化
- 调用 `renderTodos()` 重新渲染
- 播放成功音效（可复用 'add' 或新增 'save'）

### cancelTextEdit(id)

- 参数：`id` - 待办事项ID
- 恢复原 `todo.text`（从闭包或 data 属性获取）
- 移除 textarea，恢复原文本显示
- 无需保存

## 边界处理

- 空内容：不允许保存空文本，保留编辑状态并提示
- 未修改：内容未改变时视为保存成功
- 快速操作：编辑过程中切换完成状态/删除，编辑自动取消

## 实现位置

`ToDoList.html` - 单文件应用

涉及函数添加位置：与 `showPriorityEditor`、`changePriority` 等编辑函数相邻

## 测试要点

1. 点击文本 → 进入编辑态
2. 修改内容 → 失焦自动保存
3. 点击取消 → 恢复原内容
4. 编辑空内容 → 提示并保留编辑态
5. 跨筛选条件编辑 → 保存后正确反映
