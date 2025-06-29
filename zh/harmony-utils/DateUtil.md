# harmony-utils之DateUtil，日期工具类

## harmony-utils 简介与说明

------
[harmony-utils](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils) 一款功能丰富且极易上手的HarmonyOS工具库，借助众多实用工具类，致力于助力开发者迅速构建鸿蒙应用。其封装的工具涵盖了APP、设备、屏幕、授权、通知、线程间通信、弹框、吐司、生物认证、用户首选项、拍照、相册、扫码、文件、日志，异常捕获、字符、字符串、数字、集合、日期、随机、base64、加密、解密、JSON等一系列的功能和操作，能够满足各种不同的开发需求。    
[picker_utils](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fpicker_utils) 是harmony-utils拆分出来的一个子库，包含PickerUtil、PhotoHelper、ScanUtil。

下载安装  
`ohpm i @pura/harmony-utils`  
`ohpm i @pura/picker_utils`

 ```
  //全局初始化方法，在UIAbility的onCreate方法中初始化 AppUtil.init()
  onCreate(want: Want, launchParam: AbilityConstant.LaunchParam): void {
    AppUtil.init(this.context);
  }
 ```

## API方法与使用

------

##### getFormatDate  获取格式化日期，将传入的日期格式化为Date

```
let date1 = DateUtil.getFormatDate(1716181651533);
let date2 = DateUtil.getFormatDate("2024-05-21");
let date3 = DateUtil.getFormatDate("2024-05-20 13:07:45");
let date4 = DateUtil.getFormatDate("2024年05月20日 13时07分45秒");
let date5 = DateUtil.getFormatDate("2024年05月20日");
let date6 = DateUtil.getFormatDate("2024/05/20");
let date7 = DateUtil.getFormatDate(new Date());
```

##### getFormatDateStr  获取格式化日期，将传入的日期格式化为指定格式的字符串

```
let todayStr1 = DateUtil.getFormatDateStr(1716181651533);
let todayStr2 = DateUtil.getFormatDateStr(DateUtil.getTodayTime(), DATE_FORMAT11);
let todayStr3 = DateUtil.getFormatDateStr("2024-05-20 13:07:45", DATE_FORMAT17);
let todayStr4 = DateUtil.getFormatDateStr("2024年05月20日 13时07分45秒", DATE_FORMAT16);
let todayStr5 = DateUtil.getFormatDateStr("2024年05月20日");
let todayStr6 = DateUtil.getFormatDateStr("2024/05/20");
let todayStr7 = DateUtil.getFormatDateStr(new Date());
```

##### getToday  获取今天的日期

```
let today = DateUtil.getToday();
```

##### getTodayTime  获取今天的时间戳

```
let todayTime = DateUtil.getTodayTime();
```

##### getTodayStr  获取今天的时间，字符串类型

```
let todayStr1 = DateUtil.getTodayStr();
let todayStr2 = DateUtil.getTodayStr("yyyy-MM-dd HH:mm");
let todayStr3 = DateUtil.getTodayStr("yyyy-MM-dd HH");
let todayStr4 = DateUtil.getTodayStr("yyyy-MM-dd");
let todayStr5 = DateUtil.getTodayStr("yyyy/MM/dd");
let todayStr6 = DateUtil.getTodayStr("yyyy年MM月dd日");
let todayStr7 = DateUtil.getTodayStr("yyyy年MM月dd日 HH时mm分ss秒");
```

##### isToday  判断日期是否是今天

```
let today = DateUtil.getToday();
let todayTime = 1723983090245;
let todayStr1 = "2024年8月18日";
let b1 = DateUtil.isToday(today);
let b2 = DateUtil.isToday(todayTime);
let b3 = DateUtil.isToday(todayStr1);
```

##### getNowYear  获取当前年

```
let nowYear = DateUtil.getNowYear();
```

##### getNowMonth  获取当前月

```
let nowMonth = DateUtil.getNowMonth();
```

##### getNowDay  获取当前日

```
let nowDay = DateUtil.getNowDay();
```

##### isLeapYear  判断是否是闰年

```
let isLeapYear1 = DateUtil.isLeapYear();
let isLeapYear2 = DateUtil.isLeapYear(1999);
let isLeapYear3 = DateUtil.isLeapYear(2000);
let isLeapYear4 = DateUtil.isLeapYear(2026);
```

##### getDaysByYear  获取指定年份的天数

```
let day1 = DateUtil.getDaysByYear(2024);
```

##### getDaysByMonth  获取指定月份的天数

```
let day2 = DateUtil.getDaysByMonth(2024, 8);
```

##### isSameYear  判断两个日期是否是同一年

```
let isSameYear = DateUtil.isSameYear("2024-8-18", DateUtil.getToday());
```

##### isSameMonth  判断两个日期是否是同一月

```
let isSameMonth = DateUtil.isSameMonth("2024-8-1", "2024年08月18日");
```

##### isSameWeek  判断两个日期是否是同一周

```
let isSameWeek = DateUtil.isSameWeek("2024-8-12", "2024/08/18");
```

##### isSameDay  判断是否是同一天

```
let isSameDay = DateUtil.isSameDay("2024-08-18", "2024年08月18日");
```

##### isWeekend  判断指定的日期在日历中是否为周末

```
let b1 = DateUtil.isWeekend("2024-08-12");
let b2 = DateUtil.isWeekend("2024-08-15");
let b3 = DateUtil.isWeekend("2024-08-17");
let b4 = DateUtil.isWeekend(DateUtil.getToday());
```

##### compareDays  比较指定日期相差的天数

```
let diff1 = DateUtil.compareDays("2024-8-08", DateUtil.getToday());
let diff2 = DateUtil.compareDays("2024-8-21", "2024年08月18日");
```

##### compareDate  比较指定日期相差的毫秒数

```
let diff3 = DateUtil.compareDate("2024-8-22", "2024/08/18");
let diff4 = DateUtil.compareDate("2024-08-18", DateUtil.getToday());
```

##### getAmountDay  获取前几天日期或后几天日期

```
let date1 = DateUtil.getAmountDay(DateUtil.getToday(), 2);
let date2 = DateUtil.getAmountDay("2024-8-08", -2);
```

##### getAmountDayStr  获取前几天日期或后几天日期,返回字符串

```
let date3 = DateUtil.getAmountDayStr("2024-8-8", 3);
let date4 = DateUtil.getAmountDayStr(DateUtil.getToday(), -3);
```

##### getBeforeDay  获取前一天日期

```
let date1 = DateUtil.getBeforeDay(DateUtil.getToday());
```

##### getBeforeDayStr  获取前一天日期,返回字符串

```
let date2 = DateUtil.getBeforeDayStr("2024-8-08");
```

##### getAfterDay  获取后一天日期

```
let date3 = DateUtil.getAfterDay(DateUtil.getToday());
```

##### getAfterDayStr  获取后一天日期,返回字符串

```
let date4 = DateUtil.getAfterDayStr("2024-8-8");
```

##### getWeekOfMonth  获取给定日期是当月的第几周

```
let n1 = DateUtil.getWeekOfMonth(DateUtil.getToday());
```

##### getWeekDay  获取给定的日期是星期几

```
let n2 = DateUtil.getWeekDay("2024-8-08");
```

##### getLastDayOfMonth  获取给定年份和月份的最后一天是几号

```
let n3 = DateUtil.getLastDayOfMonth(2024, 8);
```

##### getFormatTime  格式化时间日期字符串（DateTimeFormat）

```
let n1 = DateUtil.getFormatTime(DateUtil.getToday());
let n2 = DateUtil.getFormatTime(DateUtil.getToday(), { dateStyle: "full", timeStyle: "medium", hourCycle: "h24" });
let n3 = DateUtil.getFormatTime(DateUtil.getToday(), { dateStyle: "full", timeStyle: "medium", hourCycle: "h12" });
let n4 = DateUtil.getFormatTime(DateUtil.getToday(), { weekday: "short" });
```

##### getFormatRange  格式化时间日期段字符串（DateTimeFormat）

```
let fr = DateUtil.getFormatRange(DateUtil.getAfterDay("2024-05-01"),DateUtil.getToday());
```

##### getFormatRelativeTime  格式化相对时间

```
let frt1 = DateUtil.getFormatRelativeTime(2, 'year');
let frt2 = DateUtil.getFormatRelativeTime(-1, 'year');
let frt3 = DateUtil.getFormatRelativeTime(-1, 'quarter');
let frt4 = DateUtil.getFormatRelativeTime(-2, 'month');
let frt5 = DateUtil.getFormatRelativeTime(-3, 'week');
let frt6 = DateUtil.getFormatRelativeTime(-6, 'day');
let frt7 = DateUtil.getFormatRelativeTime(-6, 'hour');
let frt8 = DateUtil.getFormatRelativeTime(-7, 'minute');
let frt9 = DateUtil.getFormatRelativeTime(-8, 'second');
```

##### getTipDateStr  格式化时间戳，获取提示性时间字符串

```
let timeStamp = DateUtil.getTodayTime();
let tip1 = DateUtil.getTipDateStr(timeStamp);
let tip2 = DateUtil.getTipDateStr(timeStamp - 60000 * 5);
let tip3 = DateUtil.getTipDateStr(timeStamp - 3600000 * 3);
let tip4 = DateUtil.getTipDateStr(timeStamp - 3600000 * 24 * 2);
let tip5 = DateUtil.getTipDateStr(timeStamp - 3600000 * 24 * 360 * 1);
```

## 创作不易，请给童长老点赞👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   



