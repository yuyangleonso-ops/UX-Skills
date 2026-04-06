# Arco Design 字体排版

## 字体家族

### 中文优先字体栈

```css
font-family: 'PingFang SC', 'Hiragino Sans GB', 'Microsoft YaHei', sans-serif;
```

| 平台 | 首选字体 | 备用 |
|------|----------|------|
| macOS | PingFang SC (苹方) | Hiragino Sans GB |
| Windows | Microsoft YaHei (微软雅黑) | SimHei |
| iOS | PingFang SC | - |
| Android | Noto Sans CJK | Roboto |

### 西文优先字体栈

```css
font-family: 'Nunito', 'Helvetica Neue', Helvetica, Arial, sans-serif;
```

**Primary Font**: Nunito
- 圆润友好的几何无衬线字体
- 与字节跳动品牌气质一致
- 支持 14 种字重（Light 到 Black）

### 完整字体栈（推荐）

```css
font-family: 'Nunito', 'Helvetica Neue', Helvetica, 'PingFang SC', 'Hiragino Sans GB', 'Microsoft YaHei', Arial, sans-serif;
```

---

## 字号系统

### 基础规范

| 规范项 | 数值 | 说明 |
|--------|------|------|
| **主字号** | **14px** | 正文、表单、表格默认 |
| **最小可识别** | **12px** | 辅助信息、时间戳 |
| **层级差距** | **2-4px** | 相邻层级间差距 |
| **层级数量** | **3-5 种** | 同一产品内控制 |

### 字号层级表

| 层级 | 字号 | 字重 | 行高 | 用途 |
|------|------|------|------|------|
| 大标题 | 24px | 600 | 32px | 页面大标题 |
| 标题 | 20px | 600 | 28px | 区块标题 |
| 小标题 | 16px | 600 | 24px | 卡片标题、表单分组标题 |
| 正文 | **14px** | 400/500 | 22px | 主要内容、表单 |
| 辅助 | **12px** | 400 | 20px | 辅助信息、时间戳 |

### 字号使用场景

| 场景 | 推荐字号 | 示例 |
|------|----------|------|
| 页面标题 | 20-24px | "用户管理" |
| 区块标题 | 16px | "基本信息" |
| 表格内容 | 14px | 数据表格 |
| 表单标签 | 14px | "用户名" |
| 表单输入 | 14px | 输入框文字 |
| 按钮文字 | 14px | "保存"、"取消" |
| 辅助描述 | 12px | "支持 JPG、PNG 格式" |
| 时间戳 | 12px | "2024-01-01 12:00" |

---

## 字重系统

### 字重定义

| 字重名称 | 数值 | CSS | 用途 |
|----------|------|-----|------|
| Light | 300 | font-weight: 300 | 特殊场景、大段文字 |
| Regular | 400 | font-weight: 400 | **正文主体** |
| Medium | 500 | font-weight: 500 | **中等强调** |
| Semibold | 600 | font-weight: 600 | **标题、强调** |
| Bold | 700 | font-weight: 700 | 强强调（少用） |

### 字重使用规范

**强调信息的方式（优先级）：**

1. **首选：字重变化**
   - Regular (400) → Medium (500) → Semibold (600)
   - 适用于：标签、关键数据、操作按钮

2. **其次：颜色变化**
   - Grey-10 → Grey-8 → Grey-6
   - 适用于：次要信息、辅助说明

3. **慎用：字号变化**
   - 容易导致层级混乱
   - 仅用于明确的层级区分（标题 vs 正文）

### 字重场景对照

| 元素 | 推荐字重 | 说明 |
|------|----------|------|
| 正文 | 400 (Regular) | 默认正文 |
| 表单标签 | 400 (Regular) | 标准标签 |
| 表格标题 | 500 (Medium) | 列标题稍强调 |
| 按钮文字 | 400/500 (Regular/Medium) | 根据层级 |
| 卡片标题 | 500/600 (Medium/Semibold) | 区块标题 |
| 页面标题 | 600 (Semibold) | 最大标题 |
| 关键数据 | 600 (Semibold) | 指标数字 |

---

## 行高系统

### 基础规范

| 语言/场景 | 行高 | 说明 |
|-----------|------|------|
| **默认** | **1.4** | Arco 默认行高 |
| 西文 | ~1.2 | 西文有 ascender/descender |
| 中文 | 1.5-2 | 中文更密实，需要更大行高 |
| 标题 | 较小 | 32px-44px 固定值 |

### 行高场景表

| 场景 | 字号 | 行高 | 计算值 | 说明 |
|------|------|------|--------|------|
| 正文（短） | 14px | 1.4 | 20px | 3 行以内 |
| 正文（长） | 14px | 1.6-1.8 | 22-25px | 长段落 |
| 标题 | 24px | 1.33 | 32px | 大标题 |
| 标题 | 20px | 1.4 | 28px | 中标题 |
| 标题 | 16px | 1.5 | 24px | 小标题 |
| 辅助文字 | 12px | 1.67 | 20px | 时间戳等 |

### Arco Typography 组件行高

| 组件 | 行高模式 | 说明 |
|------|----------|------|
| Text default | 默认行高 | 1.4 倍 |
| Text close | 紧凑行高 | 适合短文本 |
| Paragraph | 默认行高 | 适合长文本 |

---

## 排版模式

### 标题排版

**页面标题：**
```jsx
// 页面顶部大标题
<Typography.Title heading={3} style={{ marginBottom: 24 }}>
  用户管理
</Typography.Title>

// CSS 等效
.page-title {
  font-size: 20px;
  font-weight: 600;
  line-height: 28px;
  color: #1D2129;
  margin-bottom: 24px;
}
```

**区块标题：**
```jsx
// 卡片/区块标题
<Typography.Title heading={5} style={{ marginBottom: 16 }}>
  基本信息
</Typography.Title>

// CSS 等效
.section-title {
  font-size: 16px;
  font-weight: 600;
  line-height: 24px;
  color: #1D2129;
  margin-bottom: 16px;
}
```

### 正文排版

**段落：**
```jsx
<Typography.Paragraph style={{ fontSize: 14, lineHeight: 1.6 }}>
  这是一段正文内容，使用 14px 字号，1.6 倍行高，
  适合长文本阅读。
</Typography.Paragraph>
```

**短文本：**
```jsx
// 紧凑行高适合短文本
<Typography.Text type="secondary">
  辅助信息
</Typography.Text>
```

### 表单排版

**标签对齐：**

| 对齐方式 | 适用场景 | 特点 |
|----------|----------|------|
| 右对齐 | 常见表单 | 标签与输入框关系明确 |
| 左对齐 | 长标签 | 标签易读，但关系稍弱 |
| 顶对齐 | 复杂表单 | 空间充裕，适合长标签 |
| 内联 | 简单表单 | 标签在输入框内 |

**标签样式：**
```jsx
<Form layout="horizontal">
  <Form.Item label="用户名">
    <Input placeholder="请输入用户名" />
  </Form.Item>
</Form>

// CSS
.form-label {
  font-size: 14px;
  font-weight: 400;
  color: #4E5969;  /* Grey-8 */
  line-height: 32px;  /* 与输入框对齐 */
}
```

---

## 排版原则

### 1. 克制层级

**原则**：同一产品内控制 3-5 种字号层级

**反例**：
```css
/* ❌ 层级过多，混乱 */
.text-1 { font-size: 13px; }
.text-2 { font-size: 14px; }
.text-3 { font-size: 15px; }
.text-4 { font-size: 16px; }
.text-5 { font-size: 17px; }
```

**正例**：
```css
/* ✅ 清晰的层级 */
.text-small { font-size: 12px; }   /* 辅助 */
.text-base { font-size: 14px; }    /* 正文 */
.text-heading { font-size: 16px; } /* 标题 */
.text-large { font-size: 20px; }   /* 大标题 */
```

### 2. 用字重强调

**原则**：优先使用字重而非字号来强调

**反例**：
```jsx
// ❌ 用字号强调
<span style={{ fontSize: 16 }}>重要信息</span>
<span style={{ fontSize: 14 }}>普通信息</span>
```

**正例**：
```jsx
// ✅ 用字重强调
<span style={{ fontWeight: 600 }}>重要信息</span>
<span style={{ fontWeight: 400 }}>普通信息</span>

// 或用 Typography 组件
<Typography.Text bold>重要信息</Typography.Text>
```

### 3. 中文适配

**原则**：中文需要比西文更大的行高

**代码：**
```css
/* 西文内容 */
.english-content {
  font-family: 'Nunito', sans-serif;
  line-height: 1.4;
}

/* 中文内容 */
.chinese-content {
  font-family: 'PingFang SC', 'Microsoft YaHei', sans-serif;
  line-height: 1.6;  /* 更大行高 */
}

/* 混合内容 */
.mixed-content {
  font-family: 'Nunito', 'PingFang SC', sans-serif;
  line-height: 1.5;  /* 取中间值 */
}
```

### 4. 对齐基线

**原则**：不同字号的元素要对齐基线

**反例**：
```jsx
// ❌ 不对齐
<div>
  <span style={{ fontSize: 20 }}>标题</span>
  <span style={{ fontSize: 12 }}>副标题</span>
</div>
```

**正例**：
```jsx
// ✅ 使用 Space 组件自动对齐
<Space align="baseline">
  <span style={{ fontSize: 20 }}>标题</span>
  <span style={{ fontSize: 12, color: '#86909C' }}>副标题</span>
</Space>

// 或 Flex 对齐
<div style={{ display: 'flex', alignItems: 'baseline', gap: 8 }}>
  <span style={{ fontSize: 20 }}>标题</span>
  <span style={{ fontSize: 12, color: '#86909C' }}>副标题</span>
</div>
```

---

## 常见错误

### ❌ 错误 1：字号小于 12px

```css
/* ❌ 过小，难以阅读 */
.helper-text {
  font-size: 10px;
}

/* ✅ 最小 12px */
.helper-text {
  font-size: 12px;
  color: #86909C;  /* 用颜色弱化 */
}
```

### ❌ 错误 2：标题字重过轻

```css
/* ❌ 标题字重太轻，没有层级 */
.title {
  font-size: 20px;
  font-weight: 400;
}

/* ✅ 标题使用 Semibold */
.title {
  font-size: 20px;
  font-weight: 600;
}
```

### ❌ 错误 3：行高过小

```css
/* ❌ 行高太小，挤在一起 */
.paragraph {
  font-size: 14px;
  line-height: 1.2;
}

/* ✅ 合适的行高 */
.paragraph {
  font-size: 14px;
  line-height: 1.6;
}
```

### ❌ 错误 4：忽略字体回退

```css
/* ❌ 没有回退字体 */
body {
  font-family: 'Nunito';
}

/* ✅ 完整的字体栈 */
body {
  font-family: 'Nunito', 'Helvetica Neue', Helvetica, 'PingFang SC', 'Hiragino Sans GB', 'Microsoft YaHei', Arial, sans-serif;
}
```

---

## 检查清单

设计审查时检查：

- [ ] 主字号是否为 14px？
- [ ] 字号层级是否控制在 3-5 种？
- [ ] 是否使用字重（400/500/600）而非字号来强调？
- [ ] 行高是否合适（默认 1.4，中文长文 1.5-1.8）？
- [ ] 标题字重是否为 500 或 600？
- [ ] 辅助文字是否使用 12px + Grey-6？
- [ ] 字体栈是否包含中文回退？
- [ ] 不同字号元素是否对齐基线？
