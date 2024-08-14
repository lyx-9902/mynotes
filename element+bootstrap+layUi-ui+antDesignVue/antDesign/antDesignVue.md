# antDesignVue

##  图标使用

**使用注意**： 版本号。本案例为4.x  不同版本可能有不用使用方式。

语义化的矢量图形。使用图标组件，你需要安装 `@ant-design/icons-vue` 图标组件包：

第一步：引入

```
npm install --save @ant-design/icons-vue
```

第二步：使用

```vue
<template>
  <a-space>
    <HomeOutlined />
    <SettingOutlined />
    <SmileOutlined />
  </a-space>
</template>
 
<script>
import { HomeOutlined, SettingOutlined, SmileOutlined } from '@ant-design/icons-vue';
 
export default {
  components: {
    HomeOutlined,
    SettingOutlined,
    SmileOutlined
  }
};
</script>
```

在上面的例子中，我们导入了三个图标组件`HomeOutlined`、`SettingOutlined`和`SmileOutlined`，并在模板中直接使用它们。`<a-space>`是Ant Design Vue中的空间组件，用于排列图标。

**注意**：图标名称遵循`IconNameOutlined`的格式，`Outlined`表示图标的样式。Ant Design Vue 4.x同时提供填充图标（`Filled`）、双色图标（`TwoTone`）和线框图标（`Outline`），你可以根据需要导入相应的图标组件。

案例2

```vue
<smileTwoTone />

//注意：大驼峰写法
import { SmileTwoTone } from '@ant-design/icons-vue';
```



## a-table 单选框 功能配置

版本 4.x.x

案例

关键点：

```
1. :row-selection="{ selectedRowKeys: state.selectedRowKeys, onChange: onSelectChange, type:'radio' } //单选属性
2. rowKey="id" 指定数据中 唯一键值 
3. tableData 中提供对应的id属性值

拿值：onChange 事件回调中拿到
```





```vue
<template>
    <div class="test">
        <a-table :columns="columns" :data-source="tableData" :style="{ width: '100%' }" rowKey="id" :scroll="{ y: 400 }"
            :pagination="false"
            :row-selection="{ selectedRowKeys: state.selectedRowKeys, onChange: onSelectChange, type: 'radio' }">
            <template #bodyCell="{ column, text, record, index }">
                <template v-if="column.dataIndex === '序号'">
                    {{ index + 1 }}
                </template>
            </template>
        </a-table>

    </div>
</template>
<script setup>

const columns = [
    {
        title: '序号',
        dataIndex: '序号',
        key: '序号',
        width: 60,
    },
    {
        title: '题目名称',
        dataIndex: 'name',
        key: 'name',
        ellipsis: true,
    },
    {
        title: '题型',
        dataIndex: 'type',
        key: 'type',
        ellipsis: true,
    },
];

const tableData = reactive([
    { id: 1, name: "夏令营", type: "单选题", options: [{ label: "满意", value: 10 }, { label: "不满意", value: 19 }] },
    { id: 2, name: "航空航天", type: "单选题", options: [{ label: "满意", value: 11 }, { label: "不满意", value: 1 }] },
    { id: 3, name: "物业环境", type: "单选题", options: [{ label: "满意", value: 14 }, { label: "不满意", value: 10 }] },
])

const state = reactive({
    selectedRowKeys: [],
    // Check here to configure the default column
    loading: false,
});

const onSelectChange = selectedRowKeys => {
    console.log('selectedRowKeys changed: ', selectedRowKeys);
    state.selectedRowKeys = selectedRowKeys;
};
</script>
```

## a-table 多选框 功能配置

关键点：

```
1.  :rowSelection="{ 
selectedRowKeys: tableSelectRowIds,  
type: 'checkbox' ,
onSelect:onSelect,
onSelectAll:onSelectAll
} //多选属性
2. rowKey="id" 指定数据中 唯一键值 (根据实际列表数据，如下表的deviceId)
3. tableData 中提供对应的id属性值

拿值：多选有单个操作和一键全选，onSelect  onSelectAll两个方法获取想要的数据。
```

示例：

```vue
<a-table 
         :columns="columns" 
         :data-source="tableData" 
         :style="{ width: '100%' }"                                 
         :pagination="queryParams"   
         rowKey="deviceId" 
         :scroll="{ y: tableMaxHeight }"  
         :rowSelection="{ selectedRowKeys: tableSelectRowIds,  type: 'checkbox'      ,onSelect:onSelect,onSelectAll:onSelectAll}">
        <template #bodyCell="{ column, text, record, index }">
```

js部分

```javascript
const tableSelectRowIds = ref([])
const tableSelectRows = ref([])
/**
   * @description  table的多选框回调事件- 单个点击事件
   * @param {array}  record 表示当前行obj
   * @param {Boolean} selected:true表示选中操作  false 表示取消操作
   */
   function onSelect(record, selected, selectedRows, nativeEvent) {
    console.log('onSelect', record.deviceId, selected, selectedRows, nativeEvent)
    if (selected) {  //选中操作 保存id row
        tableSelectRowIds.value.push(record.deviceId);
        tableSelectRows.value.push(record);
    } else {//取消操作 删除id row
        tableSelectRowIds.value = tableSelectRowIds.value.filter( i=> i !== record.deviceId);
        tableSelectRows.value = tableSelectRows.value.filter( i=> i.deviceId !== record.deviceId);
    }
}
/**selected, selectedRows, changeRows
   * @description  table的多选框回调事件- 全选的chagne事件  
   * @param {array}  changeRows 
   * @param {array}  selectedRows 
   * @param {Boolean} selected: true表示全选中操作  false 表示全取消操作
   */
function onSelectAll(selected, selectedRows, changeRows){
    //全选操作时 注意查重
    if (selected) {
            selectedRows.forEach(i => {
                if (!!i&&!tableSelectRowIds.value.includes(i.deviceId)) {//不包含的添加
                    tableSelectRowIds.value.push(i.deviceId);
                    tableSelectRows.value.push(i);
                }

            }) 
    } else {//取消操作  时changeRows中有数据
        changeRows.forEach( item =>{
            console.log(item);
            tableSelectRowIds.value = tableSelectRowIds.value.filter(i => i!== item.deviceId);
            tableSelectRows.value = tableSelectRows.value.filter(i => i.deviceId!== item.deviceId);

        })

    }
}
```



## 循环表单验证



案例

```vue
        <!-- 应用场景 -->
        <div class="advantage item">
          <p class="itemTitle"> <img src="/img/product/scene.png" alt=""> <span>应用场景</span></p>
          <!-- 循环区域   -->
          <div class="itemBody">
            <div class="loop">
              <div class="loop_item" v-for="(item, index) in formState.scenarioDetailList" :key="index">
                <div class="loop_head">
                  <span class="circle"><span>{{ index + 1 }}</span></span>
                  <span class="del" @click="addUseFormItem(index)" v-if="index !== 0">
                    <DeleteOutlined :style="{ fontSize: '16px', color: '#808BB5' }" /> 删除
                  </span>
                </div>
                <div class="loop_body">
                  <a-row>
                    <a-col :span="24">
                      <a-form-item label="概述" :name="['scenarioDetailList', index, 'scenarioOverview']"  《----关键点
                        :rules="rules.scenarioOverview">
                        <a-input v-model:value="item.scenarioOverview" placeholder="请输入概述" />
                      </a-form-item>
                    </a-col>
                    <a-col :span="24">
                      <a-form-item label="详情" :name="['scenarioDetailList', index, 'scenarioDetail']"
                        :rules="rules.scenarioDetail">
                        <a-textarea v-model:value="item.scenarioDetail" placeholder="请输入详情" :rows="4" />
                      </a-form-item>
                    </a-col>
                  </a-row>
                </div>
              </div>
              <div class="loop_addbutton">
                <span @click="addUseFormItem(null)">
                  <PlusOutlined />&nbsp; 添加表单
                </span>
              </div>

            </div>
          </div>
```

## a-table的单选  自动选中



```vue
   <a-table :columns="repairPersonColumns" :data-source="repairPersonList"
        :style="{ width: '100%', marginTop: '20px' }" :pagination="queryParams" @change="changeTable" rowKey="userId"
        :scroll="{ y: tableMaxHeight }"
        :rowSelection="{ 
                       selectedRowKeys: selectedRowKeysArray,   《----关键点
                       onChange: onSelectChange,
                       type: 'radio' 
                       }"
```

selectedRowKeysArray： 绑定的是单选或多选的id，更改这个数据，表格显示对应的选中效果。

onSelectChange 是点击单选或多选时，当前行id的集合。 赋值到selectedRowKeys属性上，即实现选中。

# Ant Design Vue的table组件高度自适应问题

[Ant](https://so.csdn.net/so/search?q=Ant&spm=1001.2101.3001.7020) Design Vue的table组件高度无法自适应，高度强制定死的话针对窗口缩放又不友好，最终尝试的解决方案只能通过监听浏览器窗口变化实现自适应

**1. 设定组件滚动区域的宽和高参数**

```
//此处减去的430是其他固定元素块的总高度
const tableHeight = ref({ x: '100%', y: document.body.clientHeight - 430 });

```

**2. 在生命周期onMounted里面监听浏览器窗口变化**

```
onMounted(() => {
    //监听浏览器窗口变化
    window.onresize = () => {
      return (() => {
        tableHeight.value.y = document.body.clientHeight - 430;
      })();
    };
  });

```

**3. 参数带入组件**

```
<a-table :scroll="tableHeight"> </a-table>

```

[参考](https://blog.csdn.net/zhouoxinxin/article/details/126180738?utm_medium=distribute.pc_relevant.none-task-blog-2~default~baidujs_baidulandingword~default-0-126180738-blog-138603175.235^v43^control&spm=1001.2101.3001.4242.1&utm_relevant_index=1)