# 使用案例

## 本案例使用版本 react18  antd5

注意点：本案例使用版本4.x,，不同ui版本，使用略有差异，以官网示例为准。

[版本5-Antd](https://ant-design.antgroup.com/index-cn)

各个版本发布时间：

```
 AntD3.0  2018.1.6
 AntD4.0  2020.2.28
 AntD5.0  2022.11
```

## 全局方法

```
import {theme } from 'antd';
const { useToken } = theme;
const { token } = useToken();

  const contentStyle = { //包含当前使用主体的基础颜色（每个颜色细分1-10种），高度，字体，
    backgroundColor: token.colorBgElevated,
    borderRadius: token.borderRadiusLG,
    boxShadow: token.boxShadowSecondary,
  };
```











## 第一部分：通用模块

### Button按钮

在 Ant Design 中我们提供了五种按钮。

- 主按钮：用于主行动点，一个操作区域只能有一个主按钮。
- 默认按钮：用于没有主次之分的一组行动点。
- 虚线按钮：常用于添加操作。
- 文本按钮：用于最次级的行动点。
- 链接按钮：一般用于链接，即导航至某位置。

以及四种状态属性与上面配合使用。

- 危险：删除/移动/修改权限等危险操作，一般需要二次确认。
- 幽灵：用于背景色比较复杂的地方，常用在首页/产品页等展示场景。
- 禁用：行动点不可用的时候，一般需要文案解释。
- 加载中：用于异步操作等待反馈的时候，也可以避免多次提交。

### 代码演示

基本用法

```react
import { Button } from 'antd';   <---重点 引入
import React from 'react';
const App = () => (
  <>
    <Button type="primary">Primary Button</Button>    <---重点 使用
    
    <Button>Default Button</Button>
    
    <Button type="dashed">Dashed Button</Button>

    <Button type="text">Text Button</Button>
    <Button type="link">Link Button</Button>
  </>
);
export default App;
```

其他大小，形状，状态，颜色，幽灵，类型，点击 见官网。

### Icon图标

额外引入图标组件包

```
npm install @ant-design/icons --save   注意版本差异引入  否则报错
```



### 使用

```react
import React from 'react';
import {
  LoadingOutlined,
  SmileOutlined,
  SyncOutlined,
} from '@ant-design/icons';
import { Space } from 'antd';
const App = () => (
  <Space>

    <SyncOutlined spin />
    <SmileOutlined rotate={180} />
    <LoadingOutlined />
  </Space>
);
export default App;
```





### Typography排版

一句话概括：

对标题，段落，加粗，链接的一层封装，添加删除线样式，添加代码样式，是否加粗，加属性快捷使用

当需要展示标题、段落、列表内容时使用，如文章/博客/日志的文本样式。

标题

```react
import { Typography } from 'antd';
const { Title } = Typography;
const App = () => (
  <>
    <Title>h1. Ant Design</Title>
    <Title level={2}>h2. Ant Design</Title>
    <Title level={3}>h3. Ant Design</Title>
    <Title level={4}>h4. Ant Design</Title>
    <Title level={5}>h5. Ant Design</Title>
  </>
);
export default App;
```

文本与超链接

```react
import { Space, Typography } from 'antd';
import React from 'react';
const { Text, Link } = Typography;
const App = () => (
  <Space direction="vertical">
    <Text>Ant Design (default)</Text>
    <Text type="secondary">Ant Design (secondary)</Text>
    <Text type="success">Ant Design (success)</Text>
    <Text type="warning">Ant Design (warning)</Text>
    <Text type="danger">Ant Design (danger)</Text>
    <Text disabled>Ant Design (disabled)</Text>
    <Text mark>Ant Design (mark)</Text>
    <Text code>Ant Design (code)</Text>
    <Text keyboard>Ant Design (keyboard)</Text>
    <Text underline>Ant Design (underline)</Text>
    <Text delete>Ant Design (delete)</Text>
    <Text strong>Ant Design (strong)</Text>
    <Text italic>Ant Design (italic)</Text>
    <Link href="https://ant.design" target="_blank">
      Ant Design (Link)
    </Link>
  </Space>
);
export default App;
```

This is a copyable text.

可编辑状态

```react
import {Typography } from 'antd';

<Typography.Title
        editable   // <--- 编辑属性
        level={5}  // H1- H5（大- > 小） 超出默认最大1
        style={{ //内联样式
          margin: 0,
        }}
      >
        h1. Ant Design
 </Typography.Title>
```

## 第二部分：布局模块

### Divider分割线

对不同章节的文本段落进行分割。 或者中间加上文字 ，文字的左右布局等

```react
import { Divider  } from 'antd';

const App = () => {
  return (
    <>
        <Divider plain dashed>Text</Divider>
    </>
  );
};
export default App;
```

### Flex弹性布局

- 适合设置元素之间的间距。
- 适合设置各种水平、垂直对齐方式。

  ```react
  import React from 'react';
  import { Flex,  } from 'antd';
  ```

const baseStyle = {
  width: '25%',
  height: 54,
};
const App = () => {
  return (

      <Flex horizontal gap="small"> //horizontal 横向 vertical竖向 gap间隙
        <p style={baseStyle}>888</p>
        <p style={baseStyle}>888</p>
        <p style={baseStyle}>888</p>
      </Flex>

  );
};
export default App;
  ```

以Flex标签+传值属性 组合效果

# Grid栅格

​```react
import React from 'react';
import { Col, Row } from 'antd';
const App = () => (
  <>
    <Row>
      <Col span={6}>col-6</Col>
      <Col span={6}>col-6</Col>
      <Col span={6}>col-6</Col>
      <Col span={6}>col-6</Col>
    </Row>
  </>
);
export default App;
  ```

### Layout布局

后台管理页面，布局快捷搭建。

```react
import React, { useState } from 'react';
import {
  MenuFoldOutlined,
  MenuUnfoldOutlined,
  UploadOutlined,
  UserOutlined,
  VideoCameraOutlined,
} from '@ant-design/icons';
import { Layout, Menu, Button, theme } from 'antd';
const { Header, Sider, Content } = Layout;
const App = () => {
  const [collapsed, setCollapsed] = useState(false);
  const {
    token: { colorBgContainer },
  } = theme.useToken();
  return (
    <Layout>
      <Sider trigger={null} collapsible collapsed={collapsed}>
        <div className="demo-logo-vertical" />
        <Menu
          theme="dark"
          mode="inline"
          defaultSelectedKeys={['1']}
          items={[
            {
              key: '1',
              icon: <UserOutlined />,
              label: 'nav 1',
            },
            {
              key: '2',
              icon: <VideoCameraOutlined />,
              label: 'nav 2',
            },
            {
              key: '3',
              icon: <UploadOutlined />,
              label: 'nav 3',
            },
          ]}
        />
      </Sider>
      <Layout>
        <Header
          style={{
            padding: 0,
            background: colorBgContainer,
          }}
        >
          <Button
            type="text"
            icon={collapsed ? <MenuUnfoldOutlined /> : <MenuFoldOutlined />}
            onClick={() => setCollapsed(!collapsed)}
            style={{
              fontSize: '16px',
              width: 64,
              height: 64,
            }}
          />
        </Header>
        <Content
          style={{
            margin: '24px 16px',
            padding: 24,
            minHeight: 280,
            background: colorBgContainer,
          }}
        >
          Content
        </Content>
      </Layout>
    </Layout>
  );
};
export default App;
```

### Space间距

设置组件之间的间距。

```react
import React from 'react';
import { Button, Space } from 'antd';
const App = () => (
  <Space size={[8, 16]} wrap>   <----- 可以 Size | Size[]
    {new Array(20).fill(null).map((_, index) => (
      <Button key={index}>Button</Button>
    ))}
  </Space>
);
export default App;
                                    
  size [8,16]  表示 【左右 ，上下】间距
  size =‘20’   表示 上下左右间距  实现方式是使用了flex gap: 20px; 网格化布局属性                                
```

## 第三部分 导航



### Anchor锚点

用于跳转到页面指定位置。  当网页高度大于100vh时，点击锚点，页面快速滑动至锚点处。

案例

```react
import React from 'react';
import { Anchor, Row, Col } from 'antd';  <--重点 Anchor组件

const handleClick = (e, link) => {
  e.preventDefault();
  console.log(link);
};

const App = () => (
  <Row>
    <Col span={16}>
      <div
        id="part-1"   <--重点  id
        style={{
          height: '100vh',
          background: 'rgba(255,0,0,0.02)',
        }}
      />
      <div
        id="part-2"
        style={{
          height: '100vh',
          background: 'rgba(0,255,0,0.02)',
        }}
      />
      <div
        id="part-3"
        style={{
          height: '100vh',
          background: 'rgba(0,0,255,0.02)',
        }}
      />
    </Col>
    <Col span={8}>
      <Anchor
        onClick={handleClick}
        items={[    <--重点  入值
          {
            key: 'part-1',
            href: '#part-1',
            title: 'Part 1',
          },
          {
            key: 'part-2',
            href: '#part-2',
            title: 'Part 2',
          },
          {
            key: 'part-3',
            href: '#part-3',
            title: 'Part 3',
          },
        ]}
      />
    </Col>
  </Row>
);
export default App;
```

如果使用哈希模式的路由时，点击页面，当URL被修改后，刷新页面会导致当前路由没有定义而出现404的情况，或跳转页面。

处理方法：使用 **onClick** 阻止默认事件 。



其他详情官网

### Breadcrumb面包屑

显示当前页面在系统层级结构中的位置，并能向上返回。

* 当系统拥有超过两级以上的层级结构时

* 当需要告知用户[你在哪里]时;

* 当需要向上导航的功能时。

### Breadcrumb面包屑

案例：

展示： home --> 模块1  --> 模块1- page

使用：直接传入数组 包含title属性

```
import React from 'react';
import { Breadcrumb } from 'antd';
const App = () => (
  <Breadcrumb
    items={[
      {
        title: 'Home',
      },
      {
        title: <a href="">模块1</a>,
      },
      {
        title: '模块1- page',
      },
    ]}
  />
);
export default App;
```

### Dropdown下拉菜单

####  何时使用

当页面上的操作命令过多时，用此组件可以收纳操作元素。点击或移入触点，会出现一个下拉菜单。可在列表中进行选择，并执行相应的命令。

使用：

**Dropdown** 组件 menu属性传入参数 一个数组对象

key 唯一标识    label  可以是一个标签 或是一个字符串   icon 使用一个图标  disabled是否禁用

**官网提供**： 

下拉出现效果，如像tips方式，出现位置，触发方式，常用的点击，hover,还有鼠标右键点击。

多级菜单（children属性实现）

dropdownRender属性，对下拉自由扩展，比如加一个底部按钮

```react
import React from 'react';
import { DownOutlined, SmileOutlined } from '@ant-design/icons';
import { Dropdown, Space } from 'antd';

const items = [
  {
    key: '2',
    label: (
      <a target="_blank" rel="noopener noreferrer" href="https://www.aliyun.com">
        2nd menu item (disabled)
      </a>
    ),
    icon: <SmileOutlined />,
    disabled: true,
  },
  {
    key: '4',
    danger: true,
    label: 'a danger item',
  },
];
const App = () => (

  <Dropdown
    menu={{
      items <----重点  传入参数
    }}
  >
    <a onClick={(e) => e.preventDefault()}>
      <Space>
        Hover me
        <DownOutlined />
      </Space>
    </a>
  </Dropdown>
);
export default App;

```



### *Menu导航菜单

为页面和功能提供导航的菜单列表。

导航菜单是一个**网站的灵魂**，用户依赖导航在各个页面中进行跳转。一般分为顶部导航和侧边导航，顶部导航提供全局性的类目和功能，侧边导航提供多级结构来收纳和排列网站架构。

#### 开发者注意事项

- Menu 元素为 `ul`，因而仅支持 [`li` 以及 `script-supporting` 子元素](https://html.spec.whatwg.org/multipage/grouping-content.html#the-ul-element)。因而你的子节点元素应该都在 `Menu.Item` 内使用。
- Menu 需要计算节点结构，因而其子元素仅支持 `Menu.*` 以及对此进行封装的 HOC 组件。

 第一种使用方式：样式都是官方提供的默认样式和交互方式

```react
import { Menu } from 'antd';   1.导出核心方法

function getItem(label, key, icon, children, type) {
  return {
    label,    //显示的标题名字
    key,    //标记唯一  也是路由
    icon,    //图标
    children,  //孩子项
    type,  //  type: 'group', 定义类型为 group 时，会作为分组处理:
    title, //   设置收缩时展示的悬浮标题
  };
}

const items = [  3.只要使用规定数据字段，就能渲染出来数据
  getItem('收件箱', 'sub1', <MailOutlined />, [
    getItem('工作用信箱', '5'),
    getItem('生活用信箱', '6'),
  ]),

  getItem('飞虎战队', 'feiHu', <AndroidOutlined />, [
    getItem('飞虎1号', '13'),
     getItem('飞虎2号', '14')
    ]),
];


  <Menu
      onClick={onClick}
      style={{
        width: 256,
      }}
      defaultSelectedKeys={['1']}
      defaultOpenKeys={['sub1']}
      mode="inline"
      items={items}  2. 使用符合条件的数据结构，传入数据。
    />
```

第二种自定义方式

**Menu.Item**  支持自定义单项的样式自定义 结构自定义，根据这个结构，可以动态创建自己的路由菜单。

```react
<Menu
    onClick={onClick}
    style={{
      width: 256,
    }}
    defaultSelectedKeys={['1']}
    defaultOpenKeys={['sub1']}
    mode="inline"
    >
     <Menu.Item key={1}>
        <Link to={'/home/about'}>
          {<Icon type={'info-circle-o'}/>}
          <span>自定义child</span>
        </Link>
      </Menu.Item>

    </Menu>
```



















