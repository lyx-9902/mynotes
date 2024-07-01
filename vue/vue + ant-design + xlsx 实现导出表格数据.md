# vue + ant-design + xlsx 实现导出表格数据

#### 前言

本文将介绍如何用 xlsx 实现前端导出 table 表格数据。

#### 一、安装 xlsx

```
npm i xlsx --save-dev
```

#### 二、渲染 Table 表格

< 1 > 使用 ant-design-vue 写一个基本的表格

```
<template>
	<div class="container">
		<a-button
			type="primary"
			@click="exportData"
		>
			导出
		</a-button>
		<a-table
			:data-source="tableList"
			:columns="columns"
			row-key="id"
		/>
	</div>
</template>

<script>
import { Table, Button } from 'ant-design-vue';
import XLSX from 'xlsx';

const columns = [
	{ title: '姓名', dataIndex: 'name' },
	{ title: '性别', dataIndex: 'sex' },
	{ title: '年龄', dataIndex: 'age' },
	{ title: '邮箱', dataIndex: 'email' },
	{ title: '手机', dataIndex: 'phone' },
];

const tableList = [
	{
		id: 1,
		name: 'job',
		sex: '男',
		age: 18,
		email: '123@qq.com',
		phone: '15467543456'
	},
	{
		id: 2,
		name: 'nicy',
		sex: '女',
		age: 20,
		email: '456@qq.com',
		phone: '17734537689'
	}
];

export default {
	components: {
		[Table.name]: Table,
		[Button.name]: Button
	},
	data() {
		return {
			columns,
			tableList
		}
	}
}
</script>

```

< 2 > 效果如下：

![图片](https://img-blog.csdnimg.cn/2d0861a40ce546668b934fb7f32c9825.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBASGl6bw==,size_20,color_FFFFFF,t_70,g_se,x_16)

#### 三、导出为 Excel 表格

< 1 > 将数据转化为 xlsx 规定的格式

```js
transData(columns, tableList) {
	const obj = columns.reduce((acc, cur) => {
		if (!acc.titles && !acc.keys) {
			acc.titles = [];
			acc.keys = [];
		}
		acc.titles.push(cur.title);
		acc.keys.push(cur.dataIndex);
		return acc;
	}, {});
    const tableBody = tableList.map(item => {
    	return obj.keys.map(key => item[key]);
    });
	return [ obj.titles, ...tableBody ];
},

```

< 2 > 导出数据

```js
exportData() {
    const tableData = this.transData(
        this.columns,
        this.tableList
    );
    // 将一组 JS 数据数组转换为工作表
    const ws = XLSX.utils.aoa_to_sheet(tableData);
    // 创建 workbook
    const wb = XLSX.utils.book_new();
    // 将 工作表 添加到 workbook
    XLSX.utils.book_append_sheet(wb, ws, 'Sheet1');
    // 将 workbook 写入文件
    XLSX.writeFile(wb, 'table.xlsx');
}

```

< 3 > 最终导出的表格效果

![](https://img-blog.csdnimg.cn/0d5a73ab4bda426daec2ae9e3e4b8eb8.png)