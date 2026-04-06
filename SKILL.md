---
name: arco-design-guide
description: Arco Design 设计系统指导与审查。当用户需要设计企业级中后台界面、使用字节跳动 Arco Design 组件库、遵循务实浪漫的设计哲学、或审查现有 UI 是否符合 Arco 规范时触发。支持生成符合 Arco 规范的页面设计指导和代码，以及审查现有设计/截图/代码的问题并提供可操作的修复方案。
compatibility: web, react, vue
---

# Arco Design 指导与审查 Skill

## 概述

Arco Design 是字节跳动出品的企业级设计系统，核心理念是**"务实的浪漫主义"**。

**务实** = 同理心，解决实际问题  
**浪漫** = 想象力，注入美感与韵律

这个 skill 提供两个核心能力：
- **Guide（指导）**：为现代简洁的 UI/UX 提供设计原则和具体操作规则
- **Review（审查）**：审查现有界面并输出优先级明确、可操作的修复方案

---

## 何时使用此 Skill

**必须触发的情况：**
- 用户提到 "Arco Design"、"字节跳动组件库"、"arco"
- 用户要求设计"中后台管理系统"、"企业级产品"、"B端界面"
- 用户要求审查/检查/评估现有 UI 是否符合设计规范
- 用户需要设计原则指导或禁忌规则

**应该触发的情况：**
- 设计 React/Vue 管理后台界面
- 需要现代化、简洁的企业级 UI 方案
- 用户上传了 UI 截图或代码要求评审

---

## 核心设计价值观

### 四大价值观

| 价值观 | 含义 | 实践原则 |
|--------|------|----------|
| **清晰** Clear | 减少不确定因素，明确信息层级 | 操作流程一步到位，信息表意明确 |
| **一致** Consistent | 样式规范、操作流程高度统一 | 降低用户学习成本，建立品牌信赖感 |
| **韵律** Rhythm | 信息模块排版有规律美感 | 重复与对比的规律，减少记忆负担 |
| **开放** Open | 灵活可配置，适应复杂业务 | 在可配置范围内灵活调整设计模型 |

### 八大设计原则

1. **及时反馈** - 让用户知道当前状态
2. **贴近现实** - 使用用户的语言和熟悉的概念
3. **系统一致性** - 同一用语、功能、操作保持一致
4. **防止错误** - 用心设计防止问题发生
5. **遵从习惯** - 减少记忆负荷，动作和选项可见
6. **突出重点** - 用户是"扫"而非"读"
7. **错误帮助** - 用语言准确反映问题并提供解决方案
8. **人性化帮助** - 最佳帮助是无需提示

---

## 快速决策指南

### 颜色选择

**主色调：**
- 默认主色：`#165DFF`（极致蓝）
- 主按钮、链接、高亮状态使用 Primary-6
- Hover 状态使用 Primary-5
- 点击状态使用 Primary-7
- 禁用状态使用 Primary-3

**中性色：**
- 正文：`#1D2129`（grey-10）
- 次要文字：`#4E5969`（grey-8）
- 占位文字：`#86909C`（grey-6）
- 边框：`#E5E6EB`（grey-3）
- 背景：`#F7F8FA`（grey-1）

**功能色：**
- 成功：`#00B42A`（绿色）
- 警告：`#FF7D00`（橙色）
- 错误：`#F53F3F`（红色）
- 链接：`#165DFF`（主色）

### 字体排版

**字体栈：**
```
'Nunito', 'Helvetica Neue', Helvetica, 'PingFang SC', 'Hiragino Sans GB', 'Microsoft YaHei', Arial, sans-serif
```

**字号规范：**
- 主字号：**14px**（正文、表单）
- 最小字号：**12px**（辅助信息、时间戳）
- 标题层级差距：2-4px
- 同一产品使用 **3-5 种** 字号层级

**行高：**
- 默认：**1.4 倍** 字号
- 中文长文本：1.5-2 倍
- 标题：较小行高（32px-44px）

**强调方式：**
- ✅ 优先使用**字重变化**（Regular 400 → Medium 500 → Semibold 600）
- ❌ 避免使用字号变化来强调

### 间距系统

**基础单位：4px**

| Token | 值 | 使用场景 |
|-------|-----|----------|
| spacing-mini | 4px | 图标与文字间、紧凑内联元素 |
| spacing-small | 8px | 相关元素间、按钮内边距 |
| spacing-medium | 16px | 卡片内边距、表单字段间距 |
| spacing-large | 24px | 模块间距、区块分隔 |
| spacing-xlarge | 32px | 大模块间、页面边距 |

**间距原则：**
- 小间距用于相关元素（表单标签与输入框）
- 大间距用于不同模块（表格与筛选区）
- 通过间距大小暗示信息层级关系

### 组件层级

**按钮层级：**
1. **Primary** - 每页最多1个，核心操作（保存、提交）
2. **Secondary/Default** - 次要操作（取消、返回）
3. **Dashed** - 添加/新建类操作
4. **Text** - 最弱层级（链接、查看更多）

**禁忌：**
- ❌ 同一区域多个 Primary 按钮
- ❌ 禁用按钮没有说明原因
- ❌ 按钮文案使用「确定/取消」等模糊词汇

---

## Guide 模式：设计指导

当用户需要设计新界面时，遵循以下流程：

### 1. 确认场景类型

**常见中后台页面类型：**
- **列表页** - 数据查询、筛选、批量操作
- **表单页** - 数据录入、验证、提交
- **详情页** - 信息展示、卡片分组
- **Dashboard** - 数据可视化、关键指标
- **结果页** - 成功/失败/空状态反馈

### 2. 提供设计建议

根据场景输出：
- **布局建议** - 24列栅格如何分配
- **组件选择** - 推荐使用哪些 Arco 组件
- **交互模式** - 表单验证、表格操作、弹窗确认等
- **代码示例** - 核心组件的 JSX/Vue 代码

### 3. 引用详细规范

复杂场景下阅读参考文档：
- [设计原则](references/principles.md) - 四大价值观、八大原则
- [颜色系统](references/color-system.md) - 完整色板、使用规则
- [字体排版](references/typography.md) - 字号、行高、字重
- [间距布局](references/spacing-layout.md) - 间距、栅格、响应式
- [组件使用](references/components.md) - 各组件最佳实践
- [常见模式](references/patterns.md) - 典型页面模式

---

## Review 模式：界面审查

当用户上传截图、代码或描述现有界面时，执行审查流程：

### 1. 收集信息

请用户提供：
- 页面截图或 Figma/设计稿链接
- 页面类型（列表/表单/详情/Dashboard）
- 目标用户和使用场景
- 代码片段（如有）

### 2. 执行审查检查

使用 [审查清单](references/review-checklist.md) 逐项检查：

**颜色检查：**
- [ ] 是否使用 Arco 标准色板？
- [ ] 主色使用是否正确（Primary-6 为主，5为hover，7为active）？
- [ ] 文字对比度是否符合 WCAG AA 标准？
- [ ] 禁用状态是否使用对应色阶（Primary-3）？

**排版检查：**
- [ ] 主字号是否为 14px？
- [ ] 字号层级是否控制在 3-5 种？
- [ ] 是否使用字重而非字号来强调？
- [ ] 行高是否合适（默认 1.4，中文长文 1.5-2）？

**间距检查：**
- [ ] 间距是否为 4px 的倍数？
- [ ] 是否通过间距大小区分信息层级？
- [ ] 模块间距是否大于元素间距？

**组件检查：**
- [ ] 按钮层级是否正确（Primary 是否过多）？
- [ ] 表单标签对齐方式是否一致？
- [ ] 表格是否设置 rowKey？
- [ ] 操作是否有及时反馈（loading、toast）？

**交互检查：**
- [ ] 是否遵循及时反馈原则？
- [ ] 错误处理是否完善？
- [ ] 是否符合用户心智模型？

### 3. 输出审查报告

**报告结构：**

```markdown
# Arco Design 审查报告

## 概述
- 页面类型：XXX
- 审查日期：XXX
- 问题总数：X 个（严重：X，中等：X，建议：X）

## 严重问题（必须修复）
### 1. [问题名称]
- **位置**：截图/代码位置
- **问题描述**：违反的规范
- **影响**：用户体验问题
- **修复方案**：具体修改建议
- **参考**：相关文档链接

## 中等问题（建议修复）
...

## 优化建议
...

## 符合规范的亮点
- 列举做得好的地方
```

### 4. 优先级排序

**P0 - 严重问题：**
- 违反四大价值观（清晰、一致、韵律、开放）
- 可用性问题（用户无法完成任务）
- 可访问性问题（对比度不足、无焦点状态）

**P1 - 中等问题：**
- 违反八大设计原则
- 组件使用不当
- 间距/颜色使用不规范

**P2 - 建议：**
- 可以进一步优化的地方
- 符合规范但可以提升体验

---

## 常见页面模式

### 列表页模式

**布局结构：**
```
[筛选区] - 表单元素横向排列，16px 间距
[操作栏] - 主要按钮在左，次要按钮在右
[表格区] - 24列栅格占满
[分页] - 右对齐，24px 上边距
```

**组件组合：**
- Input + Select + DatePicker + Button（筛选）
- Button（新建/导出）+ Table（数据）
- Pagination（分页）

**代码示例：**
```jsx
import { Form, Input, Button, Table, Space } from '@arco-design/web-react';

// 筛选区
<Form layout="inline">
  <Space size={16}>
    <Form.Item field="name" label="名称">
      <Input placeholder="请输入" />
    </Form.Item>
    <Button type="primary">查询</Button>
    <Button>重置</Button>
  </Space>
</Form>

// 表格
<Table
  rowKey="id"
  columns={columns}
  data={data}
  pagination={{ pageSize: 20 }}
/>
```

### 表单页模式

**布局结构：**
```
[标题区] - 页面标题 + 描述 + 操作按钮
[表单区] - 最大宽度 800px，水平居中
[底部操作] - 固定底部或跟随表单
```

**表单布局：**
- 简单表单：单列（label 右对齐或上对齐）
- 复杂表单：多列栅格（2-3列）
- 分组表单：使用 Card 或 Divider 分组

**验证模式：**
- 即时验证：失焦时验证（onBlur）
- 提交验证：点击提交时全量验证
- 异步验证：用户名/邮箱唯一性检查（带防抖）

### Dashboard 模式

**布局结构：**
```
[指标卡片区] - 4列栅格，关键指标
[图表区] - 8-16列，趋势图/饼图
[列表区] - 8-16列，待办/动态
```

**设计原则：**
- 信息密度适中，避免过多数据
- 使用卡片容器分组相关内容
- 关键数据突出显示（字重或颜色）

---

## 代码生成规范

当生成 Arco Design 代码时，遵循以下规范：

### 1. 导入规范

```jsx
// ✅ 推荐：按组件导入
import { Button, Form, Input, Table } from '@arco-design/web-react';

// ✅ 推荐：导入样式
import '@arco-design/web-react/dist/css/arco.css';
```

### 2. 组件使用

```jsx
// ✅ 按钮层级清晰
<Space>
  <Button type="primary">保存</Button>
  <Button>取消</Button>
</Space>

// ✅ 表单字段带验证
<Form.Item
  label="用户名"
  field="username"
  rules={[{ required: true, message: '请输入用户名' }]}
>
  <Input placeholder="请输入用户名" />
</Form.Item>

// ✅ 表格设置 rowKey
<Table rowKey="id" columns={columns} data={data} />
```

### 3. 样式规范

```jsx
// ✅ 使用 Space 组件控制间距
<Space size="large">
  <Button>按钮1</Button>
  <Button>按钮2</Button>
</Space>

// ✅ 使用 Grid 布局
<Row gutter={24}>
  <Col span={12}>...</Col>
  <Col span={12}>...</Col>
</Row>
```

---

## 错误排查指南

### 常见问题

**Q: 为什么我的按钮颜色不对？**  
A: 检查是否导入了 Arco 样式文件：`import '@arco-design/web-react/dist/css/arco.css'`

**Q: Modal 内表单验证不生效？**  
A: 确保在 Modal 的 onOk 回调中手动调用 `form.validate()`，并返回 Promise 阻止关闭

**Q: 表格选中状态在翻页后丢失？**  
A: 设置 `preserveSelectedRowKeys={true}`

**Q: Switch 组件值绑定不生效？**  
A: 设置 `triggerPropName="checked"`

---

## 参考资源

- **官方网站**：https://arco.design
- **React 组件文档**：https://arco.design/react/docs/start
- **Vue 组件文档**：https://arco.design/vue/docs/start
- **设计规范**：https://arco.design/docs/spec/philosophy
- **颜色工具**：https://arco.design/palette
- **Arco Pro**：https://pro.arco.design

---

## Skill 更新日志

- **v1.0** - 初始版本，包含四大价值观、八大原则、颜色/字体/间距规范、核心组件最佳实践