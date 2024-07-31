# vue3 ant design 实现表格行拖拽排序功能，使用customRow api封装方法

```
 <a-table
      :data-source="tableData"
      :columns="tableColumns"
      :customRow="customRow"
     
 />

```



```
<script setup>
import { ref } from 'vue';
import tableRowDragSort from '@/utils/tableRowDragSort.js';
// 表格数据
const tableData = ref([
	{name: 'xx'}
]) 
// 表格列配置
const tableColumns = ref([
	{ title: '名称',dataIndex: 'name'}
]) 
// 拖拽排序
const customRow = (record, index) => {
  return tableRowDragSort(record, index, tableData.value, updateTable);
};
// 拖拽后的回调方法，可在此处执行更新数据等操作
const updateTable = () => {}
</script>

```

tableRowDragSort.js 代码如下

```
import { ref } from 'vue';
// 拖拽排序
const sourceObj = ref({});
const targetObj = ref({});
let sourceIndex;
let targetIndex;
const tableRowDragSort = (record, index, tableList, callback) => {
  const style = {
    cursor: 'pointer'
  };
  // 鼠标移入
  const onMouseenter = event => {
    // 兼容IE
    const ev = event || window.event;
    ev.target.draggable = true;
  };
  // 开始拖拽
  const onDragstart = event => {
    const ev = event || window.event;
    ev.stopPropagation();
    // 得到源目标数据
    sourceObj.value = record;
    sourceIndex = index;
  };
  // 拖动元素经过的元素
  const onDragover = event => {
    const ev = event || window.event;
    ev.preventDefault();
    ev.dataTransfer.dropEffect = 'move';
    ev.dataTransfer.effectAllowed = 'move';
    targetIndex = index;
  };
  // 拖动到达目标元素
  const onDragenter = event => {
    const ev = event || window.event;
    ev.preventDefault();
    const list = document.getElementsByClassName('ant-table-row');
    const node = document.getElementsByClassName('target');
    if (node.length) {
      node[0].classList.remove('target');
    }
    list[index].classList.add('target');
  };
  // 鼠标松开
  const onDrop = event => {
    const ev = event || window.event;
    ev.stopPropagation();
    // 得到目标数据
    targetObj.value = record;
    targetIndex = index;
    const node = document.getElementsByClassName('target');
    if (node.length) {
      node[0].classList.remove('target');
    }
    if (targetIndex === sourceIndex) return;
    tableList.splice(sourceIndex, 1);
    tableList.splice(targetIndex, 0, sourceObj.value);
    callback();
  };
  return {
    style,
    onMouseenter,
    onDragstart,
    onDragover,
    onDrop,
    onDragenter
  };
};
export default tableRowDragSort;


```



[参考](https://blog.csdn.net/weixin_46447553/article/details/140469784?utm_medium=distribute.pc_relevant.none-task-blog-2~default~baidujs_baidulandingword~default-0-140469784-blog-137117434.235^v43^control&spm=1001.2101.3001.4242.1&utm_relevant_index=1)