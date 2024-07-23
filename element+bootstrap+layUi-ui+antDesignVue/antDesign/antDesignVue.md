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









