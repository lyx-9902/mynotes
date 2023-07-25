## 知识点：

我的微信小程序app id

wxcf13082f9ae49f57

```
<script>

	export default {
		components: { 组件

		},
		data() {
			return {
				gutter: 0,
			}
		}
	}
</script>
```





### Hbuider 快捷键

  cntrl + D   删除当前行  

  双击标签 尾部，选中起止标签。

注意事项：

微信标签

vue 的钩子函数

组件中的data，以返回值的形式。

关于打包：  点击发行  云打包  选择安卓  ，打包完成后，出现下载链接，下载压缩包。

Hbuider 对于微信小程序 appid默认是一个测试id。 发布是，注意替换。

### 默认代开页面

```
"condition" : { //模式配置，仅开发期间生效
		"current": 0, //当前激活的模式(list 的索引项)
		"list": [
			{
				"name": "test", //模式名称
				"path": "pages/info/info", //启动页面，必选
				"query": "newsid=5173214" //启动参数，在页面的onLoad函数里面得到
			}
		]
	},
```



#### 1.快应用：

快应用是九大手机厂商基于硬件平台共同推出的新型应用生态。用户无需下载安装，即点即用，享受原生应用的性能体验。

![image-20210420141432896](C:\Users\luyunxiao\AppData\Roaming\Typora\typora-user-images\image-20210420141432896.png)

# uni-app 开发微信小程序

`uni-app`是一个使用`Vue.js` 开发所有前端应用的框架，开发者编写一套代码，可发布到`iOS`、`Android`、`H5`、以及各种小程序（微信/支付宝/百度/头条/QQ/钉钉）等多个平台。

即使不跨端，`uni-app`同时也是更好的小程序开发框架

![image-20210420143058763](C:\Users\luyunxiao\AppData\Roaming\Typora\typora-user-images\image-20210420143058763.png)

我使用`uni-app`框架主要用来开发微信小程序，我使用过程中感觉的好处是：

- `uni-app`框架使用的开发工具 `HBuilderX`，`HBuilderX` 内置相关环境，开箱即用，无需配置`nodejs`， 需要什么插件可直接下载，测试、打包、发布特别方便。
- `uni-app`采用`Vue.js`语法，基本支持`vue`大部分语法（`vue`的动态组件`component`不支持）。
- `PC`端使用`vue`封装的一些`js`方法，以及建构思想，可直接移植到`uni-app`中，比如：本人`pc`项目中`api`接口`js`文件，可直接复制到小程序框架`api`文件夹中（PS：`api`文件夹维护后端请求路径）
- `uni-app` 周边生态丰富，[插件市场](https://ext.dcloud.net.cn/)可用的组件特别多，也可使用vue语法自己封装一些组件。

## 开发工具（HBuilderX）

- `HBuilderX`: [官网IDE下载地址](https://www.dcloud.io/hbuilderx.html);
- `HBuilderX`是通用的前端开发工具，但为`uni-app`做了特别强化。
- `HBuilderX`提供了一些插件，可直接下载安装，具体如下图： `工具` > `插件安装`

![image-20210420143146038](C:\Users\luyunxiao\AppData\Roaming\Typora\typora-user-images\image-20210420143146038.png)

一、uniapp介绍
1.uniapp做混合开发的好处：
2. 开发环境&IDE工具：
二、使用步骤
第一步：打开HBuilderX选择文件->新建项目->选择uniapp项目
第二步：配置manifest.json文件，配置微信小程序AppID
第三步：小程序开发工具配置服务代理，端口
第四步：点击运行->运行到小程序模拟器
第五步：点击发布->选择小程序发布
第六步：小程序开发工具中填写对应的信息->上传->公众平台上提交审核



2021.04.21

##### 项目创建  ：

新建- 项目- uni-app - 默认模板 。 下载微信小程序调试工具

在项目的manifest.json配置文件中， 配置上小程序申请的appid， 和调试工具的安装位置，以供Hbuider的启动调用。

##### 关于调试：  

二维码调试和真机的二维码，保证pc和手机在同一网络下，扫描二维码，手机端可以查看。  自动真机调试，需要usb连接pc机。

##### 页面自动打开调试页面

```
page.json 文件中  参数配置如下

"condition": { //模式配置，仅开发期间生效
		"current": 0, //当前激活的模式(list 的索引项)
		"list": [{
			"name": "test", //模式名称
			"path": "pages/info/info", //启动页面，必选
			"query": "newsid=5158607" //启动参数，在页面的onLoad函数里面得到
		}]
	}
```

#### 1 uni中的像素尺寸

```
padding:10upx 2%;                    upx  相对单位
.art-content{line-height:2em;}       em  原生像素单位
                                       rpx  微信接受的单位（Hbuider 会自动转译）
```

#### 2 uni中的标签

视图容器

```
  
  <view></view> 相当于div. 微信要求的标签
  
  
```



####  3 uni中的钩子函数

页面加载钩子 

```
	onLoad: function() {
			// uni.showLoading({
			// 	title: "加载中...."
			// })
			uni.request({
				url: 'https://unidemo.dcloud.net.cn/api/news',
				method: 'GET',
				data: {},
				success: res => {
					this.news = res.data;
					// uni.hideLoading();
				},
				fail: () => {},
				complete: () => {}
			});
		},
```



####   4   点击事件

   标签中，存放属性值，和取值方式。e中

```

 <view @tap="openinfo" :data-newsid="item.post_id">
 </view>

methods: {
			openinfo(e) {
				var newsid = e.currentTarget.dataset.newsid;
				console.log(newsid)
				uni.navigateTo({
					url: '../info/info?newsid=' + newsid
				});
			}
		},
```

### 5 [模板内引入静态资源](https://uniapp.dcloud.io/frame?id=模板内引入静态资源)

> `template`内引入静态资源，如`image`、`video`等标签的`src`属性时，可以使用相对路径或者绝对路径，形式如下

```html
<!-- 绝对路径，/static指根目录下的static目录，在cli项目中/static指src目录下的static目录 -->
<image class="logo" src="/static/logo.png"></image>
<image class="logo" src="@/static/logo.png"></image>
<!-- 相对路径 -->
<image class="logo" src="../../static/logo.png"></image>
```

### [js文件引入](https://uniapp.dcloud.io/frame?id=js文件引入)

> `js`文件或`script`标签内（包括renderjs等）引入`js`文件时，可以使用相对路径和绝对路径，形式如下

```js
// 绝对路径，@指向项目根目录，在cli项目中@指向src目录
import add from '@/common/add.js'
// 相对路径
import add from '../../common/add.js'
```

**注意**

- js文件不支持使用`/`开头的方式引入

### [css引入静态资源](https://uniapp.dcloud.io/frame?id=css引入静态资源)

> `css`文件或`style标签`内引入`css`文件时（scss、less文件同理），可以使用相对路径或绝对路径（`HBuilderX 2.6.6`）

```css
/* 绝对路径 */
@import url('/common/uni.css');
@import url('@/common/uni.css');
/* 相对路径 */
@import url('../../common/uni.css');
```

## 6 [生命周期](https://uniapp.dcloud.io/frame?id=生命周期)

[应用生命周期](https://uniapp.dcloud.io/frame?id=应用生命周期)

[页面生命周期](https://uniapp.dcloud.io/frame?id=页面生命周期)

vue组件的声明周期

[路由](https://uniapp.dcloud.io/frame?id=路由)

`uni-app`页面路由为框架统一管理，开发者需要在[pages.json](https://uniapp.dcloud.io/collocation/pages?id=pages)里配置每个路由页面的路径及页面样式。类似小程序在app.json中配置页面路由一样。所以 `uni-app` 的路由用法与 `Vue Router` 不同，如仍希望采用 `Vue Router` 方式管理路由，可在插件市场搜索 [Vue-Router](https://ext.dcloud.net.cn/search?q=vue-router)。

[路由跳转](https://uniapp.dcloud.io/frame?id=路由跳转)

`uni-app` 有两种页面路由跳转方式：使用[navigator](https://uniapp.dcloud.io/component/navigator)组件跳转、调用[API](https://uniapp.dcloud.io/api/router)跳转。

[页面栈](https://uniapp.dcloud.io/frame?id=页面栈)

### `pages.json` 文件的作用

`pages.json` 文件用来对 uni-app 进行全局配置，决定页面文件的路径、窗口样式、原生的导航栏、底部的原生tabbar 等。

它类似微信小程序中`app.json`的**页面管理**部分。注意定位权限申请等原属于`app.json`的内容，在uni-app中是在manifest中配置。



#### 6 组件类

uni可以使用的组件分类:

1. icon 小图标

```
<icon type="success" size="26"/>
```

2 `<text>` 组件

组件包裹文本

3  [rich-text](https://uniapp.dcloud.io/component/rich-text?id=rich-text)

```
 富文本。   <rich-text :nodes="strings"></rich-text>
 strings 可以是原生标签
```



####  map

地图组件用于展示地图，而定位API只是获取坐标，请勿混淆两者。

问题：

1.getLocation需要在app.json中声明字段

```
manifest.json   配置文件中加入配置项。 用于提示用户得到隐私数据位置。
{
"permission": {
"scope.userLocation": {
"desc": "你的位置信息将用于小程序位置判断远近的显示。"
}
},
```



## 插件市场：

###  1 格栅布局   uni-row

流式栅格系统，随着屏幕或视口分为 24 份，可以迅速简便地创建布局。

基本使用

				<uni-row class="demo-uni-row" :gutter="gutter" :width="nvueWidth">
				<uni-col :span="6" :offset="6">
					<view class="demo-uni-col dark"></view>
				</uni-col>
				<uni-col :span="6" :offset="6">
					<view class="demo-uni-col light"></view>
				</uni-col>
			</uni-row>
使用偏移

```
 <uni-col :span="12" :pull="6">
        <view class="demo-uni-col dark"></view>
    </uni-col>
    
     :push="6"
```

### 响应式布局

共五个响应尺寸：xs、sm、md、lg 和 xl

```
<uni-col :xs="8" :sm="6" :md="4" :lg="3" :xl="1">
        <view class="demo-uni-col dark"></view>
    </uni-col>
```



## **使用uView  uniapp的前端ui 框架

今日任务： uView 所有常用的插件，熟练使用。





```
{
	"easycom": {
		"^u-(.*)": "@/uview-ui/components/u-$1/u-$1.vue"
	},

	"pages": [ //pages数组中第一项表示应用启动页，参考：https://uniapp.dcloud.io/collocation/pages
		{
			"path": "pages/index/index",
			"style": {
				"navigationBarTitleText": "uni-app"
			}
		},
		{
			"path": "pages/home/home"
		},
		{
			"path": "pages/me/me"
		},
		{
			"path": "pages/plan/plan"
		},
		{
			"path": "pages/workbar/workbar"
		}
	],
	"tabBar": {
		"color": "#7A7E83",
		"selectedColor": "#3cc51f",
		"borderStyle": "black",
		"backgroundColor": "#ffffff",
		"list": [{
			"pagePath": "pages/home/home",
			"iconPath": "static/image/home.png",
			"selectedIconPath": "static/image/homeActive.png",
			"text": "首页"
		}, {
			"pagePath": "pages/me/me",
			"iconPath": "static/image/me.png",
			"selectedIconPath": "static/image/meActive.png",
			"text": "关于我"
		}]
	},
	"globalStyle": {
		"navigationBarTextStyle": "black",
		"navigationBarTitleText": "uni-app",
		"navigationBarBackgroundColor": "#F8F8F8",
		"backgroundColor": "#F8F8F8"
	}
}

```







