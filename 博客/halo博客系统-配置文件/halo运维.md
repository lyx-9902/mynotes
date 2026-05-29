# 常见功能操作记录

## 一 、升级操作

2.21.10   升级到 2.22.13 



```
1.系统备份

2.停止系统
docker compose down
```

根据官网升级操作

地址： https://docs.halo.run/getting-started/install/docker-compose/#%E5%8D%87%E7%BA%A7-halo

修改 docker-compose.yaml 中配置的镜像版本。

```
services:
 halo:
   image: registry.fit2cloud.com/halo/halo-pro:2.22
```

  启动项目： docker compose up -d



### 项目部署

```
创建项目： 
  halo+postareSQL创建
  服务器： ubuntu系统  docker compose启动

```

###  自定义模版使

当前使用主题 Earth 版本 2.22.13









## 关于yaml的书写规范

YAML 是 "YAML Ain't a Markup Language"（YAML 不是一种标记语言）的递归缩写。在开发的这种语言时，YAML 的意思其实是："Yet Another Markup Language"（仍是一种标记语言）。

YAML 的语法和其他高级语言类似，并且可以简单表达清单、散列表，标量等数据形态。它使用空白符号缩进和大量依赖外观的特色，特别适合用来表达或编辑数据结构、各种配置文件、倾印调试内容、文件大纲（例如：许多电子邮件标题格式和YAML非常接近）。

YAML 的配置文件后缀为 **.yml**，如：**runoob.yml** 。

### 基本语法

- 大小写敏感
- 使用缩进表示层级关系
- 缩进不允许使用 tab，只允许空格
- 缩进的空格数不重要，只要相同层级的元素左对齐即可
- **#** 表示注释
- **:** 号后面要加空格

### 数据类型

YAML 支持以下几种数据类型：

- 对象：键值对的集合，又称为映射（mapping）/ 哈希（hashes） / 字典（dictionary）
- 数组：一组按次序排列的值，又称为序列（sequence） / 列表（list）
- 纯量（scalars）：单个的、不可再分的值

### YAML 对象

对象键值对使用冒号结构表示 **key: value**，冒号后面要加一个空格。

也可以使用 **key:{key1: value1, key2: value2, ...}**。

还可以使用缩进表示层级关系；

```
key: 
    child-key: value
    child-key2: value2
```

较为复杂的对象格式，可以使用问号加一个空格代表一个复杂的 key，配合一个冒号加一个空格代表一个 value：

```
?  
    - complexkey1
    - complexkey2
:
    - complexvalue1
    - complexvalue2
```

意思即对象的属性是一个数组 [complexkey1,complexkey2]，对应的值也是一个数组 [complexvalue1,complexvalue2]

### YAML 数组

以 **-** 开头的行表示构成一个数组：

```
- A
- B
- C
```

YAML 支持多维数组，可以使用行内表示：

```
key: [value1, value2, ...]
```

数据结构的子成员是一个数组，则可以在该项下面缩进一个空格。

```
-
 - A
 - B
 - C
```

一个相对复杂的例子：

```
companies:
    -
        id: 1
        name: company1
        price: 200W
    -
        id: 2
        name: company2
        price: 500W
```

意思是 companies 属性是一个数组，每一个数组元素又是由 id、name、price 三个属性构成。

数组也可以使用流式(flow)的方式表示：

```
companies: [{id: 1,name: company1,price: 200W},{id: 2,name: company2,price: 500W}]
```

### 复合结构

数组和对象可以构成复合结构，例：

```
languages:
  - Ruby
  - Perl
  - Python 
websites:
  YAML: yaml.org 
  Ruby: ruby-lang.org 
  Python: python.org 
  Perl: use.perl.org
```

转换为 json 为：

```
{ 
  languages: [ 'Ruby', 'Perl', 'Python'],
  websites: {
    YAML: 'yaml.org',
    Ruby: 'ruby-lang.org',
    Python: 'python.org',
    Perl: 'use.perl.org' 
  } 
}
```

### 纯量

纯量是最基本的，不可再分的值，包括：

- 字符串
- 布尔值
- 整数
- 浮点数
- Null
- 时间
- 日期

使用一个例子来快速了解纯量的基本使用：

```
boolean: 
    - TRUE  #true,True都可以
    - FALSE  #false，False都可以
float:
    - 3.14
    - 6.8523015e+5  #可以使用科学计数法
int:
    - 123
    - 0b1010_0111_0100_1010_1110    #二进制表示
null:
    nodeName: 'node'
    parent: ~  #使用~表示null
string:
    - 哈哈
    - 'Hello world'  #可以使用双引号或者单引号包裹特殊字符
    - newline
      newline2    #字符串可以拆成多行，每一行会被转化成一个空格
date:
    - 2018-02-17    #日期必须使用ISO 8601格式，即yyyy-MM-dd
datetime: 
    -  2018-02-17T15:02:31+08:00    #时间使用ISO 8601格式，时间和日期之间使用T连接，最后使用+代表时区
```

### 引用

**&** 锚点和 ***** 别名，可以用来引用:

```
defaults: &defaults
  adapter:  postgres
  host:     localhost

development:
  database: myapp_development
  <<: *defaults

test:
  database: myapp_test
  <<: *defaults
```

相当于:

```
defaults:
  adapter:  postgres
  host:     localhost

development:
  database: myapp_development
  adapter:  postgres
  host:     localhost

test:
  database: myapp_test
  adapter:  postgres
  host:     localhost
```

**&** 用来建立锚点（defaults），**<<** 表示合并到当前数据，***** 用来引用锚点。

下面是另一个例子:

```
- &showell Steve 
- Clark 
- Brian 
- Oren 
- *showell 
```

转为 JavaScript 代码如下:

```
[ 'Steve', 'Clark', 'Brian', 'Oren', 'Steve' ]
```









# 修改测试：

修改默认page.html ，     网站关于页面，有变化。 再次修改page模版，需要重启docker compose。 再次测试：发现如果后续修改page模版，只需要单独docker restart halo，刷新页面即可变化。



1.已经成功创建了模版。

2.已经确定了：模版使用的技术栈  模版引擎。

**2026.02.09** 

接下来：1. 确定开发调试方法，本地开发，线上直接看效果的快速调试。 2.学习tanwindcss + 模版引擎的使用方法 + halo的组件套用方法 =  自由创建个性化的页面。



## halo项目页面调试

halo项目在 阿里云 ubuntu机器上，我本机是win11,有vscode编辑器。如何调试页面

## 核心思路

本地部署一套halo 进行开发页面模版，然后再替换到先上去。

本地halo 博客的 账号密码

```
admin
admin123
```

#### 3. 启动 Halo 容器

镜像拉取成功后，执行启动命令：

要在本地 Win11 + Docker Compose 部署的 Halo 中开启**主题开发模式**，实现修改模板后浏览器实时预览，你需要完成以下两步核心配置：

------

### 1. 关闭模板缓存（核心）

Halo 默认开启了 Thymeleaf 模板缓存，修改模板后不会立即生效。在 Docker 环境下，需要通过环境变量关闭缓存：

编辑你的 `docker-compose.yml` 文件，在 `halo` 服务的 `environment` 部分添加：

```
services:
  halo:
    # ... 其他配置
    environment:
      - SPRING_THYMELEAF_CACHE=false  # 关闭模板缓存
      - HALO_CACHE-TEMPLATE=false     # 关闭 Halo 自身的模板缓存
```

### 3. 重启容器并测试

1. 保存 

   ```
   docker-compose.yml
   ```

    文件，然后重启 Halo 容器：  （重点是销毁，启动。 而不是重启）

   ```
   docker compose down
   docker compose up -d
   ```

2. 现在，你可以直接在本地 `./themes/theme-earth` 目录下修改模板文件（如 `templates/index.html`）。

3. 刷新浏览器页面，修改后的效果会立即生效。

### 总结

1. `restart`是 “原地重启”，只重启容器进程，不读取新的 compose 配置，适合仅修改应用内部配置的场景；
2. `down + up -d`是 “重建重启”，会删除旧容器并基于最新 compose 文件创建新容器，适合修改了 compose 配置的场景；
3. 你的 Halo 开启开发模式需求中，修改了环境变量和挂载目录，必须用`down + up -d`才能让配置生效



## **Thymeleaf** 作为模板引擎

### 1. 基础表达式与变量访问

- 变量取值：${variable}

  html 预览

  ```
  <h1 th:text="${singlePage.spec.title}"></h1>
  ```

- 对象属性

  ：支持点语法或方括号

  ```
<img th:src="${singlePage.owner.avatar}" />
  <img th:src="${singlePage['owner']['avatar']}" />
```
  
- 空值安全：使用 ?避免空指针

  ```
  <img th:src="${singlePage.owner?.avatar}" />
  ```

- 字符串工具：#strings 工具类

  ```
  <a th:if="${#strings.isEmpty(singlePage.owner.avatar)}">...</a>
  ```

------

### 2. 条件判断与循环

- 条件渲染：th:if / th:unless

  ```
  <div th:if="${theme.config.post.content_style == 'github'}">...</div>
  <div th:unless="${#strings.isEmpty(singlePage.owner.avatar)}">...</div>
  ```

- 循环遍历：th:each

  ```
  <div th:each="post : ${posts}" th:text="${post.spec.title}"></div>
  ```

------

### 3. 模板布局与片段复用

- 片段定义

  ：

  ```
  th:fragment
  ```

  html

  预览

  ```
  <th:block th:fragment="head">...</th:block>
  <th:block th:fragment="content">...</th:block>
  ```

- 片段替换

  ：

  ```
  th:replace
  ```

  （替换整个标签）

  html

  预览

  ```
  <html th:replace="~{modules/layout :: html(...)}">
  ```

- 片段包含

  ：

  ```
  th:insert
  ```

   / 

  ```
  th:include
  ```

  （保留父标签）

  html

  预览

  ```
  <div th:insert="~{modules/footer :: footer}"></div>
  ```

  

- 布局参数传递

  ：通过 

  ```
  ::
  ```

   传递变量

  html

  预览

  ```
  <html th:replace="~{modules/layout :: html(
      title = ${singlePage.spec.title} + ' - ' + ${site.title},
      hero = ~{::hero},
      content = ~{::content},
      head = ~{::head}
  )}">
  ```

------

### 4. 资源与链接处理

- 静态资源

  ：

  ```
  @{...}
  ```

   自动处理上下文路径

  html

  预览

  ```
  <link th:href="@{/assets/styles/github-markdown.css}" rel="stylesheet" />
  ```

- 版本参数

  ：用于缓存控制

  html

  预览

  ```
  <link th:href="@{/assets/styles/github-markdown.css?v={version}(version=${theme.spec.version})}" />
  ```

  

- 路由链接

  ：生成 Halo 内部路由

  html

  预览

  ```
  <a th:href="@{${singlePage.owner.permalink}}">...</a>
  ```

------

### 5. Halo 特有扩展

- 主题配置

  ：

  ```
  ${theme.config.*}
  ```

  html

  预览

  ```
  <div th:if="${theme.config.post.content_style == 'github'}">...</div>
  ```

  

- 全局对象

  ：

  ```
  ${site}
  ```

  、

  ```
  ${user}
  ```

  、

  ```
  ${menu}
  ```

   等

  html

  预览

  ```
  <title th:text="${site.title}"></title>
  ```

- 模板缓存

  ：开发时需通过环境变量关闭

  yaml

  ```
  # docker-compose.yml
  environment:
    - SPRING_THYMELEAF_CACHE=false
  ```

------

### 6. 开发调试技巧

- **关闭缓存**：修改模板后立即生效，无需重启容器
- **片段预览**：直接访问片段 URL 进行调试
- **日志查看**：通过 `docker compose logs -f` 查看模板渲染错误



