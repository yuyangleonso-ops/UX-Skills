# Arco Design 常见页面模式

## 列表页模式

### 标准列表页

**适用场景：** 数据查询、筛选、批量操作

**布局结构：**
```
┌─────────────────────────────────────────┐
│ [筛选区] - 表单元素横向排列，16px 间距     │
├─────────────────────────────────────────┤
│ [操作栏] - 主要按钮在左，次要按钮在右      │
├─────────────────────────────────────────┤
│                                         │
│ [表格区] - 24列栅格占满，rowKey 必填      │
│                                         │
├─────────────────────────────────────────┤
│ [分页] - 右对齐，24px 上边距             │
└─────────────────────────────────────────┘
```

**完整代码示例：**

```jsx
import React, { useState, useEffect } from 'react';
import {
  Form, Input, Button, Table, Space, Pagination, Card,
  Select, DatePicker, Message
} from '@arco-design/web-react';
import { IconSearch, IconRefresh, IconPlus } from '@arco-design/web-react/icon';

function UserListPage() {
  const [form] = Form.useForm();
  const [data, setData] = useState([]);
  const [loading, setLoading] = useState(false);
  const [pagination, setPagination] = useState({
    current: 1,
    pageSize: 20,
    total: 0
  });

  const columns = [
    {
      title: 'ID',
      dataIndex: 'id',
      width: 80
    },
    {
      title: '用户名',
      dataIndex: 'username',
      sorter: (a, b) => a.username.localeCompare(b.username)
    },
    {
      title: '邮箱',
      dataIndex: 'email'
    },
    {
      title: '状态',
      dataIndex: 'status',
      render: (status) => (
        <Badge
          status={status === 'active' ? 'success' : 'default'}
          text={status === 'active' ? '启用' : '禁用'}
        />
      ),
      filters: [
        { text: '启用', value: 'active' },
        { text: '禁用', value: 'inactive' }
      ]
    },
    {
      title: '创建时间',
      dataIndex: 'createdAt',
      sorter: (a, b) => new Date(a.createdAt) - new Date(b.createdAt)
    },
    {
      title: '操作',
      fixed: 'right',
      width: 180,
      render: (_, record) => (
        <Space size="small">
          <Button type="text" onClick={() => handleEdit(record)}>
            编辑
          </Button>
          <Button type="text" onClick={() => handleView(record)}>
            查看
          </Button>
          <Popconfirm
            title="确认删除？"
            content={`确定要删除用户 "${record.username}" 吗？`}
            onOk={() => handleDelete(record)}
          >
            <Button type="text" status="danger">
              删除
            </Button>
          </Popconfirm>
        </Space>
      )
    }
  ];

  const fetchData = async (params = {}) => {
    setLoading(true);
    try {
      const { data: res } = await api.getUsers({
        page: pagination.current,
        pageSize: pagination.pageSize,
        ...form.getFieldsValue(),
        ...params
      });
      setData(res.list);
      setPagination({ ...pagination, total: res.total });
    } catch (error) {
      Message.error('获取数据失败');
    } finally {
      setLoading(false);
    }
  };

  useEffect(() => {
    fetchData();
  }, [pagination.current, pagination.pageSize]);

  return (
    <Card style={{ padding: 24 }}>
      {/* 筛选区 */}
      <Form form={form} layout="inline">
        <Space size={16} wrap>
          <Form.Item label="用户名" field="username">
            <Input
              placeholder="请输入用户名"
              allowClear
              prefix={<IconSearch />}
            />
          </Form.Item>
          <Form.Item label="状态" field="status">
            <Select
              placeholder="全部"
              allowClear
              style={{ width: 120 }}
              options={[
                { label: '启用', value: 'active' },
                { label: '禁用', value: 'inactive' }
              ]}
            />
          </Form.Item>
          <Form.Item label="创建时间" field="dateRange">
            <DatePicker.RangePicker />
          </Form.Item>
          <Button
            type="primary"
            icon={<IconSearch />}
            onClick={() => fetchData({ page: 1 })}
          >
            查询
          </Button>
          <Button
            icon={<IconRefresh />}
            onClick={() => {
              form.resetFields();
              fetchData({ page: 1 });
            }}
          >
            重置
          </Button>
        </Space>
      </Form>

      {/* 操作栏 */}
      <div style={{ margin: '16px 0' }}>
        <Space>
          <Button
            type="primary"
            icon={<IconPlus />}
            onClick={() => handleAdd()}
          >
            新建用户
          </Button>
          <Button onClick={() => handleExport()}>
            导出
          </Button>
        </Space>
      </div>

      {/* 表格 */}
      <Table
        rowKey="id"
        columns={columns}
        data={data}
        loading={loading}
        pagination={{
          ...pagination,
          showTotal: (total) => `共 ${total} 条`,
          showJumper: true,
          showPageSize: true,
          pageSizeOptions: [10, 20, 50, 100]
        }}
        onChange={(pagination, sorter, filter) => {
          setPagination({
            current: pagination.current,
            pageSize: pagination.pageSize
          });
          fetchData({ sorter, filter });
        }}
      />
    </Card>
  );
}
```

---

## 表单页模式

### 基础表单页

**适用场景：** 数据录入、编辑

**布局结构：**
```
┌─────────────────────────────────────────┐
│ 页面标题 (20px, Semibold)                 │
│ 页面描述 (14px, Secondary)                │
├─────────────────────────────────────────┤
│                                         │
│ ┌───────────────────────────────────┐   │
│ │ 表单内容                           │   │
│ │ - 最大宽度 800px                   │   │
│ │ - 居中对齐                         │   │
│ │ - 字段间距 16px                    │   │
│ └───────────────────────────────────┘   │
│                                         │
│         [保存] [取消]                     │
└─────────────────────────────────────────┘
```

**完整代码示例：**

```jsx
import React from 'react';
import {
  Form, Input, Button, Card, Typography, Space,
  Select, Radio, Message, Spin
} from '@arco-design/web-react';

const { Title, Text } = Typography;

function UserFormPage({ userId }) {
  const [form] = Form.useForm();
  const [loading, setLoading] = useState(false);
  const [submitting, setSubmitting] = useState(false);

  // 编辑时加载数据
  useEffect(() => {
    if (userId) {
      setLoading(true);
      api.getUser(userId)
        .then(({ data }) => {
          form.setFieldsValue(data);
        })
        .finally(() => setLoading(false));
    }
  }, [userId]);

  const handleSubmit = async () => {
    try {
      const values = await form.validate();
      setSubmitting(true);

      if (userId) {
        await api.updateUser(userId, values);
        Message.success('更新成功');
      } else {
        await api.createUser(values);
        Message.success('创建成功');
      }

      // 返回列表页
      history.back();
    } catch (error) {
      if (error.errors) {
        // 表单验证错误，已在 UI 显示
        return;
      }
      Message.error(userId ? '更新失败' : '创建失败');
    } finally {
      setSubmitting(false);
    }
  };

  return (
    <div style={{ maxWidth: 800, margin: '0 auto', padding: 24 }}>
      <Card>
        <Spin loading={loading}>
          <Title heading={3} style={{ marginBottom: 8 }}>
            {userId ? '编辑用户' : '新建用户'}
          </Title>
          <Text type="secondary" style={{ marginBottom: 32, display: 'block' }}>
            {userId
              ? '修改用户信息，保存后立即生效'
              : '填写以下信息创建新用户'}
          </Text>

          <Form
            form={form}
            layout="vertical"
            initialValues={{
              status: 'active',
              gender: 'unknown'
            }}
          >
            <Form.Item
              label="用户名"
              field="username"
              rules={[
                { required: true, message: '请输入用户名' },
                { minLength: 3, message: '用户名至少3个字符' },
                { maxLength: 20, message: '用户名最多20个字符' },
                {
                  validator: (value, callback) => {
                    if (!/^[a-zA-Z0-9_]+$/.test(value)) {
                      callback('用户名只能包含字母、数字和下划线');
                    } else {
                      callback();
                    }
                  }
                }
              ]}
            >
              <Input
                placeholder="请输入用户名"
                disabled={!!userId}
                maxLength={20}
                showWordLimit
              />
            </Form.Item>

            <Form.Item
              label="邮箱"
              field="email"
              rules={[
                { required: true, message: '请输入邮箱' },
                { type: 'email', message: '邮箱格式不正确' }
              ]}
            >
              <Input placeholder="请输入邮箱" />
            </Form.Item>

            <Form.Item
              label="手机号"
              field="phone"
              rules={[
                {
                  validator: (value, callback) => {
                    if (value && !/^1[3-9]\d{9}$/.test(value)) {
                      callback('手机号格式不正确');
                    } else {
                      callback();
                    }
                  }
                }
              ]}
            >
              <Input placeholder="请输入手机号" />
            </Form.Item>

            <Form.Item
              label="性别"
              field="gender"
            >
              <Radio.Group>
                <Radio value="male">男</Radio>
                <Radio value="female">女</Radio>
                <Radio value="unknown">保密</Radio>
              </Radio.Group>
            </Form.Item>

            <Form.Item
              label="角色"
              field="role"
              rules={[{ required: true, message: '请选择角色' }]}
            >
              <Select placeholder="请选择角色">
                <Select.Option value="admin">管理员</Select.Option>
                <Select.Option value="editor">编辑</Select.Option>
                <Select.Option value="viewer">访客</Select.Option>
              </Select>
            </Form.Item>

            <Form.Item
              label="状态"
              field="status"
            >
              <Radio.Group type="button">
                <Radio value="active">启用</Radio>
                <Radio value="inactive">禁用</Radio>
              </Radio.Group>
            </Form.Item>

            <Form.Item
              label="备注"
              field="remark"
            >
              <Input.TextArea
                placeholder="请输入备注"
                maxLength={200}
                showWordLimit
                autoSize={{ minRows: 3, maxRows: 5 }}
              />
            </Form.Item>

            <Form.Item>
              <Space size={16} style={{ marginTop: 16 }}>
                <Button
                  type="primary"
                  loading={submitting}
                  onClick={handleSubmit}
                >
                  保存
                </Button>
                <Button onClick={() => history.back()}>
                  取消
                </Button>
              </Space>
            </Form.Item>
          </Form>
        </Spin>
      </Card>
    </div>
  );
}
```

### 分步表单

**适用场景：** 复杂流程，需要分步骤完成

```jsx
function StepForm() {
  const [current, setCurrent] = useState(1);
  const [formData, setFormData] = useState({});

  const steps = [
    {
      title: '基本信息',
      content: <BasicInfoForm />
    },
    {
      title: '配置信息',
      content: <ConfigForm />
    },
    {
      title: '确认信息',
      content: <ConfirmForm />
    }
  ];

  return (
    <div style={{ maxWidth: 800, margin: '0 auto', padding: 24 }}>
      <Steps current={current} style={{ marginBottom: 40 }}>
        {steps.map((step, index) => (
          <Steps.Step key={index} title={step.title} />
        ))}
      </Steps>

      <Card style={{ marginBottom: 24 }}>
        {steps[current - 1].content}
      </Card>

      <div style={{ textAlign: 'center' }}>
        <Space>
          {current > 1 && (
            <Button onClick={() => setCurrent(current - 1)}>
              上一步
            </Button>
          )}
          {current < steps.length ? (
            <Button type="primary" onClick={() => setCurrent(current + 1)}>
              下一步
            </Button>
          ) : (
            <Button type="primary" onClick={handleSubmit}>
              提交
            </Button>
          )}
        </Space>
      </div>
    </div>
  );
}
```

---

## 详情页模式

**适用场景：** 信息展示、只读查看

**布局结构：**
```
┌─────────────────────────────────────────┐
│ [页面标题]                     [编辑]     │
├─────────────────────────────────────────┤
│                                         │
│ ┌─────────────┐  ┌─────────────────┐   │
│ │ 基础信息     │  │ 详细信息         │   │
│ │ (Descript)  │  │ (Card分组)       │   │
│ └─────────────┘  └─────────────────┘   │
│                                         │
└─────────────────────────────────────────┘
```

**完整代码示例：**

```jsx
function UserDetailPage({ userId }) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    api.getUserDetail(userId)
      .then(({ data }) => setData(data))
      .finally(() => setLoading(false));
  }, [userId]);

  if (loading) return <Spin style={{ width: '100%', padding: 40 }} />;

  return (
    <div style={{ padding: 24 }}>
      {/* 页面标题 */}
      <div style={{ marginBottom: 24, display: 'flex', justifyContent: 'space-between' }}>
        <Title heading={3}>用户详情</Title>
        <Space>
          <Button onClick={() => history.back()}>返回</Button>
          <Button type="primary" onClick={() => handleEdit()}>编辑</Button>
        </Space>
      </div>

      <Row gutter={24}>
        {/* 左侧基础信息 */}
        <Col span={8}>
          <Card title="基础信息">
            <Descriptions
              colon=":"
              layout="horizontal"
              labelStyle={{ width: 100, textAlign: 'right' }}
            >
              <Descriptions.Item label="用户名">
                {data.username}
              </Descriptions.Item>
              <Descriptions.Item label="头像">
                <Avatar size={64} src={data.avatar}>
                  {data.username[0]}
                </Avatar>
              </Descriptions.Item>
              <Descriptions.Item label="状态">
                <Badge
                  status={data.status === 'active' ? 'success' : 'default'}
                  text={data.status === 'active' ? '启用' : '禁用'}
                />
              </Descriptions.Item>
              <Descriptions.Item label="角色">
                {data.role === 'admin' ? '管理员' : '普通用户'}
              </Descriptions.Item>
              <Descriptions.Item label="创建时间">
                {data.createdAt}
              </Descriptions.Item>
            </Descriptions>
          </Card>
        </Col>

        {/* 右侧详细信息 */}
        <Col span={16}>
          <Space direction="vertical" size={16} style={{ width: '100%' }}>
            <Card title="联系信息">
              <Descriptions colon=":" layout="horizontal">
                <Descriptions.Item label="邮箱">{data.email}</Descriptions.Item>
                <Descriptions.Item label="手机号">{data.phone}</Descriptions.Item>
                <Descriptions.Item label="地址">{data.address}</Descriptions.Item>
              </Descriptions>
            </Card>

            <Card title="操作记录">
              <Timeline>
                {data.logs.map((log, index) => (
                  <Timeline.Item key={index} label={log.time}>
                    {log.action}
                  </Timeline.Item>
                ))}
              </Timeline>
            </Card>
          </Space>
        </Col>
      </Row>
    </div>
  );
}
```

---

## Dashboard 模式

**适用场景：** 数据概览、关键指标展示

**布局结构：**
```
┌───────┬───────┬───────┬───────┐
│ 指标1  │ 指标2  │ 指标3  │ 指标4  │  ← Statistic Cards
├───────┴───────┴───────┴───────┤
│                               │
│          趋势图表               │  ← Line/Bar Chart
│                               │
├──────────────────┬────────────┤
│    分类占比       │   最近动态  │  ← Pie Chart + List
│   (Pie Chart)    │   (List)   │
└──────────────────┴────────────┘
```

**完整代码示例：**

```jsx
function DashboardPage() {
  return (
    <div style={{ padding: 24 }}>
      {/* 指标卡片 */}
      <Row gutter={16}>
        <Col span={6}>
          <Card>
            <Statistic
              title="总用户数"
              value={123456}
              precision={0}
              suffix="人"
              prefix={<IconUser />}
            />
            <div style={{ marginTop: 8 }}>
              <Text type="secondary">较上月 </Text>
              <Text type="success">+12.5%</Text>
            </div>
          </Card>
        </Col>
        <Col span={6}>
          <Card>
            <Statistic
              title="今日订单"
              value={1688}
              precision={0}
              prefix={<IconShopping />}
            />
            <div style={{ marginTop: 8 }}>
              <Text type="secondary">较昨日 </Text>
              <Text type="danger">-5.2%</Text>
            </div>
          </Card>
        </Col>
        <Col span={6}>
          <Card>
            <Statistic
              title="总收入"
              value={89234.56}
              precision={2}
              prefix="¥"
            />
            <div style={{ marginTop: 8 }}>
              <Text type="secondary">较上月 </Text>
              <Text type="success">+8.3%</Text>
            </div>
          </Card>
        </Col>
        <Col span={6}>
          <Card>
            <Statistic
              title="转化率"
              value={3.68}
              precision={2}
              suffix="%"
            />
            <div style={{ marginTop: 8 }}>
              <Text type="secondary">较上月 </Text>
              <Text type="success">+0.5%</Text>
            </div>
          </Card>
        </Col>
      </Row>

      {/* 趋势图表 */}
      <Card title="销售趋势" style={{ marginTop: 16 }}>
        <LineChart data={trendData} />
      </Card>

      {/* 底部区域 */}
      <Row gutter={16} style={{ marginTop: 16 }}>
        <Col span={12}>
          <Card title="用户来源">
            <PieChart data={sourceData} />
          </Card>
        </Col>
        <Col span={12}>
          <Card title="最近动态">
            <List
              dataSource={activities}
              render={(item) => (
                <List.Item>
                  <List.Item.Meta
                    avatar={<Avatar>{item.user[0]}</Avatar>}
                    title={item.action}
                    description={item.time}
                  />
                </List.Item>
              )}
            />
          </Card>
        </Col>
      </Row>
    </div>
  );
}
```

---

## 登录页模式

```jsx
function LoginPage() {
  const [form] = Form.useForm();
  const [loading, setLoading] = useState(false);

  const handleLogin = async () => {
    try {
      const values = await form.validate();
      setLoading(true);
      await login(values);
      Message.success('登录成功');
      router.push('/');
    } catch (error) {
      Message.error('登录失败，请检查账号密码');
    } finally {
      setLoading(false);
    }
  };

  return (
    <div
      style={{
        height: '100vh',
        display: 'flex',
        alignItems: 'center',
        justifyContent: 'center',
        background: '#F7F8FA'
      }}
    >
      <Card
        style={{ width: 400, padding: '40px 32px' }}
        bordered={false}
      >
        <div style={{ textAlign: 'center', marginBottom: 40 }}>
          <img src="/logo.png" alt="Logo" style={{ height: 48 }} />
          <Title heading={4} style={{ marginTop: 16 }}>
            欢迎登录
          </Title>
        </div>

        <Form form={form} size="large">
          <Form.Item
            field="username"
            rules={[{ required: true, message: '请输入用户名' }]}
          >
            <Input
              prefix={<IconUser />}
              placeholder="用户名"
            />
          </Form.Item>

          <Form.Item
            field="password"
            rules={[{ required: true, message: '请输入密码' }]}
          >
            <Input.Password
              prefix={<IconLock />}
              placeholder="密码"
            />
          </Form.Item>

          <Form.Item>
            <Checkbox>记住我</Checkbox>
            <a style={{ float: 'right' }}>忘记密码？</a>
          </Form.Item>

          <Button
            type="primary"
            long
            loading={loading}
            onClick={handleLogin}
          >
            登录
          </Button>
        </Form>
      </Card>
    </div>
  );
}
```

---

## 结果页模式

```jsx
function ResultPage() {
  return (
    <div style={{ padding: 80, textAlign: 'center' }}>
      <Result
        status="success"
        title="操作成功"
        subTitle="您的订单已提交，订单号：20240101123456"
        extra={[
          <Button key="back">返回列表</Button>,
          <Button key="detail" type="primary">查看详情</Button>
        ]}
      />
    </div>
  );
}
```

状态选项：`success` | `error` | `info` | `warning` | `404` | `403` | `500`
