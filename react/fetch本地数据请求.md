# 笔记



## fetch本地数据请求

安装和使用参考 ：https://blog.csdn.net/qq_64469057/article/details/129529788

```react
import React from 'react'
import { Card } from 'antd';

// 引入标准Fetch及IE兼容依赖
import 'whatwg-fetch'

export default class myCard extends React.Component {
    constructor(props) {
        super(props)
        this.state = {
            lists: []
        }
    }
    // 获取数据
    fetchFn = () => {
        fetch('../../data.json')
            .then((res) => { console.log(res.status);return res.json() })
            .then((data) => { this.setState({lists:data.listData}) })
            .catch((e) => { console.log(e.message) })
    }

    componentDidMount() {
        this.fetchFn()
    }


```

