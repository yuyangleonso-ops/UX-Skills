# Arco Design 组件使用指南

## 核心组件速查

### 按钮 Button

**类型层级：**

| 类型 | 用途 | 每页数量 | 代码 |
|------|------|----------|------|
| Primary | 核心操作（保存、提交） | 1个 | `type="primary"` |
| Secondary | 次要操作（取消、返回） | 不限 | `type="secondary"` 或不传 |
| Dashed | 添加/新建 | 不限 | `type="dashed"` |
| Outline | 次级操作（移动端常用） | 不限 | `type="outline"` |
| Text | 最弱层级（链接） | 不限 | `type="text"` |

**状态：**

| 状态 | 用法 | 示例 |
|------|------|------|
| 默认 | 常规显示 | - |
| Hover | 鼠标悬停 | Primary-5 |
| Active | 点击时 | Primary-7 |
| Loading | 异步操作 | `loading` |
| Disabled | 不可点击 | `disabled` |

**状态色（Danger/Warning/Success）：**

```jsx
<Button type="primary" status="danger">删除</Button>
<Button type="primary" status="warning">警告</Button>
<Button type="primary" status="success">成功</Button>
```

**最佳实践：**

```jsx
// ✅ 按钮层级清晰
<Space>
  <Button type="primary">保存</Button>
  <Button>取消</Button>
  <Button type="text">删除</Button>
</Space>

// ✅ 异步操作带 loading
<Button type="primary" loading={submitting} onClick={handleSubmit}>
  提交
</Button>

// ✅ 危险操作二次确认
<Button type="primary" status="danger" onClick={() => Modal.confirm({
  title: '确认删除？',
  content: '删除后不可恢复',
  onOk: handleDelete
})}>
  删除
</Button>
```

**禁忌：**
- ❌ 同一区域多个 Primary 按钮
- ❌ 禁用按钮没有说明原因
- ❌ 按钮文案使用「确定/取消」等模糊词汇

---

### 表单 Form

**布局方式：**

| 布局 | 适用场景 | 代码 |
|------|----------|------|
| 水平 | 常见表单 | `layout="horizontal"` |
| 垂直 | 复杂表单、长标签 | `layout="vertical"` |
| 内联 | 简单筛选 | `layout="inline"` |

**标签对齐：**

| 对齐 | 特点 | 推荐 |
|------|------|------|
| 右对齐 | 标签与输入框关系明确 | ⭐ 推荐 |
| 左对齐 | 标签易读 | 长标签场景 |
| 顶对齐 | 空间充裕 | 复杂表单 |

**验证模式：**

```jsx
// 即时验证（失焦时）
<Form.Item
  label="邮箱"
  field="email"
  rules={[
    { required: true, message: '请输入邮箱' },
    { type: 'email', message: '邮箱格式不正确' }
  ]}
  validateTrigger="onBlur"
>
  <Input placeholder="请输入邮箱" />
</Form.Item>

// 自定义验证
<Form.Item
  label="密码"
  field="password"
  rules={[{
    validator: (value, callback) => {
      if (value && value.length < 6) {
        callback('密码至少6位');
      } else {
        callback();
      }
    }
  }]}
>
  <Input.Password />
</Form.Item>

// 异步验证（带防抖）
<Form.Item
  label="用户名"
  field="username"
  rules={[{
    validator: async (value) => {
      if (!value) return;
      const exists = await checkUsername(value);
      if (exists) throw new Error('用户名已被占用');
    }
  }]}
>
  <Input />
</Form.Item>
```

**useForm Hook：**

```jsx
import { Form, useForm } from '@arco-design/web-react';

function MyForm() {
  const [form] = useForm();

  const handleSubmit = async () => {
    try {
      const values = await form.validate();
      console.log(values);
    } catch (error) {
      console.log('验证失败', error);
    }
  };

  return (
    <Form form={form}>
      <Form.Item label="用户名" field="username">
        <Input />
      </Form.Item>
      <Button type="primary" onClick={handleSubmit}>提交</Button>
    </Form>
  );
}
```

**特殊组件绑定：**

```jsx
// Switch 使用 checked 而非 value
<Form.Item label="启用" field="enabled" triggerPropName="checked">
  <Switch />
</Form.Item>

// 自定义组件
<Form.Item label="上传" field="file" triggerPropName="fileList">
  <Upload />
</Form.Item>
```

**最佳实践：**

```jsx
// ✅ 表单 + Modal 联动
const [form] = Form.useForm();
const [visible, setVisible] = useState(false);

<Modal
  visible={visible}
  onOk={async () => {
    try {
      const values = await form.validate();
      await submit(values);
      setVisible(false);
      form.resetFields();
    } catch (e) {
      // 验证失败，不关闭 Modal
    }
  }}
  onCancel={() => {
    setVisible(false);
    form.resetFields();
  }}
>
  <Form form={form}>
    <Form.Item label="名称" field="name" rules={[{ required: true }]}>
      <Input />
    </Form.Item>
  </Form>
</Modal>
```

---

### 表格 Table

**必传属性：**

```jsx
// ✅ 必须设置 rowKey
<Table rowKey="id" columns={columns} data={data} />

// ✅ 固定列必须设置 width
{
  title: '操作',
  fixed: 'right',
  width: 150,
  render: () => <Button>编辑</Button>
}
```

**分页配置：**

```jsx
<Table
  columns={columns}
  data={data}
  pagination={{
    pageSize: 20,
    showTotal: true,
    showJumper: true,
    showPageSize: true
  }}
/>
```

**行选择：**

```jsx
const [selectedKeys, setSelectedKeys] = useState([]);

<Table
  rowKey="id"
  columns={columns}
  data={data}
  rowSelection={{
    type: 'checkbox',  // 或 'radio'
    selectedRowKeys: selectedKeys,
    onChange: setSelectedKeys,
    preserveSelectedRowKeys: true  // 跨页保持选中
  }}
/>
```

**虚拟滚动（大数据量）：**

```jsx
<Table
  columns={columns}
  data={data}
  virtualized
  scroll={{ y: 500 }}
/>
```

**排序与筛选：**

```jsx
const columns = [
  {
    title: '姓名',
    dataIndex: 'name',
    sorter: (a, b) => a.name.localeCompare(b.name)
  },
  {
    title: '状态',
    dataIndex: 'status',
    filters: [
      { text: '启用', value: 'active' },
      { text: '禁用', value: 'inactive' }
    ],
    onFilter: (value, record) => record.status === value
  }
];

// 服务端排序筛选
<Table
  columns={columns}
  data={data}
  onChange={(pagination, sorter, filter) => {
    // 统一处理排序筛选
    fetchData({ page: pagination.current, sorter, filter });
  }}
/>
```

**最佳实践：**

```jsx
// ✅ 列表页完整模式
function ListPage() {
  const [form] = Form.useForm();
  const [data, setData] = useState([]);
  const [loading, setLoading] = useState(false);
  const [params, setParams] = useState({ page: 1, pageSize: 20 });

  const fetchData = async () => {
    setLoading(true);
    const res = await api.getList(params);
    setData(res.data);
    setLoading(false);
  };

  return (
    <div style={{ padding: 24 }}>
      {/* 筛选区 */}
      <Form form={form} layout="inline">
        <Space size={16}>
          <Form.Item label="名称" field="name">
            <Input placeholder="请输入" allowClear />
          </Form.Item>
          <Button type="primary" onClick={() => {
            setParams({ ...params, ...form.getFieldsValue(), page: 1 });
          }}>查询</Button>
          <Button onClick={() => { form.resetFields(); setParams({ page: 1, pageSize: 20 }); }}>
            重置
          </Button>
        </Space>
      </Form>

      {/* 操作栏 */}
      <div style={{ margin: '16px 0' }}>
        <Button type="primary">新建</Button>
      </div>

      {/* 表格 */}
      <Table
        rowKey="id"
        columns={columns}
        data={data}
        loading={loading}
        pagination={{
          ...params,
          total,
          onChange: (page, pageSize) => setParams({ ...params, page, pageSize })
        }}
      />
    </div>
  );
}
```

---

### 弹窗 Modal

**声明式使用：**

```jsx
const [visible, setVisible] = useState(false);

<>
  <Button onClick={() => setVisible(true)}>打开</Button>
  <Modal
    title="标题"
    visible={visible}
    onOk={() => setVisible(false)}
    onCancel={() => setVisible(false)}
  >
    内容
  </Modal>
</>
```

**命令式使用（推荐）：**

```jsx
import { Modal } from '@arco-design/web-react';

// 确认对话框
Modal.confirm({
  title: '确认删除？',
  content: '删除后不可恢复',
  onOk: async () => {
    await deleteItem();
  }
});

// 信息提示
Modal.info({ title: '提示', content: '操作成功' });
Modal.success({ title: '成功', content: '保存成功' });
Modal.warning({ title: '警告', content: '请注意' });
Modal.error({ title: '错误', content: '操作失败' });
```

**Modal + Form 最佳实践：**

```jsx
const [form] = Form.useForm();

Modal.confirm({
  title: '编辑',
  content: (
    <Form form={form}>
      <Form.Item label="名称" field="name" rules={[{ required: true }]}>
        <Input />
      </Form.Item>
    </Form>
  ),
  onOk: async () => {
    const values = await form.validate();
    await update(values);
  }
});
```

---

### 输入组件

**Input 输入框：**

```jsx
// 基础用法
<Input placeholder="请输入" />

// 前缀后缀
<Input prefix={<IconUser />} suffix="@gmail.com" />

// 搜索框
<Input.Search placeholder="搜索" onSearch={handleSearch} />

// 密码框
<Input.Password placeholder="请输入密码" />

// 字数限制
<Input maxLength={20} showWordLimit />
```

**Select 选择器：**

```jsx
// 基础用法
<Select placeholder="请选择">
  <Option value="1">选项1</Option>
  <Option value="2">选项2</Option>
</Select>

// 多选
<Select mode="multiple" placeholder="请选择">
  {options.map(opt => <Option key={opt.value} value={opt.value}>{opt.label}</Option>)}
</Select>

// 可搜索
<Select showSearch filterOption={(input, option) => 
  option.props.children.toLowerCase().includes(input.toLowerCase())
}>
  ...
</Select>

// 远程搜索
<Select
  showSearch
  onSearch={debounce(async (value) => {
    const data = await fetchOptions(value);
    setOptions(data);
  }, 300)}
>
  ...
</Select>
```

**DatePicker 日期选择：**

```jsx
// 单个日期
<DatePicker placeholder="选择日期" />

// 日期范围
<DatePicker.RangePicker />

// 带时间
<DatePicker showTime />

// 禁用日期
<DatePicker disabledDate={(current) => current.isBefore(dayjs())} />
```

---

### 数据展示组件

**Card 卡片：**

```jsx
// 基础卡片
<Card title="标题" extra={<a>更多</a>}>
  内容
</Card>

// 无边框
<Card bordered={false}>
  内容
</Card>

// 加载状态
<Card loading>
  内容
</Card>
```

**Statistic 统计数值：**

```jsx
<Statistic
  title="活跃用户"
  value={123456}
  precision={0}
  suffix="人"
  prefix={<IconUser />}
/>
```

**Tag 标签：**

```jsx
// 基础标签
<Tag>标签</Tag>

// 带颜色
<Tag color="red">红色</Tag>
<Tag color="arcoblue">主色</Tag>

// 可关闭
<Tag closable onClose={() => {}}>可关闭</Tag>
```

**Badge 徽标：**

```jsx
// 数字徽标
<Badge count={5}>
  <IconNotification />
</Badge>

// 状态点
<Badge status="success" text="运行中" />
<Badge status="error" text="异常" />
<Badge status="warning" text="警告" />
<Badge status="processing" text="处理中" />
```

---

### 导航组件

**Menu 导航菜单：**

```jsx
<Menu mode="vertical" defaultSelectedKeys={['1']}>
  <Menu.Item key="1" icon={<IconHome />}>首页</Menu.Item>
  <SubMenu key="sub1" icon={<IconUser />} title="用户管理">
    <Menu.Item key="2">用户列表</Menu.Item>
    <Menu.Item key="3">角色管理</Menu.Item>
  </SubMenu>
</Menu>
```

**Breadcrumb 面包屑：**

```jsx
<Breadcrumb>
  <Breadcrumb.Item>首页</Breadcrumb.Item>
  <Breadcrumb.Item>用户管理</Breadcrumb.Item>
  <Breadcrumb.Item>用户列表</Breadcrumb.Item>
</Breadcrumb>
```

**Tabs 标签页：**

```jsx
<Tabs defaultActiveTab="1">
  <Tabs.TabPane key="1" title="标签1">
    内容1
  </Tabs.TabPane>
  <Tabs.TabPane key="2" title="标签2">
    内容2
  </Tabs.TabPane>
</Tabs>
```

---

### 反馈组件

**Message 全局提示：**

```jsx
import { Message } from '@arco-design/web-react';

Message.success('操作成功');
Message.error('操作失败');
Message.warning('警告提示');
Message.info('信息提示');
Message.loading('加载中...');
```

**Notification 通知：**

```jsx
import { Notification } from '@arco-design/web-react';

Notification.success({
  title: '成功',
  content: '数据保存成功'
});

Notification.error({
  title: '错误',
  content: '网络连接失败'
});
```

**Spin 加载：**

```jsx
// 包裹模式
<Spin loading={loading}>
  <div>内容</div>
</Spin>

// 自定义提示
<Spin loading={loading} tip="加载中...">
  <div>内容</div>
</Spin>
```

---

## 组件组合模式

### 搜索筛选栏

```jsx
<Form layout="inline">
  <Space size={16}>
    <Form.Item label="关键词" field="keyword">
      <Input.Search placeholder="请输入" allowClear />
    </Form.Item>
    <Form.Item label="状态" field="status">
      <Select placeholder="全部" allowClear style={{ width: 120 }}>
        <Option value="active">启用</Option>
        <Option value="inactive">禁用</Option>
      </Select>
    </Form.Item>
    <Form.Item label="时间" field="dateRange">
      <DatePicker.RangePicker />
    </Form.Item>
    <Button type="primary">查询</Button>
    <Button>重置</Button>
  </Space>
</Form>
```

### 操作列

```jsx
const columns = [
  ...dataColumns,
  {
    title: '操作',
    fixed: 'right',
    width: 180,
    render: (_, record) => (
      <Space size="small">
        <Button type="text" onClick={() => handleEdit(record)}>编辑</Button>
        <Button type="text" onClick={() => handleView(record)}>查看</Button>
        <Popconfirm
          title="确认删除？"
          onOk={() => handleDelete(record)}
        >
          <Button type="text" status="danger">删除</Button>
        </Popconfirm>
      </Space>
    )
  }
];
```

### 分页表格

```jsx
<Table
  rowKey="id"
  columns={columns}
  data={data}
  loading={loading}
  pagination={{
    total,
    pageSize: 20,
    showTotal: (total) => `共 ${total} 条`,
    showJumper: true,
    showPageSize: true,
    pageSizeOptions: [10, 20, 50, 100]
  }}
  onChange={(pagination, sorter, filter) => {
    fetchData({
      page: pagination.current,
      pageSize: pagination.pageSize,
      sorter,
      filter
    });
  }}
/>
```
