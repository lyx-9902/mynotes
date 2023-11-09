# moment js插件

项目中经常使用的时间形式使用moment插件便捷使用；



moment 获取本年/本季度/本月/本周/今天/上年/上季度/上月/上周/昨天 开始结束时间

##### 今天

```
const startTime = moment(moment().startOf('day').valueOf()).format('YYYY/MM/DD HH:mm:ss');
const endTime = moment(moment().valueOf()).format('YYYY/MM/DD HH:mm:ss');
```

##### 昨天

```
const startTime = moment(moment().add(-1, 'days').startOf('day').valueOf()).format('YYYY/MM/DD HH:mm:ss');
const endTime = moment(moment().add(-1, 'days').endOf('day').valueOf()).format('YYYY/MM/DD HH:mm:ss');

```

##### 本周

```
const startTime = moment(moment().week(moment().week()).startOf('week').valueOf()).format('YYYY/MM/DD HH:mm:ss');
const endTime = moment(moment().week(moment().week()).endOf('week').valueOf()).format('YYYY/MM/DD HH:mm:ss');

```

##### 上周

```
const startTime = moment(moment().week(moment().week() - 1).startOf('week').valueOf()).format('YYYY/MM/DD HH:mm:ss');
const endTime = moment(moment().week(moment().week() - 1).endOf('week').valueOf()).format('YYYY/MM/DD HH:mm:ss');

```

##### 本月

```
const startTime = moment(moment().month(moment().month()).startOf('month').valueOf()).format('YYYY/MM/DD HH:mm:ss');
const endTime = moment(moment().month(moment().month()).endOf('month').valueOf()).format('YYYY/MM/DD HH:mm:ss');

```

##### 上月

```
const startTime = moment(moment().month(moment().month() - 1).startOf('month').valueOf()).format('YYYY/MM/DD HH:mm:ss');
const endTime = moment(moment().month(moment().month() - 1).endOf('month').valueOf()).format('YYYY/MM/DD HH:mm:ss');

```

##### 本季度

```
const startTime = moment(moment().quarter(moment().quarter()).startOf('quarter').valueOf()).format('YYYY/MM/DD HH:mm:ss');
const endTime = moment(moment().quarter(moment().quarter()).endOf('quarter').valueOf()).format('YYYY/MM/DD HH:mm:ss');

```

##### 上季度

```
const startTime = moment(moment().quarter(moment().quarter() - 1).startOf('quarter').valueOf()).format('YYYY/MM/DD HH:mm:ss');
const endTime = moment(moment().quarter(moment().quarter() - 1).endOf('quarter').valueOf()).format('YYYY/MM/DD HH:mm:ss');

```



##### 本年

```
const startTime = moment(moment().year(moment().year()).startOf('year').valueOf()).format('YYYY/MM/DD HH:mm:ss');
const endTime = moment(moment().year(moment().year()).endOf('year').valueOf()).format('YYYY/MM/DD HH:mm:ss');

```



##### 上年

```
const startTime = moment(moment().year(moment().year() - 1).startOf('year').valueOf()).format('YYYY/MM/DD HH:mm:ss');
const endTime = moment(moment().year(moment().year() - 1).endOf('year').valueOf()).format('YYYY/MM/DD HH:mm:ss');

```



上面的例子中今天、本周、本月、本年的结束时间都是取到最后的23:59:59。
如果不需要取到未来时间，结束时间统一用下面这行获取系统当前时间：

```
const endTime = moment(moment().valueOf()).format('YYYY/MM/DD HH:mm:ss');

```

##### 快捷时间封装库

shortcut-time.js

```
// 引入 moment 时间插件
import moment from 'moment';

//获取今日/昨日/本周/上周/本月/上月 时间
export default {
    // 获取今日的开始结束时间
    getToday() {
        let obj = {
            starttime: '',
            endtime: ''
        };
        obj.starttime = moment(
            moment()
                .startOf('day')
                .valueOf()
        ).format('YYYY/MM/DD HH:mm:ss');
        obj.endtime = moment(moment().valueOf()).format('YYYY/MM/DD HH:mm:ss');
        return obj;
    },
    // 获取昨日的开始结束时间
    getYesterday() {
        let obj = {
            starttime: '',
            endtime: ''
        };
        obj.starttime = moment(
            moment()
                .add(-1, 'days')
                .startOf('day')
                .valueOf()
        ).format('YYYY/MM/DD HH:mm:ss');
        obj.endtime = moment(
            moment()
                .add(-1, 'days')
                .endOf('day')
                .valueOf()
        ).format('YYYY/MM/DD HH:mm:ss');
        return obj;
    },
    // 获取当前周的开始结束时间
    getCurrWeekDays() {
        let obj = {
            starttime: '',
            endtime: ''
        };
        obj.starttime = moment(
            moment()
                .week(moment().week())
                .startOf('week')
                //.add(1, 'days')
                .valueOf()
        ).format('YYYY/MM/DD HH:mm:ss');
        obj.endtime = moment(moment().valueOf()).format('YYYY/MM/DD HH:mm:ss');
        return obj;
    },
    // 获取上一周的开始结束时间
    getLastWeekDays() {
        let obj = {
            starttime: '',
            endtime: ''
        };
        obj.starttime = moment(
            moment()
                .week(moment().week() - 1)
                .startOf('week')
                //.add(1, 'days')
                .valueOf()
        ).format('YYYY/MM/DD HH:mm:ss');
        obj.endtime = moment(
            moment()
                .week(moment().week() - 1)
                .endOf('week')
                //.add(1, 'days')
                .valueOf()
        ).format('YYYY/MM/DD HH:mm:ss');
        return obj;
    },
    // 获取当前月的开始结束时间
    getCurrMonthDays() {
        let obj = {
            starttime: '',
            endtime: ''
        };
        obj.starttime = moment(
            moment()
                .month(moment().month())
                .startOf('month')
                .valueOf()
        ).format('YYYY/MM/DD HH:mm:ss');
        obj.endtime = moment(moment().valueOf()).format('YYYY/MM/DD HH:mm:ss');
        return obj;
    },
    // 获取上一个月的开始结束时间
    getLastMonthDays() {
        let obj = {
            starttime: '',
            endtime: ''
        };
        obj.starttime = moment(
            moment()
                .month(moment().month() - 1)
                .startOf('month')
                .valueOf()
        ).format('YYYY/MM/DD HH:mm:ss');
        obj.endtime = moment(
            moment()
                .month(moment().month() - 1)
                .endOf('month')
                .valueOf()
        ).format('YYYY/MM/DD HH:mm:ss');
        return obj;
    },
    // 获取本季度的开始结束时间
    getCurrQuarterDays() {
        let obj = {
            starttime: '',
            endtime: ''
        };
        obj.starttime = moment(
            moment()
                .quarter(moment().quarter())
                .startOf('quarter')
                .valueOf()
        ).format('YYYY/MM/DD HH:mm:ss');
        obj.endtime = moment(moment().valueOf()).format('YYYY/MM/DD HH:mm:ss');
        return obj;
    },
    // 获取上一季度的开始结束时间
    getLastQuarterDays() {
        let obj = {
            starttime: '',
            endtime: ''
        };
        obj.starttime = moment(
            moment()
                .quarter(moment().quarter() - 1)
                .startOf('quarter')
                .valueOf()
        ).format('YYYY/MM/DD HH:mm:ss');
        obj.endtime = moment(
            moment()
                .quarter(moment().quarter() - 1)
                .endOf('quarter')
                .valueOf()
        ).format('YYYY/MM/DD HH:mm:ss');
        return obj;
    },
    // 获取本年的开始结束时间
    getCurrYearDays() {
        let obj = {
            starttime: '',
            endtime: ''
        };
        obj.starttime = moment(
            moment()
                .year(moment().year())
                .startOf('year')
                .valueOf()
        ).format('YYYY/MM/DD HH:mm:ss');
        obj.endtime = moment(moment().valueOf()).format('YYYY/MM/DD HH:mm:ss');
        return obj;
    },

    // 获取上一年的开始结束时间
    getLastYearDays() {
        let obj = {
            starttime: '',
            endtime: ''
        };
        obj.starttime = moment(
            moment()
                .year(moment().year() - 1)
                .startOf('year')
                .valueOf()
        ).format('YYYY/MM/DD HH:mm:ss');
        obj.endtime = moment(
            moment()
                .year(moment().year() - 1)
                .endOf('year')
                .valueOf()
        ).format('YYYY/MM/DD HH:mm:ss');
        return obj;
    }
};

```

[转发自](https://blog.csdn.net/lihefei_coder/article/details/103633689?utm_medium=distribute.pc_relevant.none-task-blog-2~default~baidujs_baidulandingword~default-0-103633689-blog-128662630.235^v38^pc_relevant_sort_base2&spm=1001.2101.3001.4242.1&utm_relevant_index=3)

