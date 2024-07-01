# 常用配置笔记

## echart x轴倾斜

```js
option = {
    xAxis: {
        type: 'category',
        data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'],
        axisLabel: {
            rotate: 45 // 将标签倾斜45度
        }
    },
    yAxis: {
        type: 'value'
    },
    series: [{
        data: [820, 932, 901, 934, 1290, 1330, 1320],
        type: 'line'
    }]
};
```

# echart 改变Y轴的背景横线颜色

 就是平行于x轴的线的颜色。

```
yAxis:{
    splitLine: {
        lineStyle: {
        // 设置背景横线
        color: ‘rgba(106, 110, 126,0.5)’
        }
    },
}
```



# 表针



```
function detectionData(str) {
    var color = '#5eb95e';
    if (str >= 30 && str <= 60) {
        color = '#F37B1D';
    } else if (str > 60) {
        color = '#dd514c';
    }
    return color;
}
var option = {
    "series": [{
        "name": "业务指标",
        "type": "gauge",
        "splitNumber": 5,
        "axisLine": {
            "lineStyle": {
                "color": [
                    [0.31, "#F37B1D"],//进度条色
                    [1, "#787674"] //进度条背景色
                ],
                "width": 10
            }
        },
        "axisTick": {
              "show": false,
        },
        "axisLabel": {
              "show": false,
        },
        "splitLine": {
            "show": false
        },
        "itemStyle": {
            "normal": {
                "color": "#494f50"
            }
        },
        "detail": {
             "show": false,
        },
        "title": {
            "offsetCenter": [0, "100%"]
        },
        "data": [{
            "name": "",
            "value": 31
        }]
    }]
}
// app.timeTicket = setInterval(function() {
//     var value = (Math.random() * 100).toFixed(2) - 0;
//     option.series[0].data[0].value = value;
//     option.series[0].axisLine.lineStyle.color[0][0] = value / 100;
//     option.series[0].axisLine.lineStyle.color[0][1] = detectionData(value);
//     myChart.setOption(option, true);
// }, 500);
```







