# Arco Design 间距与布局

## 间距系统

### 基础单位

**基础间距：4px**

所有间距都应该是 4px 的倍数，形成和谐的视觉韵律。

### 间距 Token

| Token | 值 | 计算 | 使用场景 |
|-------|-----|------|----------|
| spacing-mini | 4px | 1×4 | 图标与文字间、紧凑内联元素 |
| spacing-small | 8px | 2×4 | 相关元素间、按钮内边距 |
| spacing-medium | 16px | 4×4 | 卡片内边距、表单字段间距 |
| spacing-large | 24px | 6×4 | 模块间距、区块分隔 |
| spacing-xlarge | 32px | 8×4 | 大模块间、页面边距 |

### Space 组件

Arco 提供专门的 `Space` 组件控制元素间距：

```jsx
import { Space, Button } from '@arco-design/web-react';

// 水平间距（默认）
<Space size="small">
  <Button>按钮1</Button>
  <Button>按钮2</Button>
</Space>

// 垂直间距
<Space direction="vertical" size="medium">
  <Button>按钮1</Button>
  <Button>按钮2</Button>
</Space>

// 自定义数值
<Space size={20}>
  <Button>按钮1</Button>
  <Button>按钮2</Button>
</Space>

// 换行间距 [水平, 垂直]
<Space wrap size={[16, 12]}>
  {items.map(item => <Tag key={item}>{item}</Tag>)}
</Space>

// 对齐方式
<Space align="center">       {/* 居中对齐 */}
<Space align="start">        {/* 顶部对齐 */}
<Space align="end">          {/* 底部对齐 */}
<Space align="baseline">     {/* 基线对齐（文字） */}
```

### 间距使用原则

**1. 格式塔心理学原则**

通过间距大小暗示信息层级关系：

| 间距大小 | 关系暗示 | 示例 |
|----------|----------|------|
| 4-8px | 紧密相关 | 图标+文字、标签+输入框 |
| 16px | 相关元素 | 表单字段间、按钮组内 |
| 24-32px | 不同模块 | 卡片间、表格与筛选区间 |
| 40px+ | 区块分隔 | 页面区块、大模块间 |

**2. 内边距规范**

| 组件 | 内边距 | 说明 |
|------|--------|------|
| 小型按钮 | 4px 12px | 紧凑操作 |
| 默认按钮 | 6px 16px | 常规操作 |
| 大型按钮 | 8px 20px | 突出操作 |
| 卡片 | 16px / 24px | 内容区域 |
| 表格单元格 | 12px 16px | 数据展示 |
| 输入框 | 4px 12px | 表单输入 |
| 弹窗 | 24px | 内容区 |

**代码示例：**
```jsx
// ✅ 卡片内边距
<Card style={{ padding: 24 }}>
  <Space direction="vertical" size={16} style={{ width: '100%' }}>
    <div>内容区块 1</div>
    <div>内容区块 2</div>
  </Space>
</Card>
```

---

## 栅格系统

### 24 列栅格

Arco 使用 24 列响应式栅格系统：

```jsx
import { Grid } from '@arco-design/web-react';
const { Row, Col } = Grid;

// 基础布局
<Row>
  <Col span={12}>占一半</Col>
  <Col span={12}>占一半</Col>
</Row>

// 三列布局
<Row gutter={24}>
  <Col span={8}>1/3</Col>
  <Col span={8}>1/3</Col>
  <Col span={8}>1/3</Col>
</Row>

// 四列布局
<Row gutter={24}>
  <Col span={6}>1/4</Col>
  <Col span={6}>1/4</Col>
  <Col span={6}>1/4</Col>
  <Col span={6}>1/4</Col>
</Row>
```

### 响应式断点

| 断点 | 尺寸 | 说明 |
|------|------|------|
| xs | < 576px | 超小屏幕（手机） |
| sm | ≥ 576px | 小屏幕（大手机） |
| md | ≥ 768px | 中等屏幕（平板） |
| lg | ≥ 992px | 大屏幕（笔记本） |
| xl | ≥ 1200px | 超大屏幕（桌面） |
| xxl | ≥ 1600px | 特大屏幕（大屏） |

**响应式栅格：**
```jsx
<Row gutter={{ xs: 8, sm: 16, md: 24, lg: 32 }}>
  <Col xs={24} sm={12} md={8} lg={6}>
    响应式列
  </Col>
</Row>
```

### 间距（Gutter）

```jsx
// 水平间距
<Row gutter={24}>
  <Col span={12}>...</Col>
  <Col span={12}>...</Col>
</Row>

// 响应式间距
<Row gutter={{ md: 8, lg: 24, xl: 32 }}>
  ...
</Row>

// 水平和垂直间距 [水平, 垂直]
<Row gutter={[24, 16]}>
  <Col span={6}>...</Col>
  <Col span={6}>...</Col>
  <Col span={6}>...</Col>
  <Col span={6}>...</Col>
</Row>
```

### 偏移（Offset）

```jsx
// 左侧偏移
<Row>
  <Col span={12} offset={6}>居中（偏移6列）</Col>
</Row>

// Flex 自动填充
<Row>
  <Col flex="auto">自动填充</Col>
  <Col flex="200px">固定200px</Col>
</Row>
```

### 水平对齐

```jsx
<Row justify="start">      {/* 左对齐（默认） */}
<Row justify="center">     {/* 居中 */}
<Row justify="end">        {/* 右对齐 */}
<Row justify="space-between"> {/* 两端对齐 */}
<Row justify="space-around">  {/* 等分间距 */}
```

---

## 布局组件

### Layout 页面布局

```jsx
import { Layout } from '@arco-design/web-react';
const { Header, Sider, Content, Footer } = Layout;

// 经典布局：顶部导航 + 侧边栏 + 内容
<Layout>
  <Header>顶部导航</Header>
  <Layout>
    <Sider width={220}>侧边栏</Sider>
    <Content style={{ padding: 24 }}>
      页面内容
    </Content>
  </Layout>
</Layout>

// 只有顶部导航
<Layout>
  <Header>顶部导航</Header>
  <Content style={{ padding: 24 }}>
    页面内容
  </Content>
  <Footer>页脚</Footer>
</Layout>
```

### 表单布局

**水平布局（默认）：**
```jsx
<Form layout="horizontal">
  <Form.Item label="用户名">
    <Input />
  </Form.Item>
</Form>
```

**垂直布局：**
```jsx
<Form layout="vertical">
  <Form.Item label="用户名">
    <Input />
  </Form.Item>
</Form>
```

**内联布局：**
```jsx
<Form layout="inline">
  <Form.Item label="用户名">
    <Input />
  </Form.Item>
  <Button type="primary">查询</Button>
</Form>
```

**栅格表单：**
```jsx
<Row gutter={24}>
  <Col span={12}>
    <Form.Item label="姓">
      <Input />
    </Form.Item>
  </Col>
  <Col span={12}>
    <Form.Item label="名">
      <Input />
    </Form.Item>
  </Col>
</Row>
```

---

## 常见布局模式

### 1. 列表页布局

```
┌─────────────────────────────────────────┐
│ [筛选区]  表单元素横向排列，16px 间距      │
├─────────────────────────────────────────┤
│ [操作栏]  主要按钮在左，次要按钮在右      │
├─────────────────────────────────────────┤
│                                         │
│ [表格区]  24列栅格占满                   │
│                                         │
├─────────────────────────────────────────┤
│ [分页]    右对齐，24px 上边距            │
└─────────────────────────────────────────┘
```

**代码：**
```jsx
<div style={{ padding: 24 }}>
  {/* 筛选区 */}
  <Form layout="inline">
    <Space size={16}>
      <Form.Item label="名称">
        <Input placeholder="请输入" />
      </Form.Item>
      <Button type="primary">查询</Button>
    </Space>
  </Form>

  {/* 操作栏 */}
  <div style={{ margin: '16px 0' }}>
    <Button type="primary">新建</Button>
  </div>

  {/* 表格 */}
  <Table columns={columns} data={data} />

  {/* 分页 */}
  <div style={{ marginTop: 24, textAlign: 'right' }}>
    <Pagination total={100} />
  </div>
</div>
```

### 2. 表单页布局

```
┌─────────────────────────────────────────┐
│ 页面标题                                    │
│ 页面描述...                                │
├─────────────────────────────────────────┤
│                                         │
│ ┌───────────────────────────────────┐   │
│ │ 表单内容（最大宽度 800px）            │   │
│ │ 居中对齐                              │   │
│ └───────────────────────────────────┘   │
│                                         │
│         [保存] [取消]                     │
└─────────────────────────────────────────┘
```

**代码：**
```jsx
<div style={{ maxWidth: 800, margin: '0 auto', padding: 24 }}>
  <Typography.Title heading={3} style={{ marginBottom: 8 }}>
    新建用户
  </Typography.Title>
  <Typography.Text type="secondary" style={{ marginBottom: 24, display: 'block' }}>
    填写以下信息创建新用户
  </Typography.Text>

  <Form layout="vertical">
    <Form.Item label="用户名" required>
      <Input placeholder="请输入用户名" />
    </Form.Item>
    <Form.Item label="邮箱" required>
      <Input placeholder="请输入邮箱" />
    </Form.Item>
    
    <Space style={{ marginTop: 24 }}>
      <Button type="primary">保存</Button>
      <Button>取消</Button>
    </Space>
  </Form>
</div>
```

### 3. Dashboard 布局

```
┌───────┬───────┬───────┬───────┐
│ 指标1  │ 指标2  │ 指标3  │ 指标4  │  ← 4列指标卡
├───────┴───────┴───────┴───────┤
│                               │
│          趋势图表               │  ← 占满
│                               │
├──────────────────┬────────────┤
│                  │            │
│    最近动态       │  待办事项   │  ← 8+16 或 12+12
│                  │            │
└──────────────────┴────────────┘
```

**代码：**
```jsx
<div style={{ padding: 24 }}>
  {/* 指标卡片 */}
  <Row gutter={16}>
    <Col span={6}>
      <Card><Statistic title="用户数" value={1234} /></Card>
    </Col>
    <Col span={6}>
      <Card><Statistic title="订单数" value={567} /></Card>
    </Col>
    <Col span={6}>
      <Card><Statistic title="收入" value={89000} /></Card>
    </Col>
    <Col span={6}>
      <Card><Statistic title="转化率" value={12.5} suffix="%" /></Card>
    </Col>
  </Row>

  {/* 图表区 */}
  <Card style={{ marginTop: 16 }}>
    <Chart />
  </Card>

  {/* 底部列表 */}
  <Row gutter={16} style={{ marginTop: 16 }}>
    <Col span={12}>
      <Card title="最近动态"><List /></Card>
    </Col>
    <Col span={12}>
      <Card title="待办事项"><List /></Card>
    </Col>
  </Row>
</div>
```

---

## 设计原则

### 1. 韵律感

通过 4px 基数的倍数创建视觉韵律：

```css
/* ✅ 和谐 */
.card { padding: 24px; }      /* 6×4 */
.title { margin-bottom: 16px; } /* 4×4 */
.item { margin-bottom: 8px; }   /* 2×4 */

/* ❌ 混乱 */
.card { padding: 23px; }      /* 不是 4 的倍数 */
.title { margin-bottom: 15px; }
.item { margin-bottom: 7px; }
```

### 2. 亲密性

相关元素间距小，不相关元素间距大：

```jsx
// ✅ 相关元素间距 8px
<Space size="small" direction="vertical">
  <label>用户名</label>
  <Input />
  <span style={{ fontSize: 12, color: '#86909C' }}>提示文字</span>
</Space>

// ✅ 不同模块间距 24px
<Space size="large" direction="vertical" style={{ width: '100%' }}>
  <div>模块 1</div>
  <div>模块 2</div>
</Space>
```

### 3. 对齐一致性

同一页面保持对齐方式一致：

```jsx
// ✅ 表单标签全部右对齐或全部上对齐
<Form layout="horizontal">  {/* 全部水平 */}
  <Form.Item label="字段1">...</Form.Item>
  <Form.Item label="字段2">...</Form.Item>
</Form>

// ❌ 混合对齐
<Form.Item label="字段1" style={{ labelPosition: 'left' }}>...</Form.Item>
<Form.Item label="字段2" style={{ labelPosition: 'top' }}>...</Form.Item>
```

---

## 检查清单

设计审查时检查：

- [ ] 间距是否都是 4px 的倍数？
- [ ] 是否使用 Space 组件控制元素间距？
- [ ] 模块间距是否大于元素间距？
- [ ] 表单布局是否统一（水平/垂直）？
- [ ] 页面边距是否一致（通常 24px）？
- [ ] 响应式断点是否覆盖目标设备？
- [ ] 对齐方式是否一致？
- [ ] 卡片内边距是否规范（16/24px）？
