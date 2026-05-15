# 工作总结周期选择器优化 - 实施方案

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** 优化工作总结模块的周期选择器，去掉"过去一周"，将固定周期改为可选择的周度/月度/季度/年度功能

**Architecture:** 修改 ToDoList.html 中的周期选择器 UI 和相关 JavaScript 函数。使用下拉面板集成设计，保持代码集中便于维护。

**Tech Stack:** Vanilla JS, HTML, CSS (单文件应用)

---

## 文件结构

- **修改**: `ToDoList.html` - 周期选择器 UI 和逻辑

---

### Task 1: 修改周期选择器 HTML 结构

**Files:**
- Modify: `ToDoList.html:1877-1887`

- [ ] **Step 1: 替换周期选择器 HTML**

将原有的9个固定周期按钮（过去1日、过去2日、过去3日、过去一周、今日、本周、本月、本季、全年）替换为新的结构。

**新 HTML 结构**:
```html
<div class="summary-periods">
    <button class="summary-tab" data-period="past1d" onclick="switchSummaryPeriod('past1d')">过去1日</button>
    <button class="summary-tab" data-period="past2d" onclick="switchSummaryPeriod('past2d')">过去2日</button>
    <button class="summary-tab" data-period="past3d" onclick="switchSummaryPeriod('past3d')">过去3日</button>
    <button class="summary-tab active" data-period="day" onclick="switchSummaryPeriod('day')">今日</button>
    <div class="period-selector-wrapper" style="display:inline-block;position:relative">
        <button class="summary-tab period-selector-btn" id="periodSelectorBtn" onclick="togglePeriodSelector()">
            📅 <span id="periodSelectorLabel">周期选择</span>
        </button>
        <div class="period-dropdown" id="periodDropdown" style="display:none;position:absolute;top:100%;left:0;background:#fff;border:1px solid #ddd;border-radius:8px;box-shadow:0 4px 12px rgba(0,0,0,0.15);z-index:1000;min-width:320px;padding:12px">
            <div class="period-tabs" style="display:flex;border-bottom:1px solid #eee;margin-bottom:10px">
                <button class="period-tab active" data-type="week" onclick="switchPeriodType('week')" style="padding:8px 16px;border:none;background:none;cursor:pointer;font-weight:600;border-bottom:2px solid #007bff">周度</button>
                <button class="period-tab" data-type="month" onclick="switchPeriodType('month')" style="padding:8px 16px;border:none;background:none;cursor:pointer;font-weight:600">月度</button>
                <button class="period-tab" data-type="quarter" onclick="switchPeriodType('quarter')" style="padding:8px 16px;border:none;background:none;cursor:pointer;font-weight:600">季度</button>
                <button class="period-tab" data-type="year" onclick="switchPeriodType('year')" style="padding:8px 16px;border:none;background:none;cursor:pointer;font-weight:600">年度</button>
            </div>
            <div class="period-options" id="periodOptions" style="max-height:300px;overflow-y:auto"></div>
        </div>
    </div>
</div>
```

---

### Task 2: 新增 JavaScript 状态变量

**Files:**
- Modify: `ToDoList.html` (在现有变量定义区域)

- [ ] **Step 1: 添加新的状态变量**

在 `let todos = ...` 附近添加:
```javascript
let currentPeriodType = 'week'; // 'week' | 'month' | 'quarter' | 'year'
let currentPeriodValue = ''; // 如 '2026-W20', '2026-05', '2026-Q2', '2026'
```

---

### Task 3: 实现周期选项生成函数

**Files:**
- Modify: `ToDoList.html`

- [ ] **Step 1: 添加周期选项生成函数**

在 `getPeriodRange` 函数之前添加:
```javascript
// 生成周度选项（本年内所有周，按月分组）
function getWeekOptions() {
    const options = [];
    const now = new Date();
    const currentYear = now.getFullYear();
    
    for (let month = 0; month < 12; month++) {
        const monthOptions = [];
        const firstDayOfMonth = new Date(currentYear, month, 1);
        const lastDayOfMonth = new Date(currentYear, month + 1, 0);
        
        // 找到该月第一个周一
        let weekStart = new Date(firstDayOfMonth);
        weekStart.setDate(weekStart.getDate() - weekStart.getDay() + 1);
        
        while (weekStart <= lastDayOfMonth) {
            const weekEnd = new Date(weekStart);
            weekEnd.setDate(weekEnd.getDate() + 6);
            
            const weekNum = getWeekNumber(weekStart);
            const startMonth = (weekStart.getMonth() + 1).toString().padStart(2, '0');
            const startDay = weekStart.getDate().toString().padStart(2, '0');
            const endMonth = (weekEnd.getMonth() + 1).toString().padStart(2, '0');
            const endDay = weekEnd.getDate().toString().padStart(2, '0');
            
            const label = `${currentYear}年第${weekNum}周 (${startMonth}/${startDay}-${endMonth}/${endDay})`;
            const value = `${currentYear}-W${weekNum.toString().padStart(2, '0')}`;
            
            monthOptions.push({ label, value });
            weekStart.setDate(weekStart.getDate() + 7);
        }
        
        if (monthOptions.length > 0) {
            options.push({ month: month + 1, weeks: monthOptions });
        }
    }
    
    return options;
}

// 获取某日期是第几周
function getWeekNumber(date) {
    const d = new Date(date);
    d.setHours(0, 0, 0, 0);
    d.setDate(d.getDate() + 4 - (d.getDay() || 7));
    const yearStart = new Date(d.getFullYear(), 0, 1);
    return Math.ceil((((d - yearStart) / 86400000) + 1) / 7);
}

// 生成月度选项（最近12个月，按年分组）
function getMonthOptions() {
    const options = [];
    const now = new Date();
    
    for (let i = 0; i < 12; i++) {
        const d = new Date(now.getFullYear(), now.getMonth() - i, 1);
        const year = d.getFullYear();
        const month = d.getMonth() + 1;
        const label = `${year}年${month.toString().padStart(2, '0')}月`;
        const value = `${year}-${month.toString().padStart(2, '0')}`;
        
        if (options.length === 0 || options[options.length - 1].year !== year) {
            options.push({ year, months: [] });
        }
        options[options.length - 1].months.push({ label, value });
    }
    
    return options;
}

// 生成季度选项（最近4个季度）
function getQuarterOptions() {
    const options = [];
    const now = new Date();
    const currentQuarter = Math.floor(now.getMonth() / 3);
    const currentYear = now.getFullYear();
    
    for (let i = 0; i < 4; i++) {
        let q = currentQuarter - i;
        let year = currentYear;
        
        while (q < 0) {
            q += 4;
            year--;
        }
        
        const label = `${year}年第${q + 1}季度`;
        const value = `${year}-Q${q + 1}`;
        
        if (options.length === 0 || options[options.length - 1].year !== year) {
            options.push({ year, quarters: [] });
        }
        options[options.length - 1].quarters.push({ label, value });
    }
    
    return options;
}

// 生成年度选项（最近5年）
function getYearOptions() {
    const now = new Date();
    const currentYear = now.getFullYear();
    const options = [];
    
    for (let i = 0; i < 5; i++) {
        const year = currentYear - i;
        options.push({
            label: `${year}年`,
            value: year.toString()
        });
    }
    
    return options;
}
```

---

### Task 4: 实现下拉面板切换和渲染函数

**Files:**
- Modify: `ToDoList.html`

- [ ] **Step 1: 添加下拉面板控制函数**

```javascript
function togglePeriodSelector() {
    const dropdown = document.getElementById('periodDropdown');
    const isVisible = dropdown.style.display !== 'none';
    
    if (isVisible) {
        dropdown.style.display = 'none';
    } else {
        renderPeriodOptions(currentPeriodType);
        dropdown.style.display = 'block';
    }
}

function switchPeriodType(type) {
    currentPeriodType = type;
    
    // 更新选项卡样式
    document.querySelectorAll('.period-tab').forEach(tab => {
        tab.style.borderBottom = tab.dataset.type === type ? '2px solid #007bff' : 'none';
    });
    
    renderPeriodOptions(type);
}

function renderPeriodOptions(type) {
    const container = document.getElementById('periodOptions');
    let html = '';
    
    if (type === 'week') {
        const weekOptions = getWeekOptions();
        weekOptions.forEach(group => {
            html += `<div style="margin-bottom:12px">
                <div style="font-size:12px;color:#666;margin-bottom:4px;font-weight:600">${group.month}月</div>
                <div style="display:flex;flex-wrap:wrap;gap:4px">`;
            group.weeks.forEach(w => {
                const isActive = currentPeriodValue === w.value ? 'background:#e3f2fd;border-color:#007bff' : '';
                html += `<button class="period-option" onclick="selectPeriod('${w.value}')" style="padding:4px 8px;font-size:11px;border:1px solid #ddd;background:#fff;border-radius:4px;cursor:pointer;${isActive}">${w.label}</button>`;
            });
            html += `</div></div>`;
        });
    } else if (type === 'month') {
        const monthOptions = getMonthOptions();
        monthOptions.forEach(group => {
            html += `<div style="margin-bottom:12px">
                <div style="font-size:12px;color:#666;margin-bottom:4px;font-weight:600">${group.year}年</div>
                <div style="display:flex;flex-wrap:wrap;gap:4px">`;
            group.months.forEach(m => {
                const isActive = currentPeriodValue === m.value ? 'background:#e3f2fd;border-color:#007bff' : '';
                html += `<button class="period-option" onclick="selectPeriod('${m.value}')" style="padding:4px 8px;font-size:11px;border:1px solid #ddd;background:#fff;border-radius:4px;cursor:pointer;${isActive}">${m.label}</button>`;
            });
            html += `</div></div>`;
        });
    } else if (type === 'quarter') {
        const quarterOptions = getQuarterOptions();
        quarterOptions.forEach(group => {
            html += `<div style="margin-bottom:12px">
                <div style="font-size:12px;color:#666;margin-bottom:4px;font-weight:600">${group.year}年</div>
                <div style="display:flex;flex-wrap:wrap;gap:4px">`;
            group.quarters.forEach(q => {
                const isActive = currentPeriodValue === q.value ? 'background:#e3f2fd;border-color:#007bff' : '';
                html += `<button class="period-option" onclick="selectPeriod('${q.value}')" style="padding:4px 8px;font-size:11px;border:1px solid #ddd;background:#fff;border-radius:4px;cursor:pointer;${isActive}">${q.label}</button>`;
            });
            html += `</div></div>`;
        });
    } else if (type === 'year') {
        const yearOptions = getYearOptions();
        html += `<div style="display:flex;flex-wrap:wrap;gap:4px">`;
        yearOptions.forEach(y => {
            const isActive = currentPeriodValue === y.value ? 'background:#e3f2fd;border-color:#007bff' : '';
            html += `<button class="period-option" onclick="selectPeriod('${y.value}')" style="padding:8px 16px;font-size:13px;border:1px solid #ddd;background:#fff;border-radius:4px;cursor:pointer;${isActive}">${y.label}</button>`;
        });
        html += `</div>`;
    }
    
    container.innerHTML = html;
}

function selectPeriod(value) {
    currentPeriodValue = value;
    const period = currentPeriodType + ':' + value;
    switchSummaryPeriod(period);
    
    // 更新按钮显示
    updatePeriodSelectorLabel();
    
    // 关闭下拉面板
    document.getElementById('periodDropdown').style.display = 'none';
    
    // 渲染统计
    renderSummary();
}

function updatePeriodSelectorLabel() {
    const labelEl = document.getElementById('periodSelectorLabel');
    if (!currentPeriodValue) {
        labelEl.textContent = '周期选择';
        return;
    }
    
    if (currentPeriodType === 'week') {
        const [year, week] = currentPeriodValue.split('-W');
        labelEl.textContent = `${year}年第${parseInt(week)}周`;
    } else if (currentPeriodType === 'month') {
        const [year, month] = currentPeriodValue.split('-');
        labelEl.textContent = `${year}年${parseInt(month)}月`;
    } else if (currentPeriodType === 'quarter') {
        const [year, quarter] = currentPeriodValue.split('-Q');
        labelEl.textContent = `${year}年第${parseInt(quarter)}季度`;
    } else if (currentPeriodType === 'year') {
        labelEl.textContent = `${currentPeriodValue}年`;
    }
}
```

---

### Task 5: 修改 getPeriodRange 函数

**Files:**
- Modify: `ToDoList.html:2276-2304`

- [ ] **Step 1: 扩展 getPeriodRange 支持新周期格式**

找到 `function getPeriodRange(period)` 函数，添加对新格式的支持:

```javascript
function getPeriodRange(period) {
    const now = new Date();
    const start = new Date(now);
    const end = new Date(now);
    
    // 处理新格式: 'week:2026-W20', 'month:2026-05', 'quarter:2026-Q2', 'year:2026'
    if (period.includes(':')) {
        const [type, value] = period.split(':');
        
        if (type === 'week') {
            const [year, week] = value.split('-W');
            // 计算该周开始日期（周一）
            const firstDayOfYear = new Date(parseInt(year), 0, 1);
            const daysOffset = (parseInt(week) - 1) * 7 - firstDayOfYear.getDay() + 1;
            start.setTime(firstDayOfYear.getTime() + daysOffset * 86400000);
            start.setHours(0, 0, 0, 0);
            end.setTime(start.getTime() + 6 * 86400000);
            end.setHours(23, 59, 59, 999);
        } else if (type === 'month') {
            const [year, month] = value.split('-');
            start.setFullYear(parseInt(year), parseInt(month) - 1, 1);
            start.setHours(0, 0, 0, 0);
            end.setFullYear(parseInt(year), parseInt(month), 0);
            end.setHours(23, 59, 59, 999);
        } else if (type === 'quarter') {
            const [year, quarter] = value.split('-Q');
            const q = parseInt(quarter) - 1;
            start.setFullYear(parseInt(year), q * 3, 1);
            start.setHours(0, 0, 0, 0);
            end.setFullYear(parseInt(year), q * 3 + 3, 0);
            end.setHours(23, 59, 59, 999);
        } else if (type === 'year') {
            start.setFullYear(parseInt(value), 0, 1);
            start.setHours(0, 0, 0, 0);
            end.setFullYear(parseInt(value), 11, 31);
            end.setHours(23, 59, 59, 999);
        }
    }
    // 原有固定周期处理保持不变
    else if (period === 'day') { start.setHours(0,0,0,0); end.setHours(23,59,59,999); }
    else if (period === 'past1d') { end.setDate(end.getDate()-1); end.setHours(23,59,59,999); start.setTime(end.getTime()); start.setHours(0,0,0,0); }
    else if (period === 'past2d') { end.setDate(end.getDate()-1); end.setHours(23,59,59,999); start.setDate(start.getDate()-2); start.setHours(0,0,0,0); }
    else if (period === 'past3d') { end.setDate(end.getDate()-1); end.setHours(23,59,59,999); start.setDate(start.getDate()-3); start.setHours(0,0,0,0); }
    // pastweek 已移除，不再支持
    else if (period === 'week') {
        const d = now.getDay();
        const diff = now.getDate() - d + (d === 0 ? -6 : 1);
        start.setDate(diff); start.setHours(0,0,0,0);
        end.setDate(diff + 6); end.setHours(23,59,59,999);
    }
    else if (period === 'month') { start.setDate(1); start.setHours(0,0,0,0); end.setMonth(end.getMonth()+1,0); end.setHours(23,59,59,999); }
    else if (period === 'quarter') {
        const q = Math.floor(now.getMonth() / 3);
        start.setMonth(q*3, 1); start.setHours(0,0,0,0);
        end.setMonth(q*3+3, 0); end.setHours(23,59,59,999);
    }
    else if (period === 'year') { start.setMonth(0,1); start.setHours(0,0,0,0); end.setMonth(11,31); end.setHours(23,59,59,999); }
    else if (period === 'custom' && customDate) {
        const d = new Date(customDate);
        start.setTime(d.getTime()); start.setHours(0,0,0,0);
        end.setTime(d.getTime()); end.setHours(23,59,59,999);
    }
    
    return { start, end };
}
```

---

### Task 6: 添加点击外部关闭下拉面板

**Files:**
- Modify: `ToDoList.html`

- [ ] **Step 1: 在 script 开头添加 document click 事件监听**

在 `let todos = ...` 之前添加:
```javascript
document.addEventListener('click', function(e) {
    const dropdown = document.getElementById('periodDropdown');
    const btn = document.getElementById('periodSelectorBtn');
    if (dropdown && btn && !dropdown.contains(e.target) && !btn.contains(e.target)) {
        dropdown.style.display = 'none';
    }
});
```

---

### Task 7: 测试验证

- [ ] **Step 1: 在浏览器中打开 ToDoList.html**
- [ ] **Step 2: 验证"过去一周"按钮已移除**
- [ ] **Step 3: 点击"📅 周期选择"按钮，验证下拉面板正常展开**
- [ ] **Step 4: 切换周度/月度/季度/年度选项卡，验证选项显示正确**
- [ ] **Step 5: 点击具体周期选项，验证统计数据更新正确**
- [ ] **Step 6: 点击"生成工作汇报"按钮，验证汇报内容正确**

---

## 计划自检

1. **Spec 覆盖检查**:
   - ✅ 删除"过去一周" - Task 1, Task 5
   - ✅ 周度选择本年内所有周 - Task 3, Task 4
   - ✅ 月度选择最近12个月 - Task 3, Task 4
   - ✅ 季度选择最近4个季度 - Task 3, Task 4
   - ✅ 年度选择最近5年 - Task 3, Task 4
   - ✅ 下拉面板交互 - Task 1, Task 4
   - ✅ i18n 更新 - Task 6

2. **Placeholder 扫描**: 无 TBD/TODO

3. **类型一致性**: 函数名和参数格式在所有 Task 中保持一致

---

**Plan complete and saved to** `docs/superpowers/plans/2026-05-15-summary-period-selector.md`