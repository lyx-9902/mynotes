elemnet ui   vue pc端

#### 调用父组件方法

```
console.log(this.$parent.tabelRenderEvent)
```

2020.05.15 总结：

#### form表单组

```
<el-form :inline="true" :model="formInline" class="demo-form-inline">

  <el-form-item label="审批人">
    <el-input v-model="formInline.user" placeholder="审批人"></el-input>
  </el-form-item>
  
  <el-form-item label="活动区域">
    <el-select v-model="formInline.region" placeholder="活动区域">
      <el-option label="区域一" value="shanghai"></el-option>
      <el-option label="区域二" value="beijing"></el-option>
    </el-select>
  </el-form-item>
  
  <el-form-item>
    <el-button type="primary" @click="onSubmit">查询</el-button>
  </el-form-item>
  
</el-form>
```

:label-position="labelPosition"

:inline="true"              设置 `inline` 属性可以让表单域变为行内的表单域

#### 关于form表单验证。

关键点： el-form 中加上  :rules="rules"   ，ref="ruleForm"   节点     data中准备规则。  

提交按钮  this.$refs[formName].validate((valid)   方法， 全部符合规则，返回一个valid true。

在true中， 执行接口访问。

重置按钮：  this.$refs[formName].resetFields();  。

prop="名字"   和v-model  中的名字保持一致。（ 如果不一致， 恢复按钮无效。）

检测： :rules="rules"    不加， 提交都返回true . 重置按钮 恢复初始状态值。

加上 :rules="rules"     提交按钮，自动检测规则。  规则中没有对应项，不检测。

<el-form-item prop="date1">   prop与规则无对应， 提交不检测。 props与规则对应但是与data不对应，提交检测，但是恢复无效。    所以，规则名字， prop名字，和data中的名字 保持对应。  提交和恢复都会有效。

## 项目中动态表单验证

````javascript

  <el-form-item
        v-for="(item, index) in dynamicValidateForm.domains"
        :label="'域名' + index"
        :key="item.key"
                             :prop="'domains.' + index + '.value'"
                            :rules="{
      required: true, message: '域名不能为空', trigger: 'blur'
    }"
      >
        <el-input v-model="item.value"></el-input>
        <el-button @click.prevent="removeDomain(item)">删除</el-button>
      </el-form-item>
````

关于动态的表单验证。

首先是静态的验证   form中 :rules="res_formRules",     item 中的    prop="eventDeptList"   即可。

而动态的渲染input, 按照官方方法：item中写入  rules   prop。

注意点： 如果v-for循环的是  对象中的数组。    :prop="'domains.' + index + '.value'"  的写法。  （禁止写父级的键名，直接写二级键名就可以）







#### 浏览器输出报错信息

```
 mounted:function(){
      throw Error('I was created using a function call!');

  }
```

![1597505875896](C:\Users\luyunxiao\AppData\Roaming\Typora\typora-user-images\1597505875896.png)

console.warn('[Element Warn]please pass correct props!');  打印一个提醒

![1597506152382](C:\Users\luyunxiao\AppData\Roaming\Typora\typora-user-images\1597506152382.png)

##### 关于element  input  回显    

只要，对应好value， 自动回显。 涉及到的就是，如果值不对，需要更改为vuleu取值的类型。

```
 
 blockupReason: "08",   //  阻断原因分类


```

![1598024433728](C:\Users\luyunxiao\AppData\Roaming\Typora\typora-user-images\1598024433728.png)



第二种：情况 

下拉框无法回显，原因是， 数字好字符串的原因；

选中时保存的字符串形式的数字，那么回显时，也要是字符串式的数字。

```
isBlockupTotal: "1",          // 是否完全中断
```

![1598026326508](C:\Users\luyunxiao\AppData\Roaming\Typora\typora-user-images\1598026326508.png)



# 悬浮下拉

```
    <el-dropdown @command="handleCommand">
            <span class="el-dropdown-link">
                  <el-button type="primary" icon="el-icon-plus" size='mini' circle></el-button>
            </span>
      <el-dropdown-menu slot="dropdown">
        <el-dropdown-item command="a">黄金糕</el-dropdown-item>
        <el-dropdown-item 
          v-for="item in selectList.investment_vehicle_type"
                :key="selectList.fdCode"
            :command="item.fdCode">{{ item.fdDescription }}</el-dropdown-item>
     
      </el-dropdown-menu>
    </el-dropdown>
```

这是一个回调事件，接受点击的值。

```
   handleCommand(a) { // 添加按钮
      this.resourceList1.push(  { inputCategory: "1", resourceType: a, num: "" }) 
    },
```

### 项目碰到的问题：

弹窗中的 悬浮下拉组件，下拉项使用v-for循环， 下拉数据 在父组件打开是执行了一次，在弹窗打开时，又执行了一次。  导致下拉数据为空。  

处理： 弹窗打开执行去掉。正常。

#### 项目常用的提交成功的提示

```
  this.$message({
                        type: "success",
                        message: "成功!",
                      });
```

### 图片的下载功能

# （在用项目 可使用）文件下载：event ->log 文件

```
    //文件下载
    // 入参 file：被下载文件对象
    fileDownload(file) {
      
      const loading = this.$loading({
        lock: true,
        text: "导出中",
        spinner: "el-icon-loading",
        background: "rgba(0, 0, 0, 0.7)",
      });
    //  ------
     this.$axios({
        url:
          this.$zjyhPath +
          "/yhEvent/downloadFile?fdObjectid=" +
          file.fdObjectid,
        method: "get",
        timeout: 180000,
        responseType: "blob",
      })
        .then((res) => {
          // 定义文件名等相关信息
          loading.close();
          const blob = res.data;
          if ("download" in document.createElement("a")) {
            const reader = new FileReader();
            reader.readAsDataURL(blob);
            reader.onload = (e) => {
              const a = document.createElement("a");
              var date = moment().format("YYYY-MM-DD hh:mm:ss");
              a.download = `${file.name}${date}${file.fileext}`;
              document.body.appendChild(a);
              a.href = URL.createObjectURL(blob);
              a.click();
              URL.revokeObjectURL(blob);
              document.body.removeChild(a);
            };
          } else {
            navigator.msSaveBlob(blob, `${file.name}${date}${file.fileext}`);
          }
        })
        .catch(() => {
          loading.close();
        });
    },
```

上传：

````javascript
 

this.handleForm.handleFiles.forEach((item) => {
            params.append("files", item.raw);
          });
````





项目ajax请求失败优化方案：

```
 if (code === 200) {
            this.tableData = res.data.resultData.dataList;
            this.total = res.data.resultData.total;
          } else {
            this.$message.error("查询失败");
          }
```





## 1 介绍

Element，一套为开发者、设计师和产品经理准备的基于 Vue 2.0 的组件库，提供了配套设计资源，帮助你的网站快速成型。由饿了么公司前端团队开源。

**特性：**

**一致性 Consistency**

**反馈 Feedback**

**效率 Efficiency**

**可控 Controllability**

## 2  安装  与引入

```
npm i element-ui -S
```

#### 完整引入

在 main.js 中写入以下内容：

```
import Vue from 'vue'
            import ElementUI from 'element-ui'
            import 'element-ui/lib/theme-chalk/index.css'
import App from './App.vue'

            Vue.use(ElementUI)

new Vue({
  el: '#app',
  render: h => h(App)
})
```

初始化，引入，所有组件即可以使用。

### form与layou布局混合使用

layou标签至于form标签内，不影响验证功能。

```
   <el-form label-width="140px">
   
      <el-row>
      
        <el-col :span="12">
        
          <el-form-item label="路线名称">
            <div>{{ this.tabellistdata.roadInfo}}</div>
          </el-form-item>
        </el-col>
        <el-col :span="12">
          <el-form-item label="路段名称">
            <div>{{ this.tabellistdata.roadSectionCode}}</div>
          </el-form-item>
          
        </el-col>
        
      </el-row>
      
       </el-form>
```





## 第一部分：基本部件

### 1 按钮

```
    <el-button>默认按钮</el-button>
    <el-button type="primary">主要按钮</el-button>
    <el-button type="success">成功按钮</el-button>
    <el-button type="info">信息按钮</el-button>
    <el-button type="warning">警告按钮</el-button>
    <el-button type="danger">危险按钮</el-button>

```

 注意点： el-button  控制基本样式      type="danger"  控制样式 就是颜色

### 2 Layout 布局   格栅

使用注意事项：  layout布局只控制屏幕占比。 边距和边框。 在内部加盒子控制。



格栅布局主要就是行和列的布局

```
   <el-row :gutter="10">
     <el-col :span="6"><div class="grid-content bg-purple"></div></el-col>
     <el-col :span="6"><div class="grid-content bg-purple"></div></el-col>
     <el-col :span="6"><div class="grid-content bg-purple"></div></el-col>
     <el-col :span="6"><div class="grid-content bg-purple"></div></el-col>
   </el-row>
```

![1596969010688](C:\Users\luyunxiao\AppData\Roaming\Typora\typora-user-images\1596969010688.png)

#### 参数： 

#### row  行

:gutter="10"   栅格间隔   作用是  父盒子两侧 加margin -5    子盒子 两侧加pdding -5 px

行标签上还可以设置 flex ，当父盒子 高度比较大时， 控制子盒子上对其，或者是下对齐。

<el-row :gutter="10" type='flex' align='bottom' justify='space-between' class="outbox">

#### col  列

1  <el-col :span="6"   总宽度是100%    24均分。  子元素均分。如果大于100%， 另起一行。

注意： 这只是控制宽度。 高度有子盒子的高撑起来。

2   <el-col  offset='6'>    表示    margin-left: 25%;  盒子向右侧推出指定距离。

3.<el-col :span="6" push='1'>    栅格向右移动格数  推

4  <el-col :span="6" pull='1'>   栅格向左移动格数    拉

### 3  Container 布局容器

快速搭建标准的后台管理系统的  三分布局

### 4 Color 色彩

四种标准颜色   只是16进制的色值

### 5  字体

### 6  Icon 图标

直接通过设置类名为 `el-icon-iconName` 来使用即可。例如：

```

<el-button type="primary" icon="el-icon-d-arrow-right">搜索</el-button>

<i class="el-icon-edit"></i>
```

通过i  标签， 或者是 el- 的标签内设置  icon="el-icon-d-arrow-right"。  class名按需查找。

### 7 Button 按钮

<el-button type="primary" >主要按钮</el-button>

<el-button type="primary" icon="el-icon-d-arrow-right">搜索</el-button>

### 

| 参数        | 说明           | 类型    | 可选值                                             | 默认值 |
| :---------- | :------------- | :------ | :------------------------------------------------- | :----- |
| size        | 尺寸           | string  | medium / small / mini                              | —      |
| type        | 类型           | string  | primary / success / warning / danger / info / text | —      |
| plain       | 是否朴素按钮   | boolean | —                                                  | false  |
| round       | 是否圆角按钮   | boolean | —                                                  | false  |
| circle      | 是否圆形按钮   | boolean | —                                                  | false  |
| loading     | 是否加载中状态 | boolean | —                                                  | false  |
| disabled    | 是否禁用状态   | boolean | —                                                  | false  |
| icon        | 图标类名       | string  | —                                                  | —      |
| autofocus   | 是否默认聚焦   | boolean | —                                                  | false  |
| native-type | 原生 type 属性 | string  | button / submit / reset                            | button |



解析会加上class名
.el-button  控制高宽
el-button--primary控制颜色



### 8 Link 文字链接

```
<el-link :underline="false">无下划线</el-link>
  <el-link>有下划线</el-link>
```

就是a 标签

属性有

### Attributes

| 参数      | 说明           | 类型    | 可选值                                      | 默认值  |
| :-------- | :------------- | :------ | :------------------------------------------ | :------ |
| type      | 类型           | string  | primary / success / warning / danger / info | default |
| underline | 是否下划线     | boolean | —                                           | true    |
| disabled  | 是否禁用状态   | boolean | —                                           | false   |
| href      | 原生 href 属性 | string  | —                                           | -       |
| icon      | 图标类名       | string  | —                                           | -       |

## 第二部分： form表单

## 1 Radio 单选框

基础用法 

由于选项默认可见，不宜过多，若选项过多，建议使用 Select 选择器。

要使用 Radio 组件，只需要设置`v-model`绑定变量，选中意味着变量的值为相应 Radio `label`属性的值，`label`可以是`String`、`Number`或`Boolean`。

```
<template>

  <el-radio v-model="radio" label="1">备选项</el-radio>
  <el-radio v-model="radio" label="2">备选项</el-radio>
  
</template>

<script>
  export default {
    data () {
      return {
        radio: '1'   //这个值只会是1,2其中一个值。
      };
    }
  }
</script>
```

总结： 使用el 标签， 绑定变量。  data 配置项中给个绑定值。 label控制 值是什么。

 

### 禁用状态

单选框不可点击的状态。  但可以赋予初始值，选中。



## 2 单选框多个组使用

打组使用。

```javascript
 <el-radio-group v-model="radio">
    <el-radio label="1">备选项</el-radio>
    <el-radio label="6">备选项</el-radio>
    <el-radio label="9">备选项</el-radio>
  </el-radio-group>
  
  <script>
  export default {
    data () {
      return {
        radio: 1
      };
    }
  }
</script>
```

在`el-radio-group`中绑定`v-model`，  在`el-radio`中设置好`label`即可，无需再给每一个`el-radio`绑定变量，另外，还提供了`change`事件来响应变化，它会传入一个参数`value`。

```
<el-radio-group v-model="labelPosition" size="small">
  <el-radio-button label="left">左对齐</el-radio-button>
  <el-radio-button label="right">右对齐</el-radio-button>
  <el-radio-button label="top">顶部对齐</el-radio-button>
</el-radio-group>


 data() {
    return {
       labelPosition: 'right',
   
    };
  },
```

###  表单验证

Form 组件提供了表单验证的功能，只需要通过 `rules` 属性传入约定的验证规则，并 Form-Item 的 `prop` 属性设置为需校验的字段名即可。



#### 关于表单验证：总结：

```
<el-form 

:model="ruleForm"   灌入数据1
:rules="rules"    规则2
ref="ruleForm"    节点3


">


 <el-form-item label="活动名称" prop="name"  >      4  prop
    <el-input   v-model="ruleForm.name"  ></el-input>  5v-model="ruleForm.name
  </el-form-item>
6. 如果是不能为空， 看一下是否有默认值。 有值默认符合条件。

```

#### 忽略验证的情况：

 01  表单验证中，item如果v-if =false 。 节点从页面去掉。验证通过。

02 

#### 关于循环input 的动态验证方法

案例：下面是循环的其中一项item . 

关键点是 prop="res_form.rateTemplateList[index].templateId"   动态指定值。

 :rules='res_formRules.templateId'     动态绑定规则中的内容。

```
  <el-form-item label="上传模板："
  :prop="res_form.rateTemplateList[index].templateId" :rules='res_formRules.templateId'>
                <el-select v-model="item.templateId" >  // 和这一块没有关系
                
                  <el-option
                    v-for="(item,index) in templateSelectDate"
                    :key="index"
                    :label="item.templateName"
                    :value="item.fdObjectid"
                  ></el-option>
                </el-select>
              </el-form-item>
```







### 按钮样式

只需要把`el-radio`元素换成`el-radio-button`元素即可，此外，Element 还提供了`size`属性。



```
  <el-radio-group v-model="radio3">
      <el-radio-button label="上海"></el-radio-button>
      <el-radio-button label="北京"></el-radio-button>
      <el-radio-button label="广州"></el-radio-button>
      <el-radio-button label="深圳"></el-radio-button>
    </el-radio-group>
```

### 单选的回调函数

```
<template>
  <div class="hello">

 <el-radio-group v-model="radio" @change="radio_enent">
      <el-radio-button label="上海" class="el-icon-delete"></el-radio-button>
      <el-radio-button label="北京"></el-radio-button>
      <el-radio-button label="广州"></el-radio-button>
      <el-radio-button label="深圳" icon="el-icon-search"></el-radio-button>
    </el-radio-group>

  </div>
</template>

<script>
  export default {
    name: 'HelloWorld',
    data() {
      return {
    radio: '上海'
      }
    },
    methods:{
      radio_enent:(value)=>{
            console.log(value);
      }
    }
}
</script>
```



### Radio Events

| 事件名称 | 说明                   | 回调参数              |
| :------- | :--------------------- | :-------------------- |
| change   | 绑定值变化时触发的事件 | 选中的 Radio label 值 |



## 3 Checkbox 多选框

### 基础用法

单独使用可以表示两种状态之间的切换，写在标签中的内容为 checkbox 按钮后的介绍。



在`el-checkbox`元素中定义`v-model`绑定变量，单一的`checkbox`中，默认绑定变量的值会是`Boolean`，选中为`true`。



```

<el-checkbox v-model="checked">备选项</el-checkbox>

checked: true   
```

一个dom标签  ，data中给个布尔值。  点击 布尔值变化

### 禁用状态

设置`disabled`属性即可。



### 多选框组

打组， 多选。  和单选类似。  v-model="checkList"  选中的项，以数组形式自动保存到data中。

```
<template>
  <el-checkbox-group v-model="checkList">
    <el-checkbox label="复选框 A"></el-checkbox>
    <el-checkbox label="复选框 B"></el-checkbox>
    <el-checkbox label="复选框 C"></el-checkbox>
    <el-checkbox label="禁用" disabled></el-checkbox>
    <el-checkbox label="选中且禁用" disabled></el-checkbox>
  </el-checkbox-group>
</template>

<script>
  export default {
    data () {
      return {
        checkList: ['选中且禁用','复选框 A']
      };
    }
  };
</script>
```

![1596977055528](C:\Users\luyunxiao\AppData\Roaming\Typora\typora-user-images\1596977055528.png)

### 复选框的一键全选

indeterminate 状态

`indeterminate` 属性用以表示 checkbox 的不确定状态，一般用于实现全选的效果

```
<template>
  <el-checkbox :indeterminate="isIndeterminate" v-model="checkAll" @change="handleCheckAllChange">全选</el-checkbox>
  <div style="margin: 15px 0;"></div>
  <el-checkbox-group v-model="checkedCities" @change="handleCheckedCitiesChange">
    <el-checkbox v-for="city in cities" :label="city" :key="city">{{city}}</el-checkbox>
  </el-checkbox-group>
</template>
<script>
  const cityOptions = ['上海', '北京', '广州', '深圳'];
  export default {
    data() {
      return {
        checkAll: false,
        checkedCities: ['上海', '北京'],
        cities: cityOptions,
        isIndeterminate: true
      };
    },
    methods: {
      handleCheckAllChange(val) {
        this.checkedCities = val ? cityOptions : [];
        this.isIndeterminate = false;
      },
      handleCheckedCitiesChange(value) {
        let checkedCount = value.length;
        this.checkAll = checkedCount === this.cities.length;
        this.isIndeterminate = checkedCount > 0 && checkedCount < this.cities.length;
      }
    }
  };
</script>
```

基本用法： 还是用了单个复选框， 和打组复选框。  

单选控制 全选。 点击修改data数组。   打组项用v-for="city in cities"  循环。  

### 可选项目数量的限制

使用 `min` 和 `max` 属性能够限制可以被勾选的项目的数量。

在父标签上写属性。

```
<el-checkbox-group 
    v-model="checkedCities1"
    :min="1"
    :max="2">
```

### 按钮样式

用法同上，直接更换标签。

### 按钮事件

| 事件名称 | 说明                     | 回调参数   |
| :------- | :----------------------- | :--------- |
| change   | 当绑定值变化时触发的事件 | 更新后的值 |

## 3  Input 输入框

### 基础用法

```
<el-input v-model="input" placeholder="请输入内容"></el-input>

 input: ''
```

最简单的用法，放个标签，给个值。

### 禁用状态

通过 `disabled` 属性指定是否禁用 input 组件

### 可清空

使用`clearable`属性即可得到一个可清空的输入框 

![1596979526453](C:\Users\luyunxiao\AppData\Roaming\Typora\typora-user-images\1596979526453.png)

### 带 icon图标 的输入框

可以通过 `prefix-icon` 和 `suffix-icon` 属性在 input 组件首部和尾部增加显示图标，也可以通过 slot 来放置图标。

```
<el-input
    placeholder="请选择日期"
   						 suffix-icon="el-icon-date"
    v-model="input2">
  </el-input>
```

prefix-icon` 和 `suffix-icon`  控制图标前放还是后放。 图标class 参考  组件图标。

### 可自适应文本高度的文本域 textarea

### 复合型输入框

### 带输入建议

项目使用

```
    <el-autocomplete
    clearable 
      placeholder="(默认距离中心50KM内)"
      popper-class="my-autocomplete"
      v-model="search_label"
                :fetch-suggestions="querySearch"焦点时展示的数据。callback返回形式
                 @select="handleSelect_search"    点选的回调方法
    >
    </el-autocomplete>
    
    
    
    两个方法：
      querySearch(queryString, cb) { // 获取焦点时，当前input可选数组对象
      // 调用 callback 返回建议列表的数据
      cb( [
        { value: "最近1公里内", num: "3000" },
        { value: "最近2公里内", num: "2000" },
        { value: "最近3公里内", num: "1000" },
      ]);
    },

  
    handleSelect_search(item) { //  点击下拉的值
      console.log(item);
    },
```





### 密码形式：input

```
   修改type="password"  即可
 
 <el-form-item label="确认密码" prop="checkPass">
    <el-input type="password" v-model="ruleForm.checkPass" autocomplete="off"></el-input>
  </el-form-item>
```



## 4 Select 选择器

### 1. 基础用法

`总结： v-model`的值为当前被选中的`el-option`的 value 属性值

下拉框： 使用数据分两两部分。 最终选择值的变量存放。 

  option展示选项的值。

```
<el-select v-model="value" placeholder="请选择">
    <el-option
      v-for="item in options"   // options是data中的数据。 
      :key="item.value"    // key是唯一性标识
      :label="item.label"// label是下拉的可以看到的中文名字
      :value="item.value">// value是一个选择的字符。 1 0  或者是true等
    </el-option>
  </el-select>
```

 选项是v-for 循环出来的， v-model 绑定一个data的值。

项目使用：

```
   <el-form-item label="角色">
            <el-select  multiple v-model="searchCondition.role" placeholder="请选择">
              <el-option
                v-for="item in dataAllRole" 
                :key="item.fdObjectid"
                :label="item.roleName"
                :value="item.roleCode"
              ></el-option>
            </el-select>
          </el-form-item>
```



### 禁用状态

为`el-select`设置`disabled`属性，则整个选择器不可用

```
 <el-select v-model="value" disabled placeholder="请选择">
```



### 2. 远程搜索

#### 下拉框和翻页混合使用

为了启用远程搜索，需要将`filterable`和`remote`设置为`true`，同时传入一个`remote-method`。`remote-method`为一个`Function`，它会在输入值发生变化时调用，参数为当前输入值。需要注意的是，如果`el-option`是通过`v-for`指令渲染出来的，此时需要为`el-option`添加`key`属性，且其值需具有唯一性，比如此例中的`item.value`。

```
<el-select
                  ref="roadInfo"
                  popper-class="pagina-select"
                  :popper-append-to-body="false" 
                  style="width:100%"
                  v-model="epForm.roadInfo"
                  filterable        //是否可搜索  true
                  remote             //是否为远程搜索  true            
                  placeholder="请输入关键词"
                  :remote-method="remoteMethod"   // 远程搜索方法 参数为当前输入值
                  :loading="roadCodeLoading"      // 是否正在从远程获取数据 true        
                  @change="roadCodeChange"     // 选中值发生变化时触发
                >
                  <el-option
                    :key="1"
                    :label="测试"
                    :value="1"
                  >
                  </el-option>

                </el-select>
```

测试： 

### 3 下拉多选功能：

el-select 标签中加入：multiple  多选属性



```
  <el-select  multiple v-model="searchCondition.role" placeholder="请选择">
              <el-option
                v-for="item in dataAllRole" 
                :key="item.fdObjectid"
                :label="item.roleName"
                :value="item.roleCode"
              ></el-option>
            </el-select>
```





## 5  Cascader 级联选择器   级联下拉   练级下拉

​            联动下拉框  

关键点看下面4个  

一个存储选择的值。 [ ]  是一个数组

 一个是渲染下拉   下拉数据是分层级的结构

![1597243120289](C:\Users\luyunxiao\AppData\Roaming\Typora\typora-user-images\1597243120289.png)

#### 1 下方是标准数据： 具体看官网

````javascript
     
<el-cascader
        v-model="value"    //  选择的值
        :options="options"  //  联查数据
        :props="{ expandTrigger: 'hover' }" //  点击和hover两种
        @change="handleChange" //  选择事件
      ></el-cascader>



export default {
  data() {
    return {
      value: ['一级'],
      options: [
        {
          value: "zhinan",
          label: "指南",
          children: [
          
                {
                  value: "cexiangdaohang",
                  label: "侧向导航",
                },
                {
                  value: "dingbudaohang",
                  label: "顶部导航",
                },
              ],
            },
          ],
        },
        {
          value: "zujian",
          label: "组件",
          children: [
            {
              value: "basic",
              label: "Basic",
              children: [
                {
                  value: "layout",
                  label: "Layout 布局",
                },
                {
                  value: "color",
              
                {
                  value: "radio",
                  label: "Radio 单选框",
                },
                {
                  value: "checkbox",
                  label: "Checkbox 多选框",
                
    };
  },

  methods: {
    handleChange(value) {
      console.log(value);
    },
  },
};
````

#### 2 非标准数据的调整

二级数据如果不是 child键值命名， 则无法使用。

需要自行添加配置项。  props 中配置。

#### 使用props设置value、label、children

从后端拿到arr数据结构：

```
cityList: [
	{
		id: 1,
		name: '北京',
		child: [
			id: 11,
			name: '大兴区',
			child: [
				id: 111,
				name: '亦庄'
			]
		]
	}
]

```

vue文件代码

```
<el-cascader
    :options="cityList"
    :props="optionProps"
    v-model="selectedOptions"
    @change="handleChange">
</el-cascader>

```

js

备注： 下面的写法等于行内的写法。

```
data: {
	optionProps: {
		value: 'id',
		label: 'name',
		children: 'child'
	}
}

```

等同于：

```
      <el-cascader
              v-model="searchCondition.orgCode"
              :options="userOrg"
:props="{ expandTrigger: 'hover' , label:'name', value:'distsCode' }"   <---
              @change="listUasOrghandleChange">
              </el-cascader>
              
              
  备注：  指定数据中的哪一项作为value获取值 ，label的显示值。               
```



项目中使用：   组织机构连级下拉

所用的工具函数

1. 源数据    
2. 数据特点：每一组数据，都有自己的id. 有自己归属的father id。  需要的数据格式   有二级的数据，加一个child [] 项。

```
{ 
distsCode: "330000"
distsName: "浙江省"
fdObjectid: "1"
id: "33000001"
name: "省公路与运输管理中心"
orgOrder: null
orgType: "province"
orgTypeName: "省级机构"
pId: "0"
remark: ""  }
```

3. 工具函数：

   使用方法：  

```
/**
     * @description 处理级联数据
     * @param {array} data 被处理数据
     * @return {array} 处理后数据
     */
    setUnitList(data) {
                               var _id = "id";     自己的id
                             var _pid = "pId";      papent id 指明
                       var _children = "children";   （二级数据以什么键名字）
      var map = {};
      data.forEach(function (item) {
        if (!item[_pid]) {
          item[_pid] = "~";
        }
        var _idval = item[_id].toString();
        map[_idval] = item;
      });
      var val = [];
      data.forEach(function (item) {
        var _pidval = item[_pid].toString();
        var parent = map[_pidval];
        if (parent) {
          (parent[_children] || (parent[_children] = [])).push(item);
        } else {
          val.push(item);
        }
      });
      return val;
    },
```

4. 使用的标签和 键值指定 props

```
  <el-form-item label="组织">
            <el-cascader
              v-model="searchCondition.orgCode"
              :options="userOrg"
              :props="{ expandTrigger: 'hover' , label:'name', value:'distsCode' }"
              @change="listUasOrghandleChange">
              </el-cascader>
          </el-form-item>
```







### 基础多选

为`el-select`设置`multiple`属性即可启用多选，此时`v-model`的值为当前选中值所组成的数组。默认情况下选中值会以 Tag 的形式展现，你也可以设置`collapse-tags`属性将它们合并为一段文字。

## 6  Switch 开关

### 基本用法

绑定`v-model`到一个`Boolean`类型的变量。可以使用`active-color`属性与`inactive-color`属性来设置开关的背景色。

设置`active-value`和`inactive-value`属性，接受`Boolean`, `String`或`Number`类型的值。

```
<el-switch
  v-model="value2"
  active-color="#13ce66"
  inactive-color="#ff4949">
</el-switch>

<script>
  export default {
    data() {
      return {
      
        value2: true
      }
    }
  };
</script>
```

## 7  TimePicker  日期选择器

使用 el-time-select 标签，分别通过`star`、`end`和`step`指定可选的起始时间、结束时间和步长

总结：1 放置时间标签

2 准备变量结果值存储

```
    <el-time-picker
    v-model="value2"   //存储选择结果的值
    :picker-options="{  //限制可选时间范围
      selectableRange: '18:30:00 - 20:30:00'
    }"
    placeholder="任意时间点">
  </el-time-picker>
  
  
  
  value2: new Date(2016, 9, 10, 18, 40),   一个变量存储选择结果值
```

 

@change ='changeevent'   写在时间标签内

### Events

| 事件名 | 说明                   | 参数       |
| :----- | :--------------------- | :--------- |
| change | 用户确认选定的值时触发 | 组件绑定值 |

## 8 DatePicker 日期选择器

和timepicker类似。

### 选择日

### 其他日期单位

### 选择日期范围

### 日期格式



如果是时间范围，则data是一个数组。

```
   <el-date-picker
      v-model="value6"
      type="year"  // 控制显示周  年 日 或者显示周 选择器
    value-format = 'yyyy-MM-dd-HH-mm'   时间格式  可以自定义
    @change='changeevent'  时间确定后的回调函数
      
      >
    </el-date-picker>
```

### 项目使用时间格式

```
    <el-time-picker
                type="datetime"
               format="yyyy-MM-dd HH:mm"     显示在输入框中的格式
              value-format=" yyyy-MM-dd HH:mm"   可选，绑定值的格式。不指定则绑定值为 Date 对象
                v-if=" item.type==='time' "
                v-model="formdata[item.code]"
                placeholder="时间点"
              ></el-time-picker>
```

### **时间选择器遇到的问题：

   日期，时间，选择器的标签不一样，转换显示格式的时候，可能需要更换标签。

value-format="timestamp"   关于后台传递datatime格式的时间字段

后台数据报错，先看报错信息。

![1598505380338](C:\Users\luyunxiao\AppData\Roaming\Typora\typora-user-images\1598505380338.png)



2020.0827 出现数据库格式无法校验成功。

原因是：

```
 <el-date-picker
                type="datetime"
                        format="yyyy-MM-dd HH:mm"
                                     value-format="yyyy-MM-dd HH:mm"  <--- 这里不能留空格
                v-if=" item.type==='time' "
                v-model="formdata[item.code]"
                placeholder="时间点"
              ></el-date-picker>
```



## 9 Upload 上传

使用： 放置上传标签

总结： 一个upload标签， 所有的属性和方法都放到里面。

包含接口的调试。

```
<el-upload
  class="upload-demo"
  action="https://jsonplaceholder.typicode.com/posts/"   //	必选参数，上传的地址
  :on-preview="handlePreview"  点击文件列表中已上传的文件时的钩子function(file)
  :on-remove="handleRemove" 文件列表移除文件时的钩子	function(file, fileList)
  :before-remove="beforeRemove"
  multiple  	是否支持多选文件
  :limit="3"   最大允许上传个数    number
  :show-file-list="false"  已上传图片以列表显示
  :on-exceed="handleExceed"	文件超出个数限制时的钩子	function(files, fileList)
  :file-list="fileList"   上传的文件列表  [], 
   list-type="text"  文件列表的类型text/picture/picture-card  以图片显示还是文字
  >
  <el-button size="small" type="primary">点击上传</el-button>
  <div slot="tip" class="el-upload__tip">只能上传jpg/png文件，且不超过500kb</div>
</el-upload>
```

上传功能：包含图片。world excel 等文件的上传。

 下载功能： 查看文件的头部的项目总结。

### 使用总结：

初次粘贴官网 案例，上传图片时，查看绑定的数组，没有任何变化。 

粘贴项目中使用的案例，可以看到数据的变化。如下代码：

```
<el-upload
  class="upload-demo"
  action="https://jsonplaceholder.typicode.com/posts/"
  :on-preview="handlePreview"
  :on-remove="handleRemove"
  :before-remove="beforeRemove"
  multiple
  :limit="3"
  :on-exceed="handleExceed"
  :file-list="fileList">
  <el-button size="small" type="primary">点击上传</el-button>
  <div slot="tip" class="el-upload__tip">只能上传jpg/png文件，且不超过500kb</div>
</el-upload>


imgList :[
{name:"图片2 - 副本.jpg"
percentage:0
raw:File
size:37491
status:"ready"
uid:1616075196984}
]   ， 总结： 原因是，项目案例在上传图片时，通过回调，实时保存上传的图片数据，所以看到数据变化。
图片的页面回显：  只需要在绑定的数据中， push进去 {name:"图片名字.png"}, 如果有url 属性，也可以回显图片。
例如： 
fileList: 
[
{name:"我是测试图片名字",
url: 'https://fuss10.elemecdn.com/3/63/4e7f3a15429bfda99bce42a18cdd1jpeg.jpeg?imageMogr2/thumbnail/360x360/format/webp/quality/100'}, ],
```







## 10  Form 表单 综合

由输入框、选择器、单选框、多选框等控件组成，用以收集、校验、提交数据

在 Form 组件中，每一个表单域由一个 Form-Item 组件构成，表单域中可以放置各种类型的表单控件，包括 Input、Select、Checkbox、Radio、Switch、DatePicker、TimePicker

form 

```
<template>
  <div>
<!-- form开始 -->
    <el-form ref="form" :model="form" label-width="80px">
<!-- 第一个 -->
      <el-form-item label="活动名称">
        <el-input v-model="form.name"></el-input>
      </el-form-item>

<!-- 第二个 -->
      <el-form-item label="即时配送">
        <el-switch v-model="form.delivery"></el-switch>
      </el-form-item>
<!-- 第三 个 -->
      <el-form-item>
        <el-button type="primary" @click="onSubmit">立即创建</el-button>
        <el-button>取消</el-button>
      </el-form-item>

    </el-form>
<!-- form结束 -->
  </div>
</template>

<script>
export default {
  data() {
    return {
      form: {
        name: "",
        region: "",
        date1: "",
        date2: "",
        delivery: false,
        type: [],
        resource: "",
        desc: "",
      },
    };
  },
  methods: {
    onSubmit() {
      console.log("submit!");
    },
  },
};
</script>
```

#### form使用规则

<!-- form表单，有多个表单组件构成。 
注意点： 数据以对象方式，form 属性方式 注入。传值。  :model="formInline"
子项： label 是单个表单的label名字。 
v-model="formInline.user"  绑定选择的值。 --> v-model="formInline.user"  

一般用于 以数组形式保存form的全部的用户选择的值。

```
<template>
  <div>

<el-form :inline="true" :model="formInline" class="demo-form-inline">


  <el-form-item label="审批人">
    <el-input v-model="formInline.user" placeholder="审批人"></el-input>
  </el-form-item>


  <el-form-item label="活动区域">
    <el-select v-model="formInline.region" placeholder="活动区域">
      <el-option label="区域一" value="shanghai"></el-option>
      <el-option label="区域二" value="beijing"></el-option>
    </el-select>
  </el-form-item>


  <el-form-item>
    <el-button type="primary" @click="onSubmit">查询</el-button>
  </el-form-item>


</el-form>


  </div>
</template>

<script>
export default {
  data() {
    return {
     formInline: {
          user: '',
          region: ''
        }
    };
  },
  methods: {
    onSubmit() {
      console.log("submit!");
    },
  },
};
</script>
```

### 数据绑定

   el-form  :model="formInline"

![1597332771898](C:\Users\luyunxiao\AppData\Roaming\Typora\typora-user-images\1597332771898.png)

```
<script>
export default {
  data() {
    return {
     formInline: {
          user: '',
          region: ''
        }
    };
  },
  methods: {
    onSubmit() {
      console.log("submit!");
    },
  },
};
</script>
```



### 对齐方式

通过设置 `label-position` 属性可以改变表单域标签的位置，可选值为 `top`、`left`，当设为 `top` 时标签会置于表单域的顶部

```
<el-form :label-position="labelPosition" label-width="80px" :model="formLabelAlign">

<el-form>  在form上设置
```

### 表单验证  required 触发方式

实现校验成功   需要这两个属性配合使用。 

:rules="rules" ref="ruleForm"  

一个注入规则，一个点击时，校验，合格则返回一个布尔值。

<el-form :model="ruleForm" :rules="rules" ref="ruleForm" label-width="100px" class="demo-ruleForm">

:model="ruleForm"   灌入数据

:rules="rules"  灌入验证规则

ref="ruleForm"    获取指定的dom。  注意点： 如果修改变量名，下面按钮的传值也要跟这变，

item项：

  <el-form-item label="活动名称" prop="name1">   prop="name1  是    rules中的name1  验证 
    <el-input v-model="ruleForm.name"></el-input>   v-model="ruleForm.name"  
  </el-form-item>

提交按钮要在form中。

​    ![1597337305932](C:\Users\luyunxiao\AppData\Roaming\Typora\typora-user-images\1597337305932.png)

     resetForm(formName) {  这里接受的时形参。 对应错误将找不到方法。
     
           this.$refs[formName].resetFields();
      }
```
<template>
  <div>


<el-form :model="ruleForm" :rules="rules" ref="ruleForm" label-width="100px" class="demo-ruleForm">
  
  <el-form-item label="活动名称" prop="name1">
    <el-input v-model="ruleForm.name"></el-input>
  </el-form-item>

  <el-form-item label="活动区域" prop="region">
    <el-select v-model="ruleForm.region" placeholder="请选择活动区域">
      <el-option label="区域一" value="shanghai"></el-option>
      <el-option label="区域二" value="beijing"></el-option>
    </el-select>
  </el-form-item>

  <el-form-item label="活动时间" required>
    <el-col :span="11">
      <el-form-item prop="date1">
        <el-date-picker type="date" placeholder="选择日期" v-model="ruleForm.date1" style="width: 100%;"></el-date-picker>
      </el-form-item>
    </el-col>
    <el-col class="line" :span="2">-</el-col>
    <el-col :span="11">
      <el-form-item prop="date2">
        <el-time-picker type="fixed-time" placeholder="选择时间" v-model="ruleForm.date2" style="width: 100%;"></el-time-picker>
      </el-form-item>
    </el-col>
  </el-form-item>

  <el-form-item label="即时配送" prop="delivery">
    <el-switch v-model="ruleForm.delivery"></el-switch>
  </el-form-item>



  <el-form-item>
    <el-button type="primary" @click="submitForm('ruleForm')">立即创建</el-button>
    <el-button @click="resetForm('ruleForm')">重置</el-button>
  </el-form-item>

</el-form>


  </div>
</template>

<script>
export default {
    data() {
      return {
        ruleForm: {
          name: '',
          region: '',
          date1: '',
          date2: '',
          delivery: false,
          type: [],
          resource: '',
          desc: ''
        },
        rules: {
          name1: [
            { required: true, message: '请输入活动名称', trigger: 'blur' },
            { min: 3, max: 5, message: '长度在 3 到 5 个字符', trigger: 'blur' }
          ],
          region: [
            { required: true, message: '请选择活动区域', trigger: 'change' }
          ],
          date1: [
            { type: 'date', required: true, message: '请选择日期', trigger: 'change' }
          ],
          date2: [
            { type: 'date', required: true, message: '请选择时间', trigger: 'change' }
          ],
          type: [
            { type: 'array', required: true, message: '请至少选择一个活动性质', trigger: 'change' }
          ],
          resource: [
            { required: true, message: '请选择活动资源', trigger: 'change' }
          ],
          desc: [
            { required: true, message: '请填写活动形式', trigger: 'blur' }
          ]
        }
      };
    },
    methods: {
      submitForm(formName) {

        this.$refs[formName].validate((valid) => {
          if (valid) {
            alert('submit!');
          } else {
            console.log('error submit!!');
            return false;
          }
        });
      },

      
      resetForm(formName) {
    
        this.$refs[formName].resetFields();
      }
    }
  }
</script>
```

### rule规则

 :rules  对应规则。  prop  对应data中的值。

```
rules: {
          name: [
            { required: true, message: '请输入活动名称', trigger: 'blur' },
            { min: 3, max: 5, message: '长度在 3 到 5 个字符', trigger: 'blur' }
          ],
          region: [
            { required: true, message: '请选择活动区域', trigger: 'change' }
          ],
          date1: [
            { type: 'date', required: true, message: '请选择日期', trigger: 'change' }
          ],
          date2: [
            { type: 'date', required: true, message: '请选择时间', trigger: 'change' }
          ],
          type: [
            { type: 'array', required: true, message: '请至少选择一个活动性质', trigger: 'change' }
          ],
          resource: [
            { required: true, message: '请选择活动资源', trigger: 'change' }
          ],
          desc: [
            { required: true, message: '请填写活动形式', trigger: 'blur' }
          ]
        }
        
        
         { type: 'number', message: 'paramValue必须为数字值'}
```

![1597338848585](C:\Users\luyunxiao\AppData\Roaming\Typora\typora-user-images\1597338848585.png)



#### rule的  item写法

```
     <el-form-item label="年龄" prop="age"  :rules='[
          { required: true, message: "年龄不能为空" ,trigger: "blur"},
          { type: "number", message: "年龄必须为数字值" ,trigger: "blur"},
        ]'>
        <el-input type="age" v-model.number="numberValidateForm.age"   autocomplete="off"></el-input>
      </el-form-item>
```

注意点：   双引号和单引号的问题   :rules  对应规则。  prop  对应data中的值。

### 自定义表单验证

![1597507647163](C:\Users\luyunxiao\AppData\Roaming\Typora\typora-user-images\1597507647163.png)



```
<template>
  <div class="hello">
    <el-form
      :model="ruleForm"
      status-icon
      :rules="rules"
      ref="ruleForm"
      label-width="100px"
      class="demo-ruleForm"
    >
      <el-form-item label="密码" prop="pass">
        <el-input type="password" v-model="ruleForm.pass" autocomplete="off"></el-input>
      </el-form-item>

      <el-form-item label="确认密码" prop="checkPass">
        <el-input type="password" v-model="ruleForm.checkPass" autocomplete="off"></el-input>
      </el-form-item>

      <el-form-item label="年龄" prop="age">
        <el-input v-model.number="ruleForm.age" ></el-input>
      </el-form-item>

      <el-form-item>
        <el-button type="primary" @click="submitForm('ruleForm')">提交</el-button>
        <el-button @click="resetForm('ruleForm')">重置</el-button>
      </el-form-item>

    </el-form>
  </div>
</template>
<script>
export default {
  data() {
    var checkAge = (rule, value, callback) => {
      // console.log(rule)
      // console.log(value)  //输入框的值
      // console.log(callback)  //回调函数  输入框中的错误 显示文字

      if (!value) {
        return callback(new Error("年龄不能为空"));
      }
      setTimeout(() => {
        if (!Number.isInteger(value)) {
          callback(new Error("请输入数字值"));
        } else {
          if (value < 18) {
            callback(new Error("必须年满18岁"));
          } else {
            callback();
          }
        }
      }, 1000);
    };
    var validatePass = (rule, value, callback) => {
      if (value === "") {
        callback(new Error("请输入密码"));
      } else {
        if (this.ruleForm.checkPass !== "") {
          this.$refs.ruleForm.validateField("checkPass"); // 对表单的部分字段检测
        }
        callback();
      }
    };
    var validatePass2 = (rule, value, callback) => {
      if (value === "") {
        callback(new Error("请再次输入密码"));
      } else if (value !== this.ruleForm.pass) {
        callback(new Error("两次输入密码不一致!"));
      } else {
        callback();
      }
    };
    return {
      ruleForm: {
        pass: "",
        checkPass: "",
        age: "",
      },
      rules: {
        pass: [{ validator: validatePass, trigger: "blur" }],
        checkPass: [{ validator: validatePass2, trigger: "blur" }],
        age: [{ validator: checkAge, trigger: "blur" }],
      },
    };
  },
  methods: {

    submitForm(formName) {
      this.$refs[formName].validate((valid) => {
        if (valid) {
          alert("submit!");
        } else {
          console.log("error submit!!");
          return false;
        }
      });
    },

    resetForm(formName) {
      this.$refs[formName].resetFields();
    },

  }

};
</script>
```

自定义验证与form验证的区别是data规则自定义部分

```
  data() {
    var checkAge = (rule, value, callback) => {
      if (!value) {
        return callback(new Error("年龄不能为空"));
      }
      setTimeout(() => {
        if (!Number.isInteger(value)) {
          callback(new Error("请输入数字值"));
        } else {
          if (value < 18) {
            callback(new Error("必须年满18岁"));
          } else {
                                       callback(); < ---  必须reture 
          }
        }
      }, 1000);
    };
 

    return {
      ruleForm: {
  
        age: "",
      },
      rules: {
        age: [{ validator: checkAge, trigger: "blur" }],
      },
    };
  },
```

validator  新属性。 用于自定义配置。 和 trigger触发方式

项目使用：

#### 第一：

在data中定义规则，注意不是return之中。

  data() {

//定义规则

  return { }

}

#### 第二：

配置触发

```
  rolerule: {
            name: [ { required: true, message: '角色名称不可重复', trigger: 'blur' },
  配置属性validator-------->  {validator: checkname, trigger: 'blur' }, ],
                code: [{ required: true, message: '必填项', trigger: 'blur' }],
               },
```

#### 第三

回调函数，抛出错误方法

return callback(new Error('年龄不能为空'));

```
  var checkname = (rule, value, callback) => {
      console.log(value)
        if (!value) {
          return callback(new Error('年龄不能为空'));
        }
        setTimeout(() => {
         
        }, 1000);


      };
```

#### 关于自定义验证的必须条件      callback(); < ---  必须reture 







### form表单的和layout的配合使用

可能出现的问题：  input输入中文的时候， 输入框可能布局变化，可能高度变化。 解决方案：不用layout布局。

```

    <el-form ref="form" label-width="80px">
      <el-row>
      
        <el-col :span="6">
        
          <el-form-item label="活动名称">
            <el-input></el-input>
          </el-form-item>
          
        </el-col>
       
      
        <el-col :span="6" >
          <el-button size="small" type="primary">新增</el-button>
          <el-button size="small" type="primary">导出</el-button>
        </el-col>
        
      </el-row>
      
    </el-form>
```



## 11  穿梭框

####  1.基础使用

```
 <el-transfer 
         v-model="value" 
         :data="data"
 ></el-transfer>
 

  data: [
  {"key":8,
  "label":"备选项 8",
  "disabled":false},
  ],                         //第一个数组是待选项model   对象中包含三个属性：key label disable
   value: [1,2,3]       ,   //第二个数组是已选项data
```



### 两侧默认选中。

```
    <el-transfer
            style="text-align: left; display: inline-block"
            v-model="value1"
            filterable
            :left-default-checked="[2, 3]"     左侧默认选中    key值
            :right-default-checked="[1]"    //右侧默认选中
            :render-content="renderFunc"
            :titles="['待选', '已选']"
            :format="{
                noChecked: '${total}',
                hasChecked: '${checked}/${total}'}"
            @change="handleChange"
            :data="data"
          ></el-transfer>
```

@change="handleChange"

```
   handleChange(value, direction, movedKeys) {
      // console.log(value, direction, movedKeys);
      console.log(  direction);
      console.log(  value);
      console.log(  movedKeys);

    },    回调接受三个值。  一个是移动方向 一个是移动的但前值。一个是移动组的所剩余的值组。
```



```
  <el-transfer
                style="text-align: left; display: inline-block"
                                         v-model="shuttleInput"  2.选中的key集合
                filterable     
                :render-content="renderFunc"  //自定义渲染函数  03 见下方案例
                :titles="['待选', '已选']"

                :format="{
                noChecked: '${total}',
                hasChecked: '${checked}/${total}'
                }"

                @change="handleChange"
                @right-check-change="rightHandleChange"
                                       :data="shuttledata"   1. 数据输入
              ></el-transfer>
```

#### 自定义渲染函数

```
   案例 03    renderFunc(h, option) { // 穿梭框自定义结构
        return (
          <span>
            {option.key} - {option.label}
          </span>
        );
      },
```

自定义数据格式

标准数据是： label value  disable   ; 如果不是标准数据，可以props中指定。

```

:props="{key: 'fdObjectid',label: 'deviceName',disabled: true}"

```

右侧选中，

```
  // 视频区数据
      shuttledata: [
        { key: 1, label: "备选项 1", disabled: false },
        { key: 2, label: "备选项 2", disabled: false },
      ],
      shuttleInput: [], // 穿梭框已选中变量
```



### 关于穿梭框key重复的问题

```
data: [
          {value:1,desc:'选项1',disabled:false},
          // {value:1,desc:'选项11',disabled:false},
          {value:2,desc:'选项2',disabled:false},
          {value:3,desc:'选项3',disabled:false},
          ],
        value: [1,1]
```

data中有重复的value时，会报错。

value,有重复的值，不会报错。





# 第三部分： Data



## 1  Table 表格

#### 在table中  prop  是data值 

当`el-table`元素中注入`data`对象数组后，在`el-table-column`中用`prop`属性来对应对象中的键名即可填入数据，用`label`属性来定义表格的列名。可以使用`width`属性来定义列宽。

```
 <el-table
      :data="tableData"
      style="width: 100%">
      
      <el-table-column
        prop="date"
        label="日期"
        width="180">
      </el-table-column>
      
      <el-table-column
        prop="name"
        label="姓名"
        width="180">
      </el-table-column>
      
      <el-table-column
        prop="address"
        label="地址">
      </el-table-column>
      
    </el-table>
    
    
      tableData: [{
                 date: '2016-05-02',
                 name: '王小虎',
                 address: '上海市普陀区金沙江路 1518 弄'
               }, {
                 date: '2016-05-04',
                 name: '王小虎',
                 address: '上海市普陀区金沙江路 1517 弄'
               }, {
                 date: '2016-05-01',
                 name: '王小虎',
                 address: '上海市普陀区金沙江路 1519 弄'
               }, {
                 date: '2016-05-03',
                 name: '王小虎',
                 address: '上海市普陀区金沙江路 1516 弄'
               }
```

父标签 注入数据

<el-table-column
        prop="name"    //注入数据
        label="姓名"     // 表格名字
        width="180">
      </el-table-column>

![1597335282253](C:\Users\luyunxiao\AppData\Roaming\Typora\typora-user-images\1597335282253.png)



#### 2  斑马纹的表格

el-table  中直接放入属性：    stripe（ n. 条纹，斑纹；种类）

### 3 带边框表格

el-table  中直接放入属性：    border

### 4  带状态表格 高亮行背景色

根据数据状态添加背景色

可以通过指定 Table 组件的 `row-class-name` 属性来为 Table 中的某一行添加 class，表明该行处于某种状态。

```
 <el-table
      :data="tableData"
      style="width: 100%"
 
         :row-class-name="tableRowClassName"
      >
      
      
      methods: {
      tableRowClassName({row, rowIndex}) {

        if (row.active === 0) {
          return 'warning-row';
        } else {
          return 'success-row';
        }
      }
    },   
      
```

tableRowClassName  添加事件， 回调参数是每行的数据和index .  每条数据条用一次。 return   class名字。

配合 css 区分颜色。

### 5  固定表头

只要在`el-table`元素中定义了`height`属性，即可实现固定表头的表格，而不需要额外的代码。

el-table    标签中 添加   height="150"  一个高度。

### 6 固定列

横向内容过多时，可选择固定列

固定列需要使用`fixed`属性，它接受 Boolean 值或者`left``right`，表示左边固定还是右边固定。



```
 <el-table-column fixed prop="date" label="日期" width="150"></el-table-column>
```

方法是： 在column中 添加 fixed   . 想固定那一列就添加在哪一行。

![1597515790460](C:\Users\luyunxiao\AppData\Roaming\Typora\typora-user-images\1597515790460.png)

### 7   传值  操作栏按钮

###  slot-scope="scope"  

场景： 表格的点击事件中， 传入本行的数据。

```
    <el-table-column fixed="right" label="操作" width="100">

        <template slot-scope="scope">
        
 <el-button @click="handleClick(scope.row)" type="text" size="small">查看</el-button>
  
        </template>

      </el-table-column>
```



### 8  固定列和表头

横纵内容过多时，可选择固定列和表头。

固定列和表头可以同时使用，只需要将上述两个属性分别设置好即可。

### 9 流体高度

当数据量动态变化时，可以为 Table 设置一个最大高度。

通过设置`max-height`属性为 Table 指定最大高度。此时若表格所需的高度大于最大高度，则会显示一个滚动条。

table 标签中 放置   max-height="250"     控制最大高度。 

### 10多级表头

只需要在 el-table-column 里面嵌套 el-table-column，就可以实现多级表头。

![1597517626090](C:\Users\luyunxiao\AppData\Roaming\Typora\typora-user-images\1597517626090.png)

```
 <el-table-column label="地址">
      <el-table-column prop="address" label="地址" width="300"></el-table-column>
      <el-table-column prop="zip" label="邮编" width="120"></el-table-column>
      <el-table-column fixed="right" label="操作" width="100">
 </el-table-column>
```

column  标签包裹

### 11 单选   点击变色  行

able 组件提供了单选的支持，只需要配置`highlight-current-row`属性即可实现单选。之后由`current-change`事件来管理选中时触发的事件，它会传入`currentRow`（ 点击行的数据），`oldCurrentRow`。如果需要显示索引，可以增加一列`el-table-column`，设置`type`属性为`index`即可显示从 1 开始的索引号。

关键点 :  el-table 标签中   

```

<el-table
    ref="singleTable"
    :data="tableData"
                          highlight-current-row    这一个属性
                           @current-change="handleCurrentChange"   方法
    style="width: 100%">
    
    
```

指定行背景色改变。两种方式：一种是点击表格，所在行变色。  一种是不惦记表格， 函数触发变色。

1.  点击表格变色：  highlight-current-row   加属性即可。 如果想获取点击行的数据，方法：@current-change="handleCurrentChange"

````javascript
 handleCurrentChange(val) {
      console.log(val);
      this.currentRow_ = val;
    },
````

2  函数式变色：

```
 ref="singleTable"
 table标签加上ref  属性。获取dom指定表格
   
   
   <div style="margin-top: 20px">
      <el-button @click="setCurrent(tableData[3])">选中第二行</el-button>
      <el-button @click="setCurrent()">取消选择</el-button>
    </div>
    
    
      methods: {
    setCurrent(row) {
      this.$refs.singleTable.setCurrentRow(row);
    },
    
    
    
    
```



#### 表格  首列 index显示

如果需要显示索引，可以增加一列`el-table-column`，设置`type`属性为`index`即可显示从 1 开始的索引号。

```
 <el-table-column type="index" width="50"></el-table-column>
      <el-table-column property="date" label="日期" width="120"></el-table-column>
```

### 12 多选  获取多行的数据

选择多行数据时使用 Checkbox。

实现多选非常简单: 手动添加一个`el-table-column`，设`type`属性为`selection`即可；默认情况下若内容过多会折行显示，若需要单行显示可以使用`show-overflow-tooltip`属性，它接受一个`Boolean`，为`true`时多余的内容会在 hover 时以 tooltip 的形式显示出来

关键点： 

手动添加一个`el-table-column`，设`type`属性为`selection`即可。 可以进行多选。 如果想获取选中的几行数据。使用方法

```
 <el-table
      ref="multipleTable"
      :data="tableData"
      tooltip-effect="dark"
      style="width: 100%"
      @selection-change="handleSelectionChange"
    >
```

方法 methods : 

```
handleSelectionChange(val) {
      console.log(val);
      this.multipleSelection = val;
    },
    
    data中准备
    multipleSelection: [],
    
```



#### 函数式 选中几行事件

```
   <div style="margin-top: 20px">
      <el-button @click="toggleSelection([tableData[1], tableData[2]])">切换第二、第三行的选中状态</el-button>
      <el-button @click="toggleSelection()">取消选择</el-button>
    </div>
```

```
  methods: {
    toggleSelection(rows) {
      if (rows) {
        rows.forEach((row) => {
          this.$refs.multipleTable.toggleRowSelection(row);
        });
      } else {
        this.$refs.multipleTable.clearSelection();
      }
    },
```

 和上面一样。 注意点： 方法使用需要指定tabel  。 ref属性加上。

<el-table

​      ref="multipleTable"

### 13   排序

在列中设置`sortable`属性即可实现以该列为基准的排序，接受一个`Boolean`，默认为`false`。可以通过 Table 的`default-sort`属性设置默认的排序列和排序顺序。可以使用`sort-method`或者`sort-by`使用自定义的排序规则。如果需要后端排序，需将`sortable`设置为`custom`，同时在 Table 上监听`sort-change`事件，在事件回调中可以获取当前排序的字段名和排序顺序，从而向接口请求排序后的表格数据。在本例中，我们还使用了`formatter`属性，它用于格式化指定列的值，接受一个`Function`，会传入两个参数：`row`和`column`，可以根据自己的需求进行处理。

第一种： 列排序 ，想那列可以排序，就在列上加上属性： 

sortable  表明可以排序

```
 <el-table-column prop="name" label="姓名" sortable width="180"></el-table-column>
```

第二种： 设置默认排序

 :default-sort="{prop: 'date', order: 'descending'}"   设置默认的  排序列   和    排序顺序

```
    <el-table
      :data="tableData"
      style="width: 100%"
      :default-sort="{prop: 'date', order: 'descending'}"
    >
      <el-table-column prop="date" label="日期"  width="180"></el-table-column>
      <el-table-column prop="name" label="姓名" sortable width="180"></el-table-column>
      <el-table-column prop="address" label="地址" :formatter="formatter"></el-table-column>
    </el-table>
```

监听排序变化

列设置为可以排序后，监听事件，

```
 <el-table
      :data="tableData"
      style="width: 100%"
      @sort-change='change'

    >
    
    方法： 
      methods: {
change(val){
  console.log(val);

},
```



### 对列数据进行加后缀

对数组显示做处理

在本例中，我们还使用了`formatter`属性，它用于格式化指定列的值，接受一个`Function`，会传入两个参数：`row`和`column`，可以根据自己的需求进行处理。

想处理哪一行： :="formatter" 绑定方法;  

```
    <el-table
      :data="tableData"
      style="width: 100%"
      @sort-change='change'

 <el-table-column prop="address" label="地址" :formatter="formatter"></el-table-column>
 
    </el-table>
```

方法， 数据渲染是，自动过滤每一行，进行数据处理。  统一判断加后缀等。比如返回不同的按钮等。

```
  methods: {

    formatter(row, column) {
      // console.log(row);  行信息 
      // console.log(column);  列信息
      return row.name+ '   后缀';
    },
  },
```

像如下方法：使用场景

```
  formatter(row, column) {
      console.log(row);  
   if(row.name=="张三"){
     return "危险分子"
   }else{
     return row.address+ '   后缀';
   }
      
    },
```

### 14  筛选   过滤器

对表格进行筛选，可快速查找到自己想看的数据。

在列中设置`filters``filter-method`属性即可开启该列的筛选，filters 是一个数组，`filter-method`是一个方法，它用于决定某些数据是否显示，会传入三个参数：`value`, `row` 和 `column`。

```
      <el-table-column
        prop="date"
        label="日期"
        :filters="[{text: '2016-05-03', value: '2016-05-03'}, {text: '2016-05-04', value: '2016-05-04'}]"
        :filter-method="filterHandler"
      ></el-table-column>
```



完整代码: 

```
<template>
  <div>

    <el-button @click="resetDateFilter">清除日期过滤器</el-button>
    <el-button @click="clearFilter">清除所有过滤器</el-button>


    <el-table ref="filterTable" :data="tableData" style="width: 100%">

      <el-table-column
        prop="date"
        label="日期"
        sortable
        width="180"
        column-key="date"
        :filters="[{text: '2016-05-20', value: '2016-05-20'}, {text: '2016-05-02', value: '2016-05-02'}, {text: '2016-05-03', value: '2016-05-03'}, {text: '2016-05-04', value: '2016-05-04'}]"
        :filter-method="filterHandler"
      ></el-table-column>

      <el-table-column prop="name" label="姓名" width="180"></el-table-column>
      <el-table-column prop="address" label="地址" :formatter="formatter"></el-table-column>
      
      <el-table-column
        prop="tag"
        label="标签"
        width="100"
        :filters="[{ text: '家', value: '家' }, { text: '公司', value: '公司' }]"
        :filter-method="filterTag"
        filter-placement="bottom-end"
      >
        <template slot-scope="scope">
          <el-tag
            :type="scope.row.tag === '家' ? 'primary' : 'success'"
            disable-transitions
          >{{scope.row.tag}}</el-tag>
        </template>
      </el-table-column>


    </el-table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tableData: [
        {
          date: "2016-05-02",
          name: "王小虎",
          address: "上海市普陀区金沙江路 1518 弄",
          tag: "家",
        },
        {
          date: "2016-05-04",
          name: "王小虎",
          address: "上海市普陀区金沙江路 1517 弄",
          tag: "公司",
        },
        {
          date: "2016-05-01",
          name: "王小虎",
          address: "上海市普陀区金沙江路 1519 弄",
          tag: "家",
        },
        {
          date: "2016-05-03",
          name: "王小虎",
          address: "上海市普陀区金沙江路 1516 弄",
          tag: "公司",
        },
      ],
    };
  },
  methods: {

    resetDateFilter() {
      this.$refs.filterTable.clearFilter("date");
    },

    clearFilter() {
      this.$refs.filterTable.clearFilter();
    },
    formatter(row, column) {
      return row.address;
    },

    filterTag(value, row) {
      return row.tag === value;
    },

    filterHandler(value, row, column) {
      const property = column["property"];
      return row[property] === value;
    },
    
  },
};
</script>
```

### 15  自定义列模板  显示组件搭配

自定义列的显示内容，可组合其他组件使用。

通过 `Scoped slot` 可以获取到 row, column, $index 和 store（table 内部的状态管理）的数据，用法参考 demo。



第一种  拦截数据, 加图标

```

    <el-table-column
      label="日期"
      width="180">

      <template slot-scope="scope">
        <i class="el-icon-time"></i>
        <span style="margin-left: 10px">{{ scope.row.date }}</span>
      </template>
      
    </el-table-column>
```

第二种 ; 拦截  使用组件  hober悬浮显示



```
    <el-table-column
      label="姓名"
      width="180">

      <template slot-scope="scope">

        <el-popover trigger="hover" placement="top">
          <p>姓名: {{ scope.row.name }}</p>
          <p>住址: {{ scope.row.address }}</p>

          <div slot="reference" class="name-wrapper">
            <el-tag size="medium">{{ scope.row.name }}</el-tag>
          </div>
          
        </el-popover>

      </template>

    </el-table-column>
```

第三种： 操作栏 事件获取行数据

```
    <el-table-column label="操作">

      <template slot-scope="scope">
        <el-button
          size="mini"
          @click="handleEdit(scope.$index, scope.row)">编辑</el-button>
        <el-button
          size="mini"
          type="danger"
          @click="handleDelete(scope.$index, scope.row)">删除</el-button>
      </template>

    </el-table-column>
```



### 16 展开行

当行内容过多并且不想显示横向滚动条时，可以使用 Table 展开行功能。

过设置 type="expand" 和 `Scoped slot` 可以开启展开行功能，`el-table-column` 的模板会被渲染成为展开行的内容，展开行可访问的属性与使用自定义列模板时的 `Scoped slot` 相同

总结： 方法是添加一行。 行类型设置 type="expand"， 里面嵌套一个slot模板，将行数据写入。

```
    <el-table-column type="expand">
      <template slot-scope="props">

        <el-form label-position="left" inline class="demo-table-expand">
         
          <el-form-item label="店铺地址">
            <span>{{ props.row.address }}</span>
          </el-form-item>
          <el-form-item label="商品描述">
            <span>{{ props.row.desc }}</span>
          </el-form-item>
        </el-form>

      </template>
    </el-table-column>
```

### 17 树形数据与懒加载

![1597548837166](C:\Users\luyunxiao\AppData\Roaming\Typora\typora-user-images\1597548837166.png)

支持树类型的数据的显示。当 row 中包含 `children` 字段时，被视为树形数据。渲染树形数据时，必须要指定 `row-key`。支持子节点数据异步加载。设置 Table 的 `lazy` 属性为 true 与加载函数 `load` 。通过指定 row 中的 `hasChildren` 字段来指定哪些行是包含子节点。`children` 与 `hasChildren` 都可以通过 `tree-props` 配置。

总结： 树形结构的判断首先是数据结构，如下  

数据中出现children字段，判断为该行是树形，

```
{
          id: 3,
          date: '2016-05-01',
          name: '王二吗',
          address: '上海市普陀区金沙江路 1519 弄',
          children: [{
              id: 31,
              date: '2016-05-01',
              name: '王二',
              address: '上海市普陀区金沙江路 1519 弄'
            }, {
              id: 32,
              date: '2016-05-01',
              name: '王二',
              address: '上海市普陀区金沙江路 1519 弄'
          }]
        }
```

tabel标签中设置  数据参数，和是否默认打开。 

```
default-expand-all
    :tree-props="{children: 'children_', hasChildren: 'hasChildren'}">
    
```

children: 'children_  设置数据。  

### 18 自定义表头

通过设置 [Scoped slot](https://cn.vuejs.org/v2/guide/components-slots.html#作用域插槽) 来自定义表头。



总结： 上边的搜索框和下边的按钮可以分别设置。

方式就是table 上加上过滤条件。 

search 是data中的值。  search: ""  。 空就是false.

每一条数据都经过输入框内容的过滤。然后渲染。

```
 <el-table
    :data="tableData.filter(data =>  !search || data.name.toLowerCase().includes(search.toLowerCase()  )  )"
    style="width: 100%">
```





![1597550469688](C:\Users\luyunxiao\AppData\Roaming\Typora\typora-user-images\1597550469688.png)

上边的搜索框和下面的按钮，是透过添加一行。

slot-scope="scope"  自定义出来的。

```
 <el-table-column
      align="left">

      <template slot="header" slot-scope="scope">

        <el-input
          v-model="search"
          size="mini"
          placeholder="输入关键字搜索"/>

      </template>

      <template slot-scope="scope">
        <el-button
          size="mini"
          @click="handleEdit(scope.$index, scope.row)">Edit</el-button>
        <el-button
          size="mini"
          type="danger"
          @click="handleDelete(scope.$index, scope.row)">Delete</el-button>
      </template>
      
    </el-table-column>
```

完整代码：

```
<template>
<div>

  <el-table
    :data="tableData.filter(data =>  data.name.toLowerCase().includes(search.toLowerCase()  )  )"
    style="width: 100%">

    <el-table-column
      label="Date"
      prop="date">
    </el-table-column>

    <el-table-column
      label="Name"
      prop="name">
    </el-table-column>

    <el-table-column
      align="left">

      <template slot="header" slot-scope="scope">

        <el-input
          v-model="search"
          size="mini"
          placeholder="输入关键字搜索"/>

      </template>

      <template slot-scope="scope">
        <el-button
          size="mini"
          @click="handleEdit(scope.$index, scope.row)">Edit</el-button>
        <el-button
          size="mini"
          type="danger"
          @click="handleDelete(scope.$index, scope.row)">Delete</el-button>
      </template>
      
    </el-table-column>

  </el-table>

</div>
</template>
<script>
  export default {
    data() {
      return {
        tableData: [{
          date: '2016-05-02',
          name: '王二',
          address: '上海市普陀区金沙江路 1518 弄'
        }, {
          date: '2016-05-04',
          name: '王小',
          address: '上海市普陀区金沙江路 1517 弄'
        }, {
          date: '2016-05-01',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1519 弄'
        }, {
          date: '2016-05-03',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1516 弄'
        }],
        search: ""
      }
    },
    methods: {

      handleEdit(index, row) {
        console.log(index, row);
      },

      handleDelete(index, row) {
        console.log(index, row);
      }

    },
  }
</script>
```



### 19  表尾合计行

总结： 两种方法，一个自动，一个自定义。

第一个：将`show-summary`设置为`true`就会在表格尾部展示合计行默认情况下，对于合计行，第一列不进行数据求合操作，而是显示「合计」二字（可通过`sum-text`配置），其余列会将本列所有数值进行求合操作，并显示出来。

```
<el-table
    :data="tableData"
    border
                     show-summary
                     sum-text='表名字'
    style="width: 100%">
```

第二种：

你也可以定义自己的合计逻辑。使用`summary-method`并传入一个方法，返回一个数组，这个数组中的各项就会显示在合计行的各列中，具体可以参考本例中的第二个表格。

table 标签中   :summary-method="getSummaries"   格式化函数。

函数中返回一个处理后的数组。

![1597552635618](C:\Users\luyunxiao\AppData\Roaming\Typora\typora-user-images\1597552635618.png)



计算方法参照官方案例。





![1597552238445](C:\Users\luyunxiao\AppData\Roaming\Typora\typora-user-images\1597552238445.png)



### 20 合并行或列

使用情景 :  多行或多列共用一个数据时，可以合并行或列

通过给`table`传入`span-method`方法可以实现合并行或列，方法的参数是一个对象，里面包含当前行`row`、当前列`column`、当前行号`rowIndex`、当前列号`columnIndex`四个属性。该函数可以返回一个包含两个元素的数组，第一个元素代表`rowspan`，第二个元素代表`colspan`。 也可以返回一个键名为`rowspan`和`colspan`的对象。

总结： 

tabel中绑定一个方法： 方法中回调。

```
:span-method="arraySpanMethod"
```

方法：

```
   methods: {
      arraySpanMethod({ row, column, rowIndex, columnIndex }) {
        if (rowIndex % 2 === 0) {
          if (columnIndex === 0) {
            return [1, 2];   //  意思就是 第一行，跨两列。进行合并。
          } else if (columnIndex === 1) {
            return [0, 0];
          }
        }
      },
```





### 21 自定义索引

通过给 `type=index` 的列传入 `index` 属性，可以自定义索引。该属性传入数字时，将作为索引的起始值。也可以传入一个方法，它提供当前行的行号（从 `0` 开始）作为参数，返回值将作为索引展示。

总结： tabel中绑定一个属性。:index="indexMethod"

方法中 定义一个自定义的逻辑。

methods: {
indexMethod(index) {
return index * 2;
}

### 22  tips   行内容多时，tips显示



![1598542342597](C:\Users\luyunxiao\AppData\Roaming\Typora\typora-user-images\1598542342597.png)



总结： element ui 有tips的组件。这个和其功能差不多。

### 23 tabel中的加载过渡效果

```
  <el-table
                         v-loading="loading"  绑定一个变量
          :data="tabellistdata"
          :stripe="true"
          :row-style="{height:'40px'}"
        >
```



````javascript
   data:{
       
      tableMaxHeight: "496", // 表格流体高度
      loading: false, //表格加载动画 
          
   }

````

使用

```
数据请求中， 
this.loading = true;   进入时   确定打开过渡

 this.loading = false;  数据返回时    关闭过渡


if (code === 200) {
            this.loading = false;
            this.tableData = res.data.resultData.dataList;
            this.total = res.data.resultData.total;
          }
```







## 2 Pagination 分页

分页标签

分页标签属性控制显示按钮，几个事件，上一页 点击时，下一页点击时。  可以用于调用接口，更换数据。达到渲染的目的。

```
<el-pagination
  small
  layout="prev, pager, next"
  :total="50">
</el-pagination>
```

## 3 Badge  标记 消息条数显示

基础用法

![1597554956875](C:\Users\luyunxiao\AppData\Roaming\Typora\typora-user-images\1597554956875.png)

:value="n"  写多少就是几条消息

```
<el-badge :value="12" class="item">
  <el-button size="small">评论</el-button>
</el-badge>
```

可自定义最大值

![1597555078153](C:\Users\luyunxiao\AppData\Roaming\Typora\typora-user-images\1597555078153.png)

value="new"  冒号去掉就是绑定文字。



## 4 Avatar 头像

用图标、图片或者字符的形式展示用户或事物信息。

形象标签

```
 <el-avatar icon="el-icon-user-solid"></el-avatar>
```

通过 `shape` 和 `size` 设置头像的形状和大小。

```
<el-avatar shape="square" :size="size" :src="squareUrl"></el-avatar>
```

### 展示类型

支持三种类型：图标、图片和字符

标签找中放 图片，文字和表情。

```
 <el-avatar icon="el-icon-user-solid"></el-avatar>

<el-avatar src="https://cube.elemecdn.com/0/88/03b0d39583f48206768a7534e55bcpng.png"></el-avatar>


  <el-avatar> user </el-avatar>

```

### 5. Tree属性控件

### 基础用法

```
<el-tree :data="data" :props="defaultProps" @node-click="handleNodeClick"></el-tree>


1. 树形标签
数据data 
format数据规则
node-clic  点击方法   参数是点击节点数据

2. 节点默认打开  和关闭
 node-key="id"
  :default-expanded-keys="[2, 3]"
  :default-checked-keys="[5]"
每组数据中都有一个id属性
 {
id: 9,
 label: "三级 1-1-1",
  },
3.  禁止点击
show-checkbox  属性
data数据中加上禁用属性。  
 disabled: true,
 效果是： checkbox禁止选中，但是节点打开和关闭不受影响。

4. 默认打开全部
 default-expand-all 属性
 5. checkbox 获取选中的数据
     <div class="buttons">
      <el-button @click="getCheckedNodes">通过 node 获取</el-button>
      <el-button @click="getCheckedKeys">通过 key 获取</el-button>
      <el-button @click="setCheckedNodes">通过 node 设置</el-button>
      <el-button @click="setCheckedKeys">通过 key 设置</el-button>
      <el-button @click="resetChecked">清空</el-button>
    </div>
    第一种：获取节点详情信息   获取原始全部数据
    第二种： id数组    弊端： 当子节点全部选中时，父节以上点默认选中。
    
 可以通过两种方法：设置默认点选
 6. 手风琴点击  扩展点击范围
 :expand-on-click-node="false"
 7. 
 :render-content="renderContent"
 树节点的内容区的渲染 Function	Function(h, { node, data, store }
8.
可以通过两种方法进行树节点内容的自定义：render-content和 scoped slot。



```



















# 第四部分：Notice提醒

# 

##  1  Alert 警告

页面中的非浮层元素，不会自动消失。

![1597074945072](C:\Users\luyunxiao\AppData\Roaming\Typora\typora-user-images\1597074945072.png)

```
Alert 组件提供四种主题，由type属性指定，默认值为info。

  <el-alert
    title="成功提示的文案"
    type="success">
  </el-alert>

```

放到页面中就显示。

页面加载，就会显示。点击可以关闭。  适用场景： 页面加载的提醒。





##  2  Loading 加载

分为三种： table     指令   和服务

### 局部加载效果

Element 提供了两种调用 Loading 的方法：指令和服务。对于自定义指令`v-loading`，只需要绑定`Boolean`即可。

场景1 ： el-table 中的。 充当一个配置项    loading绑定一个data  布尔值。路网项目中使用。

看下面， 直接卸载table中， 布尔值控制。

```
<el-table
               v-loading="loading"
    element-loading-text="拼命加载中"
    element-loading-spinner="el-icon-loading"
    element-loading-background="rgba(0, 0, 0, 0.8)"
    :data="tableData"
    style="width: 100%">
```



```
<el-table
    v-loading="loading"
    element-loading-text="拼命加载中"
    element-loading-spinner="el-icon-loading"
    element-loading-background="rgba(0, 0, 0, 0.8)"
    :data="tableData"
    style="width: 100%">
```



### 整页加载

#### 指令方式

总结： 

在按钮中v-loading.fullscreen.lock="是或者是否"  加入属性。并用一个方法控制   布尔值的 是与否



当使用指令方式时，全屏遮罩需要添加`fullscreen`修饰符（遮罩会插入至 body 上），此时若需要锁定屏幕的滚动，可以使用`lock`修饰符；当使用服务方式时，遮罩默认即为全屏，无需额外设置。

dom部分	

```
<el-button
    type="primary"
    @click="openFullScreen1"
    v-loading.fullscreen.lock="fullscreenLoading"
    >
    指令方式
  </el-button>
  
  
  data部分控制显示
    fullscreenLoading: false
    一个方法
    
     openFullScreen1() {
        this.fullscreenLoading = true;
        setTimeout(() => {
          this.fullscreenLoading = false;
        }, 2000);
      },
```

触发方式： 需要一个点击事件。例如按钮来触发

#### 服务方式

比较简单一点： 是需要一个事件。

```
  <el-button
    type="primary"
    @click="openFullScreen2">
    服务方式
  </el-button>
```

每次使用，声明一个loadding   .   loading.close();方法是关闭。

```
 openFullScreen2() {
        const loading = this.$loading({
          lock: true,
          text: 'Loading',
          spinner: 'el-icon-loading',
          background: 'rgba(0, 0, 0, 0.7)'
        });
        setTimeout(() => {
          loading.close();
        }, 2000);
      }
```



  项目使用：

```
 //  导出 exportExcel 模板
    downExcelTemplate() {
      const loading = this.$loading({
        lock: true,
        text: "导出中",
        spinner: "el-icon-loading",
        background: "rgba(0, 0, 0, 0.7)",
      });
      this.$axios({
        url: this.$path + "/api-auth/uasUser/exportUasUserTemplate",
        method: "get",
        timeout: 180000,
        responseType: "blob",
      })
        .then((res) => {
          // 定义文件名等相关信息
          loading.close();
          const blob = res.data;
          if ("download" in document.createElement("a")) {
            const reader = new FileReader();
            reader.readAsDataURL(blob);
            reader.onload = (e) => {
              const a = document.createElement("a");
              var date = moment().format("YYYY-MM-DD hh:mm:ss");
              a.download = `用户信息模板${date}.xlsx`;
              document.body.appendChild(a);
              a.href = URL.createObjectURL(blob);
              a.click();
              URL.revokeObjectURL(blob);
              document.body.removeChild(a);
            };
          } else {
            navigator.msSaveBlob(blob, `用户信息模板${date}.xlsx`);
          }
        })
        .catch(() => {
          loading.close();
        });
    }, 
```







#### 

## 3 Message 消息提示this.$message

总结：  访问错误，直接调用方法。 this.$message('参数错误，请重新输入');

参数type控制显示警告还是成功的样式。

```
this.$message({
          message: '恭喜你，这是一条成功消息',
          type: 'success'
        });
        
   this.$message({
          message: '警告哦，这是一条警告消息',
          type: 'warning'
        });
```

### 可关闭

弹窗可以手动关闭。



常用于主动操作后的反馈提示。与 Notification 的区别是后者更多用于系统级通知的被动提醒。

Element 注册了一个`$message`方法用于调用，Message 可以接收一个字符串或一个 VNode 作为参数，它会被显示为正文内容。

```
methods: {
      open() {
        this.$message('这是一条消息提示');
      },
      
      
      mounted(){
      this.openVn()
    }  
```

就一个方法， 可以直接mounted中调用。 使用方便。 使用场景： 在提交成功时的提醒。 3s后自动消失。也可以主动关闭。

## 4  MessageBox 弹框 this.$alert

使用： 也是直接调用方法，传入参数。

定位：弹出简单的内容

这里表明： 有三个方法。

alert         只有确定

 confirm     确定和取消

  prompt      prompt() 方法用于显示可提示用户进行输入的对话框。  弹出一个输入框。



从场景上说，MessageBox 的作用是美化系统自带的 `alert`、`confirm` 和 `prompt`





模拟系统的消息提示框而实现的一套模态对话框组件，用于消息提示、确认消息和提交内容。

从场景上说，MessageBox 的作用是美化系统自带的 `alert`、`confirm` 和 `prompt`，因此适合展示较为简单的内容。如果需要弹出较为复杂的内容，请使用 Dialog。

### 消息提示

调用`$alert`方法即可打开消息提示，它模拟了系统的 `alert`，无法通过按下 ESC 或点击框外关闭。此例中接收了两个参数，`message`和`title`。

![1597079854335](C:\Users\luyunxiao\AppData\Roaming\Typora\typora-user-images\1597079854335.png)

弹出位置是屏幕中间。 使用方法是this.$alert(） 直接调用方法。 和message使用 方法是一样的。



```
 this.$alert('这是一段内容', '标题名称', {
          confirmButtonText: '确定',
          callback: action => {
                         console.log(action);// 在这里判断点击了是还是否
            this.$message({
              type: 'info',
              message: `action: ${ action }`
            });
          }
        });
```



### 点击确认消息  

提示用户确认其已经触发的动作，并询问是否进行此操作时会用到此对话框。

总结： 也是一个方法，类似propose then和catch,分两种情况。

## 5  Notification 通知

右侧闯入提醒。

悬浮出现在页面角落，显示全局的通知提醒消息。

## 项目使用：

###  简单弹窗  this.$prompt

使用方式：完全是调用方法，特点，不占用dom.  直接犯法调用



1. 使用： @click="open"

```
 2.    methods: {
      open() {
        this.$prompt('请输入邮箱', '提示', {
          title: '审核',  //弹窗标题
            // message:'我是现实内容',
          confirmButtonText: '确定',   //确定按钮
          cancelButtonText: '取消',  //取消按钮
        message:`<div class='name'></div>`,
        dangerouslyUseHTMLString:true,

        }).then(({ value }) => {
          this.$message({
            type: 'success',
            message: '你输入的是: ' + value
          });
        }).catch(() => {
        this.$message.warning("取消操作");
        });
      }
    }
```

配置项说明： 

### 01

      01. message  使用html 解析。
       message:`<div class='name'></div>`,
        dangerouslyUseHTMLString:true,
功能是，message可以使用html。

### 02

使用场景： 只需要判断是 ，或否的场景。 根据点击了  取消还是确定，进行下一步操作。

showInput: false, //是否显示输入框	

![1600967576981](C:\Users\luyunxiao\AppData\Roaming\Typora\typora-user-images\1600967576981.png)

```
 open() {
      this.$prompt("请输入邮箱", "提示", {
        title: "审核", //弹窗标题
        message: "我是自己填写的内容",
        confirmButtonText: "确定", //确定按钮
        cancelButtonText: "取消", //取消按钮
        showInput: false, //是否显示输入框	

        callback: (action) => {
      //  action  变量 
      //  在点击确定时是： confirm    取消是cancel
             if(action =='confirm'){
                alert('选择了confirm')
             }else{
                alert(action)
             }

        },
      });
    },
```

### 03  使用场景是 弹窗输入一个变量。input

![1600967627435](C:\Users\luyunxiao\AppData\Roaming\Typora\typora-user-images\1600967627435.png)



## 第五部分

## Dropdown 下拉菜单

dropdown 标签  

command 回调事件

```
    <el-dropdown @command="handleCommand">
      <span class="el-dropdown-link">
        下拉菜单
        <i class="el-icon-arrow-down el-icon--right"></i>
      </span>
      <el-dropdown-menu slot="dropdown">
        <el-dropdown-item command="a">黄金糕</el-dropdown-item>
        <el-dropdown-item command="b">狮子头</el-dropdown-item>
        <el-dropdown-item command="c">螺蛳粉</el-dropdown-item>
        <el-dropdown-item command="d" disabled>双皮奶</el-dropdown-item>
        <el-dropdown-item command="e" divided>蚵仔煎</el-dropdown-item>
      </el-dropdown-menu>
    </el-dropdown>
    
    
    <script>
export default {
  methods: {
    handleCommand(command) {
      console.log(command);
      this.$message("click on item " + command);
    },
  },
};
</script>
```









# 其他弹窗

注意点：   

dialog配置项的写法：

```
    <el-dialog 
    title="填报信息" 
    :visible.sync="eventOrderDialogVisible" 
    :before-close="cancelDialog"
    custom-class = detailDialog
    :center = true
    >
```

```
Attributes
参数	说明	类型	可选值	默认值
visible	是否显示 Dialog，支持 .sync 修饰符	boolean	—	false
```

注意加  ： center。  否则报错

### 1  Dialog 对话框

在保留当前页面状态的情况下，告知用户并承载相关操作。

Dialog 弹出一个对话框，适合需要定制性更大的场景。

### 基本用法

需要设置`visible`属性，它接收`Boolean`，当为`true`时显示 Dialog。Dialog 分为两个部分：`body`和`footer`，`footer`需要具名为`footer`的`slot`。`title`属性用于定义标题，它是可选的，默认值为空。最后，本例还展示了`before-close`的用法。

![1597081198974](C:\Users\luyunxiao\AppData\Roaming\Typora\typora-user-images\1597081198974.png)

弹框层，由一个布尔值控制。 body  foot两部分。 

body可以构建自己的dom。 可以是form 表单， 可以是表格。

 foot两个按钮。

````javascript
<el-button type="text" @click="dialogVisible = true">点击打开 Dialog</el-button>

<el-dialog
  custom-class
  title="提示"     左上角弹窗名字
  :visible.sync="dialogVisible"   显示控制
  width="30%"    弹窗宽度
  :before-close="handleClose"   关闭前的回调
>   
      
  <span>这是一段信息</span>

  <span slot="footer" class="dialog-footer">
    <el-button @click="dialogVisible = false">取 消</el-button>
    <el-button type="primary" @click="dialogVisible = false">确 定</el-button>
  </span>

</el-dialog>

<script>
  export default {
    data() {
      return {
        dialogVisible: false
      };
    },
    methods: {
      handleClose(done) {
        this.$confirm('确认关闭？')
          .then(_ => {
            done();
          })
          .catch(_ => {});
      }
    }
  };
</script>
````

## 项目使用：

弹窗框的标题，变量替换

 :title="加变量  "

```
 <el-dialog
                              :title="this.currentName"
      :visible.sync="editDetailDialogVisible"
      width="85%"
      :before-close="editDetailClose"
      custom-class="sgkbIdeit"
    >
```



### Events

| 事件名称 | 说明                        | 回调参数 |
| :------- | :-------------------------- | :------- |
| open     | Dialog 打开的回调           | —        |
| opened   | Dialog 打开动画结束时的回调 | —        |
| close    | Dialog 关闭的回调           | —        |
| closed   | Dialog 关闭动画结束时的回调 |          |

```
 <el-dialog
      title="损失"
      :visible.sync="lossDialogVisible"
      :before-close="cancelDialog"
                              @open="openDialog"   弹窗打开时的回调
      custom-class="detailDialog"
      :center="true"   //弹窗框按钮居中
    >
```



### Dialog  两层对话框

如果需要在一个 Dialog 内部嵌套另一个 Dialog，需要使用 `append-to-body` 属性。

正常情况下，我们不建议使用嵌套的 Dialog，如果需要在页面上同时显示多个 Dialog，可以将它们平级放置。对于确实需要嵌套 Dialog 的场景，我们提供了`append-to-body`属性。将内层 Dialog 的该属性设置为 true，它就会插入至 body 元素上，从而保证内外层 Dialog 和遮罩层级关系的正确。

![1597591986023](C:\Users\luyunxiao\AppData\Roaming\Typora\typora-user-images\1597591986023.png)



```
    <el-dialog title="外层 Dialog" :visible.sync="outerVisible">

      <el-dialog width="30%" title="内层 Dialog" :visible.sync="innerVisible" append-to-body>
        <h1>我是二级内容</h1>
      </el-dialog>
     
        <h1>我是一级内容</h1>
      <div slot="footer" class="dialog-footer">
        <el-button @click="outerVisible = false">取 消</el-button>
        <el-button type="primary" @click="innerVisible = true">打开内层 Dialog</el-button>
      </div>

    </el-dialog>
```

总结： 

二级弹窗，就是在原本放一级内容的 区域，有放入要给dialog标签，配置 append-to-body属性。

两个布尔值控制。一个内，一个外。

二级弹窗配置项，和一级一样使用。

```
<el-dialog width="30%" title="内层 Dialog" :visible.sync="innerVisible" append-to-body>
        <h1>我是二级内容</h1>
</el-dialog>
```



### 2  Tooltip文字提示

作用： 悬浮就显示

使用方法： tooltip 标签包裹即可。content动态绑定提示内容。

![1597081822059](C:\Users\luyunxiao\AppData\Roaming\Typora\typora-user-images\1597081822059.png)

### 基础用法

在这里我们提供 9 种不同方向的展示方式，可以通过以下完整示例来理解，选择你要的效果。

```
 <el-tooltip class="item" effect="dark" content="提示文字" placement="bottom-end">
      <el-button>下右</el-button> 
    </el-tooltip>
```

总结： content控制显示内容。placement控制显示方向。

## 3 Popover 弹出框

### 基础用法

Popover 的属性与 Tooltip 很类似，它们都是基于`Vue-popper`开发的，因此对于重复属性，请参考 Tooltip 的文档，在此文档中不做详尽解释。

````javascript
 <el-popover
  placement="right"
  width="600"
  trigger="click">
  <el-table :data="gridData">
    <el-table-column width="150" property="date" label="日期"></el-table-column>
    <el-table-column width="100" property="name" label="姓名"></el-table-column>
    <el-table-column width="300" property="address" label="地址"></el-table-column>
  </el-table>
  <el-button slot="reference">click 激活</el-button>
</el-popover>
````

总结： 弹窗框，嵌套table。 table渲染的数据灌入使用。 property指定数据键值对。

![1597082580341](C:\Users\luyunxiao\AppData\Roaming\Typora\typora-user-images\1597082580341.png)

### Popover 弹出框 总结： 

只适合用于展示一个界面， 切面上可以是一些按钮。   路网检测中的菜单等。

不需要js。 只需要dom，就可以实现点击或hover弹窗。

```
 <el-popover
    placement="top-start"
    title="标题"
    width="200"
    trigger="hover"
    content="这是一段内容,这是一段内容,这是一段内容,这是一段内容。">
    <el-button slot="reference">hover 激活</el-button>
  </el-popover>
```

`trigger`属性用于设置何时触发 Popover，支持四种触发方式：`hover`，`click`，`focus` 和 `manual`







## 4 Popconfirm 气泡确认框



```
<el-popconfirm
  title="这是一段内容确定删除吗？"
 @onConfirm = 'fn'  //  回调
>
  <el-button slot="reference">删除</el-button>
</el-popconfirm>

```

Events

| 事件名称  | 说明               | 回调参数 |
| :-------- | :----------------- | :------- |
| onConfirm | 点击确认按钮时触发 | —        |
| onCancel  | 点击取消按钮时触发 | —        |



### Divider 分割线

<el-divider></el-divider>





# 第六部分 Others

### 1 [¶](https://element.faas.ele.me/#/zh-CN/component/timeline#timeline-shi-jian-xian)Timeline 时间线

基础用法

使用el-timeline时间线标签     和组标签 el-timeline-item 。

属性：可以自定义图标，颜色，时间戳，标题。 上线显示位置。

​       时间线 排序属性。

```
   <el-timeline>
        <el-timeline-item
          v-for="(activity, index) in activities"
          :key="index"
          :icon="activity.icon"
          :type="activity.type"
          :color="activity.color"
          :size="activity.size"
          :timestamp="activity.timestamp">

        {{activity.content}}
        
        </el-timeline-item>
      </el-timeline>
      
      
   
      
<script>
export default {
  data() {
    return {
      activities: [
        {
          content: "支持使用图标",
          timestamp: "2018-04-12 20:46",
          size: "large",
          type: "danger",
          icon: "el-icon-more",
        },
        {
          content: "支持自定义颜色",
          timestamp: "2018-04-03 20:46",
          color: "#0bbd87",
        },
        {
          content: "支持自定义尺寸",
          timestamp: "2018-04-03 20:46",
          size: "large",
        },
        {
          content: "默认样式的节点",
          timestamp: "2018-04-03 20:46",
        },
      ],
    };
  },
};
</script>
```



## Navigation  导航菜单

#### 基础用法：

```
 <el-menu
      :default-active="activeIndex"// 默认显示的bar
      class="el-menu-demo"   // 自定义class
      mode="horizontal"    // 排列方式
      @select="handleSelect"// 点击的回调
    >
      <el-menu-item index="1">处理中心</el-menu-item>
      <el-submenu index="2">
        <template slot="title">我的工作台</template>
        <el-menu-item index="2-1">选项1</el-menu-item>
        <el-menu-item index="2-2">选项2</el-menu-item>
        <el-menu-item index="2-3">选项3</el-menu-item>
      </el-submenu>
      <el-menu-item index="3" disabled>消息中心</el-menu-item>
      <el-menu-item index="4">
        <a href="https://www.ele.me" target="_blank">订单管理</a>
      </el-menu-item>

    </el-menu>
--------方法--------------
    
methods: {
    handleSelect(key, keyPath) {
      console.log(key, keyPath);
    },
  },
    
```

#### 父标签：el-menu 标签包裹

```
    :default-active="activeIndex"// 默认显示的bar
      class="el-menu-demo"   // 自定义class
      mode="horizontal"    // 排列方式
      @select="handleSelect"// 点击的回调
```

#### 子项： el-menu-item  

```
<el-menu-item index="1">处理中心</el-menu-item>
  子项：index="1"   是选中时的value值。 中间的是显示的内容。 相当于label

子项有几种表现形式：
01. 链接形式
    <el-menu-item index="4">
        <a href="https://www.ele.me" target="_blank">订单管理</a>
      </el-menu-item>
02 禁用
 <el-menu-item index="3" disabled>消息中心</el-menu-item>
 03   多级
    <el-submenu index="2">
        <template slot="title">我的工作台</template>
        <el-menu-item index="2-1">选项1</el-menu-item>
        <el-menu-item index="2-2">选项2</el-menu-item>
        <el-menu-item index="2-3">选项3</el-menu-item>
      </el-submenu>
      
      
      
      
```

### 项目使用：

router ： 是否使用 vue-router 的模式，启用该模式会

```
  <el-menu
            router
            :default-active="$route.path"
            class="el-menu-demo"
            mode="horizontal"
            text-color="#000"
            active-text-color="#255ada"
            menu-trigger="click"
          >
            <el-menu-item index="/earlyWarningManagement/response">预警响应管理</el-menu-item>
            <el-menu-item index="/earlyWarningManagement/emergency">突发事件管理</el-menu-item>
            <el-submenu index="/earlyWarningManagement/disposal" popper-class="submenu">
              <template slot="title">处置管理</template>
              <el-menu-item index="/earlyWarningManagement/emergencyManagement">应急处置管理</el-menu-item>
              <el-menu-item index="/earlyWarningManagement/emergencyHandle">突发事件处置</el-menu-item>
              <el-menu-item index="/earlyWarningManagement/activityInstructionHandle">活动指令事件处置</el-menu-item>
            </el-submenu>
            <el-menu-item index="/earlyWarningManagement/materialAllocation">物资调拨</el-menu-item>
          </el-menu>
```



#### index 使用router形式

项目使用：

   router 是否使用 vue-router 的模式，启用该模式会在激活导航时以 index 作为 path 进行路由跳转

插件配置  ，关注两点： 01. router  属性  02    item 中 的index="/helloWorld/layout"  ，写路由。 易错点：

点击bar时， 路由叠加，导致无法显示。原因是    /helloWorld/layou      / 横杠别忘了加。

```
    <el-menu
      router  // 属性
      class="el-menu-demo"
      mode="horizontal"
      @select="handleSelect"
    >
      <el-menu-item index="/helloWorld/layout">处理中心</el-menu-item>
      <el-menu-item index="/helloWorld/border" >消息中心</el-menu-item>
    </el-menu>
    
    <router-view></router-view>
```

路由的配置：

```
{
      path: '/helloWorld',
      name: 'HelloWorld',
      component: Button,
      children:[
           { path: 'layout', component: Layout },
        
           { path: 'border', component: Border },
      ]
    }
```

基础知识： 父级组件中写入bar，切换的头部。   container 内容写在子级组件中。 当路由中同时/helloWorld/layout， 同时切换时，  页面会同时显示父 ，子级内容。  子级内容会显示在  <router-view></router-view>的位置，并替换掉view标签。

这里：可以使用element插件的上下布局。

<el-container>
<el-header>Header</el-header>
<el-main>Main</el-main>
</el-container>









