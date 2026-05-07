# 待办事项置顶功能设计

## 概述

为待办事项增加置顶功能，允许用户将重要事项固定在列表顶部显示。

## 需求决策

| 问题 | 选择 |
|------|------|
| 置顶数量限制 | 不限制，可同时置顶任意数量 |
| 触发方式 | 专用按钮（📌），位于每条待办右侧 |
| 已完成置顶项处理 | 保留置顶状态，显示删除线 |
| 置顶在筛选视图中的行为 | 仅在"全部"和"待完成"筛选时置顶显示 |

## 数据模型

### 变更

在 `todo` 对象中新增 `pinned` 字段：

```javascript
todo = {
  id: number,           // Date.now()
  text: string,         // 待办内容
  priority: string,     // 'high' | 'medium' | 'low'
  category: string,     // 分类名称，默认 '工作'
  completed: boolean,   // 是否完成
  createTime: string,   // ISO 日期字符串
  completedAt: string,  // ISO 日期字符串，完成时设置
  pinned: boolean       // 新增：是否置顶，默认 false
}
```

### 新增函数

- `togglePin(id)` — 切换待办的置顶状态

## UI 设计

### 置顶按钮

- 位置：每条待办项右侧，优先级标签旁
- 图标：📌
- 样式：
  - 未置顶：灰色（`var(--text-tertiary)`）
  - 已置顶：主题色（`var(--primary)`）

### 已置顶待办显示

- 置顶按钮填充主题色
- 在"全部"和"待完成"筛选下，置顶项始终显示在列表顶部

## 核心逻辑

### 排序规则

在 `renderTodos()` 函数中应用以下排序：

```
if (currentFilter === 'all' || currentFilter === 'active') {
  // 1. 置顶项在前（按创建时间倒序）
  // 2. 非置顶项在后（按创建时间倒序）
} else {
  // 按原筛选逻辑不变
}
```

### 完成时的行为

- 完成后保留 `pinned: true`
- 不自动取消置顶状态

## 受影响的函数

| 函数 | 变更内容 |
|------|----------|
| `renderTodos()` | 增加置顶排序逻辑 |
| `renderTodosByDate()` | 不变（按时间分组，置顶不单独处理） |
| `renderTodosByCategory()` | 不变 |
| `renderTodosByPriority()` | 不变 |
| `addTodo()` | 默认设置 `pinned: false` |
| `exportJSON()` / `exportDOCX()` | 包含 pinned 字段 |
| `saveTodos()` | 已有的 localStorage 保存逻辑无需变更 |

## 音效

- 置顶切换时复用现有 `playSound('add')` 音效

## 测试要点

1. 点击置顶按钮，状态正确切换
2. 置顶项在"全部"和"待完成"视图中显示在最前
3. 置顶项在"按创建时间"、"按分类"、"按紧急程度"视图中按原逻辑显示
4. 完成的置顶项保留置顶状态和删除线
5. 刷新页面后置顶状态保持
6. 导出功能包含 pinned 字段
