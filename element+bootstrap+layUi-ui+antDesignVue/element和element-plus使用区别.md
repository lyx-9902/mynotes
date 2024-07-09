# element和element-plus使用区别

## el-table

```cpp
  <template slot-scope="scope"></template>  // element
  <template #default="scope"></template>  // element-plus
```

## el-dialog

```xml
  <!-- element -->
  <span slot="footer" class="dialog-footer">  
      <el-button @click="_cancel">取 消</el-button>
      <el-button type="primary" @click="save">保 存</el-button>
  </span>

  <el-dialog :visible="dialogVisible"></el-dialog>

<!-- element-plus -->
  <template #footer>
      <span class="dialog-footer">
          <el-button @click="_cancel">取 消</el-button>
          <el-button type="primary" @click="save">确 定</el-button>
      </span>
  </template>

  <el-dialog v-model="dialogVisible"></el-dialog>
```

## el-button

```xml
<!-- element -->
   <el-button type="text" @click="rowAdd(scope)">新增</el-button>
<!-- element-plus -->
   <el-button type="primary" link @click="rowAdd(scope)">新增</el-button>
```

## el-date-picker

```xml
  <!-- element -->
  <el-date-picker 
  class="delay-times-picker dia-ipts" 
  v-model="ruleForm.releaseTime" 
  :picker-options="pickerBeginDateBefore" 
  default-time="00:00:00" 
  type="datetime" 
  value-format="yyyy-MM-dd HH:mm:ss" 
  placeholder="请选择发布时间">
  </el-date-picker>

  <!-- element-plus -->
  <el-date-picker 
  v-model="ruleForm.releaseTime" 
  :disabled-date="pickerBeginDateBefore" 
  :default-time="new Date(0,0,0,0,0,0)" 
  type="datetime" 
  value-format="YYYY-MM-DD HH:mm:ss" 
  placeholder="请选择发布时间">
  </el-date-picker>
```

## el-icon

```xml
<!-- element -->
<i class="el-icon-edit"></i>
<!-- element-plus -->
<el-icon><component is="el-icon-edit" /></el-icon>
```

## 去掉修饰符

### 如stop、async、trim、native

## css

```ruby
  /deep/  => ::v-deep
```

## echarts

### 错误图片

![](//upload-images.jianshu.io/upload_images/21836592-6886e6aaa7a1aba3.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200/format/webp)

```xml
//引入
<!-- v2 -->
import echarts from 'echarts'
this.chart = echarts.init(document.getElementById('echarts-wrap'));
<!-- v3 -->
import * as echarts from 'echarts';
let chart = echarts.init(document.getElementById('echarts-wrap'));

不用响应式变量来获取echarts元素： 因为前者切换legend时会报错
```







补充：

```
const options = Array.from({ length: 10000 }).map((_, idx) => ({
    value: `${idx + 1}`,
    label: `${idx + 1}`,
}))
```

# Array.from详解

### Array.from(obj,mapFn(可选))

obj指的是[数组对象](https://so.csdn.net/so/search?q=数组对象&spm=1001.2101.3001.7020)、类似数组对象或者是set对象，
mapFn指的是对数组中的元素进行处理的方法



>mapFn是调用数组每个元素的函数。如果提供，每个将要添加到数组中的值首先会传递给该函数，然后将 mapFn 的返回值增加到数组中

```
//将数组中布尔值为false的成员指为0
Array.from([1, ,2,3,3], x => x || 0) //[1,0,2,3,3]
 
//将一个类似数组的对象转为一个数组，并在原来的基础上乘以2倍
let arrayLike = { '0': '2', '1': '4', '2': '5', length: 3 }
Array.from(arrayLike, x => x*2) //[4,8,10]
 
//将一个set对象转为数组，并在原来的基础上乘以2倍
Array.from(new Set([1,2,3,4]), x => x*2) //[2,4,6,8]

```

### Array.from ({length:n}, Fn)

第一个参数指定了第二个参数执行的次数。可以将各种值转化为真正的数组。

```
Array.from({length:3}, () => 'jack') //["jack", "jack", "jack"]
 
Array.from({length:3}, item => (item = {'name':'shao','age':18})) 
//[{'name':'shao','age':18}, {'name':'shao','age':18}, {'name':'shao','age':18}]
 
Array.from({length: 2}, (v, i) => item = {index:i});
//生成一个index从0到4的数组对象[{index: 0},{index: 1}]

const options = Array.from({ length: 10000 }).map((_, idx) => ({
  value: `${idx + 1}`,
  label: `${idx + 1}`,
}))
//Array.from({ length: 10000 }) 是创建一个新的数组，其长度为10000，元素的默认值为undefined。
//.map((_, idx) => ({ value: idx+1‘,label:‘{idx + 1} })) 是一个映射操作，它遍历每个元素，并返回一个新的对象数组。
//每个对象都有两个属性：value和label，它们的值都是当前索引加一。
//所以，如果你运行这段代码，你会得到一个包含10000个对象的数组，每个对象都有value和label属性，它们的值都是从1到10000的整数。

```

### Array.from(string)

```
Array.from('abc') //['a','b','c']
```

