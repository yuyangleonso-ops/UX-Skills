# Arco Design 颜色系统

## 颜色分类

Arco Design 将颜色分为 **四大类**：

| 分类 | 用途 | 示例 |
|------|------|------|
| **主色** | 品牌代表，核心交互 | Primary-6: #165DFF |
| **中性色** | 视觉层级，文字/背景 | Grey-6: #86909C |
| **功能色** | 状态传达 | 成功、警告、错误、链接 |
| **遮罩色** | 弹窗遮罩背景 | 黑色 60% 透明度 |

---

## 主色系统

### 默认主色

**Arco Blue（极致蓝）**：`#165DFF`

这是 Arco Design 的默认品牌色，代表专业、科技、可信赖。

### 完整色板

每个主色生成 **10 级色板**（1-10），使用动态梯度算法：

#### Arco Blue 色板

| 级别 | 色值 | 对比度 | 用途 |
|------|------|--------|------|
| Primary-1 | `#E8F3FF` | AAA | 浅色背景、hover 浅背景 |
| Primary-2 | `#BEDAFF` | AAA | 禁用文字背景 |
| Primary-3 | `#94BFFF` | AAA | 一般禁用状态 |
| Primary-4 | `#6AA1FF` | AAA | 特殊场景 |
| Primary-5 | `#4080FF` | AA | **Hover 状态** |
| Primary-6 | `#165DFF` | AA | **基础/常规（主色）** |
| Primary-7 | `#0E42D2` | AAA | **点击/激活状态** |
| Primary-8 | `#072CA6` | AAA | 深色强调 |
| Primary-9 | `#031A79` | AAA | 深色背景 |
| Primary-10 | `#000D4D` | AAA | 最深色 |

### 其他可选主色

| 名称 | 色值 | 气质 |
|------|------|------|
| 极致蓝 | `#165DFF` | 科技、专业（默认） |
| 暗夜紫 | `#722ED1` | 神秘、高端 |
| 青春紫 | `#D91AD9` | 活力、创意 |
| 品红 | `#F5319D` | 时尚、女性 |
| 成功绿 | `#00B42A` | 正向、健康 |
| 活力橙 | `#FF7D00` | 活力、促销 |
| 警戒红 | `#F53F3F` | 警示、重要 |
| 明青 | `#14C9C9` | 清新、现代 |

---

## 中性色系统（灰度）

中性色用于创建视觉层级，基于 **Grey-6: #86909C**

| 级别 | 色值 | 用途 |
|------|------|------|
| Grey-1 | `#F7F8FA` | 页面背景、卡片背景 |
| Grey-2 | `#F2F3F5` | 次级背景、hover 背景 |
| Grey-3 | `#E5E6EB` | 边框、分割线 |
| Grey-4 | `#C9CDD4` | 禁用边框 |
| Grey-5 | `#AEB5BE` | 占位符、禁用文字 |
| Grey-6 | `#86909C` | **中性色基础** |
| Grey-7 | `#6B7785` | 次要图标 |
| Grey-8 | `#4E5969` | **次要文字** |
| Grey-9 | `#272E3B` | 标题文字 |
| Grey-10 | `#1D2129` | **主要文字** |

### 中性色应用规范

| 场景 | 推荐色值 | 说明 |
|------|----------|------|
| 主要文字 | Grey-10 (#1D2129) | 正文、标题 |
| 次要文字 | Grey-8 (#4E5969) | 描述、辅助信息 |
| 占位文字 | Grey-5 (#AEB5BE) | placeholder |
| 禁用文字 | Grey-5 (#AEB5BE) | disabled 状态 |
| 边框 | Grey-3 (#E5E6EB) | 输入框边框、分割线 |
| 深色背景 | Grey-1 (#F7F8FA) | 页面背景 |
| 卡片背景 | `#FFFFFF` | 白色卡片 |
| 悬停背景 | Grey-2 (#F2F3F5) | hover 状态 |

---

## 功能色系统

功能色用于传达特定状态，与主色独立。

### 成功色（Success）

| 级别 | 色值 | 用途 |
|------|------|------|
| Success-1 | `#E8FFEA` | 成功状态浅背景 |
| Success-2 | `#AFF0B5` | - |
| Success-3 | `#7BE188` | - |
| Success-4 | `#4CD263` | - |
| Success-5 | `#23C343` | - |
| Success-6 | `#00B42A` | **成功主色** |
| Success-7 | `#009A29` | 点击状态 |
| Success-8 | `#008026` | - |
| Success-9 | `#006622` | - |
| Success-10 | `#004D1C` | - |

**使用场景**：操作成功提示、成功状态标签、正向数据趋势

### 警告色（Warning）

| 级别 | 色值 | 用途 |
|------|------|------|
| Warning-1 | `#FFF7E8` | 警告状态浅背景 |
| Warning-2 | `#FFE4BA` | - |
| Warning-3 | `#FFCF8B` | - |
| Warning-4 | `#FFB65D` | - |
| Warning-5 | `#FF9F2E` | - |
| Warning-6 | `#FF7D00` | **警告主色** |
| Warning-7 | `#D25F00` | 点击状态 |
| Warning-8 | `#A64500` | - |
| Warning-9 | `#792E00` | - |
| Warning-10 | `#4D1B00` | - |

**使用场景**：警告提示、需要关注的信息、中等风险操作

### 错误色（Danger/Error）

| 级别 | 色值 | 用途 |
|------|------|------|
| Danger-1 | `#FFECE8` | 错误状态浅背景 |
| Danger-2 | `#FDCDC5` | 错误轻背景 |
| Danger-3 | `#FBACA3` | - |
| Danger-4 | `#F98981` | - |
| Danger-5 | `#F76560` | - |
| Danger-6 | `#F53F3F` | **错误主色** |
| Danger-7 | `#CB2E34` | 点击状态 |
| Danger-8 | `#A11F2B` | - |
| Danger-9 | `#771325` | - |
| Danger-10 | `#4D0A1E` | - |

**使用场景**：错误提示、删除操作、校验失败、高风险警告

### 链接色（Link）

| 状态 | 色值 | 说明 |
|------|------|------|
| 默认 | `#165DFF` | 使用主色 |
| Hover | `#4080FF` | Primary-5 |
| 已访问 | `#0E42D2` | Primary-7 |
| 禁用 | `#AEB5BE` | Grey-5 |

---

## 颜色使用规则

### 主色使用规范

**按钮状态：**

| 状态 | 色值 | Token |
|------|------|-------|
| 默认 | `#165DFF` | Primary-6 |
| Hover | `#4080FF` | Primary-5 |
| 点击/激活 | `#0E42D2` | Primary-7 |
| 禁用 | `#94BFFF` | Primary-3 |
| 轻背景 | `#E8F3FF` | Primary-1 |

**代码示例：**
```jsx
// ✅ 正确：使用标准色阶
<Button type="primary">默认</Button>              // Primary-6
<Button type="primary" disabled>禁用</Button>     // Primary-3

// 自定义样式时
.custom-button:hover {
  background-color: #4080FF;  // Primary-5
}
.custom-button:active {
  background-color: #0E42D2;  // Primary-7
}
```

### 文字颜色规范

| 层级 | 色值 | 用途 |
|------|------|------|
| 主要文字 | `#1D2129` | 正文、标题 |
| 次要文字 | `#4E5969` | 描述、辅助 |
| 辅助文字 | `#86909C` | 时间戳、占位 |
| 禁用文字 | `#AEB5BE` | disabled 状态 |

**代码示例：**
```jsx
// ✅ 正确
<Text style={{ color: '#1D2129' }}>主要文字</Text>
<Text style={{ color: '#4E5969' }}>描述信息</Text>
<Text style={{ color: '#86909C' }}>2024-01-01</Text>
<Text style={{ color: '#AEB5BE' }}>已禁用</Text>
```

### 背景与边框

| 场景 | 色值 | Token |
|------|------|-------|
| 页面背景 | `#F7F8FA` | Grey-1 |
| 卡片背景 | `#FFFFFF` | 纯白 |
| 悬停背景 | `#F2F3F5` | Grey-2 |
| 边框 | `#E5E6EB` | Grey-3 |
| 禁用边框 | `#C9CDD4` | Grey-4 |
| 分割线 | `#E5E6EB` | Grey-3 |

---

## 可访问性（Accessibility）

### 对比度标准

Arco Design 所有颜色组合均满足 **WCAG 2.1 AA 标准**：

| 组合 | 对比度 | 等级 |
|------|--------|------|
| 白底 + Grey-10 文字 | 14.5:1 | AAA |
| 白底 + Grey-8 文字 | 8.6:1 | AAA |
| 白底 + Primary-6 | 5.2:1 | AA |
| Primary-1 背景 + Primary-7 文字 | 7.1:1 | AA |

### 禁止使用的颜色组合

| 组合 | 问题 | 解决方案 |
|------|------|----------|
| 白底 + Grey-5 | 对比度不足 (2.1:1) | 使用 Grey-8 或更深的颜色 |
| Primary-3 + 白字 | 对比度不足 | 使用 Primary-6 |
| Warning-1 + Warning-6 | 对比度不足 | Warning-1 + Warning-8 |

---

## 颜色工具

### 在线调色板工具

**URL**: https://arco.design/palette

功能：
- 从任意品牌色生成 10 级色板
- 实时预览对比度评级（AAA/AA）
- 支持亮/暗主题预览

### NPM 包

```bash
npm install @arco-design/color
```

**使用示例：**
```javascript
import { generate, getPresetColors } from '@arco-design/color';

// 从基础色生成 10 级色板
const palette = generate('#165DFF', { list: true });
// ['#E8F3FF', '#BEDAFF', '#94BFFF', '#6AA1FF', '#4080FF', '#165DFF', '#0E42D2', '#072CA6', '#031A79', '#000D4D']

// 获取所有预设颜色
const presetColors = getPresetColors();
// 包含 14 种预设颜色的完整色板

// 暗色主题
const darkPalette = generate('#165DFF', { list: true, dark: true });
```

---

## 常见错误

### ❌ 错误 1：直接使用色板外的颜色

```css
/* 错误：使用非标准颜色 */
.button {
  background-color: #1890ff;  /* Ant Design 的主色！ */
}

/* 正确：使用 Arco 标准色 */
.button {
  background-color: #165DFF;  /* Arco Primary-6 */
}
```

### ❌ 错误 2：hover 状态颜色跳跃

```css
/* 错误：hover 颜色比默认色更深 */
.button:hover {
  background-color: #0E42D2;  /* 这是 active 色！ */
}

/* 正确：hover 使用 Primary-5 */
.button:hover {
  background-color: #4080FF;
}
.button:active {
  background-color: #0E42D2;
}
```

### ❌ 错误 3：禁用状态对比度不足

```css
/* 错误：禁用状态太淡 */
.button:disabled {
  background-color: #E8F3FF;  /* Primary-1，对比度不足 */
  color: #FFFFFF;
}

/* 正确：使用 Primary-3 */
.button:disabled {
  background-color: #94BFFF;  /* Primary-3 */
  color: #FFFFFF;
}
```

---

## 检查清单

设计审查时检查：

- [ ] 是否使用 Arco 标准色板（非自定义颜色）？
- [ ] 主色是否为 Primary-6 (#165DFF)？
- [ ] 文字颜色是否符合层级规范（Grey-10/8/6/5）？
- [ ] 按钮状态颜色是否正确（hover-5, active-7, disabled-3）？
- [ ] 所有颜色组合对比度是否满足 WCAG AA？
- [ ] 功能色使用是否正确（成功绿、警告橙、错误红）？
- [ ] 链接颜色是否遵循规范？
