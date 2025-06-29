# DateUtil, date tool class

## Introduction and description of harmony-utils

------
[harmony-utils](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)A HarmonyOS tool library with rich features and extremely easy to use, with the help of many practical tools, is committed to helping developers quickly build Hongmeng applications. Its encapsulated tools cover APP, device, screen, authorization, notification, inter-thread communication, pop-up frames, toast, biometric authentication, user preferences, taking photos, albums, scanning codes, files, logs, exception capture, characters, strings, numbers, collections, dates, random, base64, encryption, decryption, JSON and other functions, which can meet various development needs.
[picker_utils](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fpicker_utils)It is a sub-store split by harmony-utils, including PickerUtil, PhotoHelper, and ScanUtil.

Download and install
`ohpm i @pura/harmony-utils`  
`ohpm i @pura/picker_utils`

 ```
  //全局初始化方法，在UIAbility的onCreate方法中初始化 AppUtil.init()
  onCreate(want: Want, launchParam: AbilityConstant.LaunchParam): void {
    AppUtil.init(this.context);
  }
 ```

## API methods and usage

------

##### getFormatDate Gets the formatted date and formats the passed date as Date

```
let date1 = DateUtil.getFormatDate(1716181651533);
let date2 = DateUtil.getFormatDate("2024-05-21");
let date3 = DateUtil.getFormatDate("2024-05-20 13:07:45");
let date4 = DateUtil.getFormatDate("2024年05月20日 13时07分45秒");
let date5 = DateUtil.getFormatDate("2024年05月20日");
let date6 = DateUtil.getFormatDate("2024/05/20");
let date7 = DateUtil.getFormatDate(new Date());
```

##### getFormatDateStr Gets the formatted date and formats the passed date into a string of the specified format

```
let todayStr1 = DateUtil.getFormatDateStr(1716181651533);
let todayStr2 = DateUtil.getFormatDateStr(DateUtil.getTodayTime(), DATE_FORMAT11);
let todayStr3 = DateUtil.getFormatDateStr("2024-05-20 13:07:45", DATE_FORMAT17);
let todayStr4 = DateUtil.getFormatDateStr("2024年05月20日 13时07分45秒", DATE_FORMAT16);
let todayStr5 = DateUtil.getFormatDateStr("2024年05月20日");
let todayStr6 = DateUtil.getFormatDateStr("2024/05/20");
let todayStr7 = DateUtil.getFormatDateStr(new Date());
```

##### getToday Get today's date

```
let today = DateUtil.getToday();
```

##### getTodayTime Get the timestamp of today

```
let todayTime = DateUtil.getTodayTime();
```

##### getTodayStr Gets the time of today, string type

```
let todayStr1 = DateUtil.getTodayStr();
let todayStr2 = DateUtil.getTodayStr("yyyy-MM-dd HH:mm");
let todayStr3 = DateUtil.getTodayStr("yyyy-MM-dd HH");
let todayStr4 = DateUtil.getTodayStr("yyyy-MM-dd");
let todayStr5 = DateUtil.getTodayStr("yyyy/MM/dd");
let todayStr6 = DateUtil.getTodayStr("yyyy年MM月dd日");
let todayStr7 = DateUtil.getTodayStr("yyyy年MM月dd日 HH时mm分ss秒");
```

##### isToday determines whether the date is today

```
let today = DateUtil.getToday();
let todayTime = 1723983090245;
let todayStr1 = "2024年8月18日";
let b1 = DateUtil.isToday(today);
let b2 = DateUtil.isToday(todayTime);
let b3 = DateUtil.isToday(todayStr1);
```

##### getNowYear Get the current year

```
let nowYear = DateUtil.getNowYear();
```

##### getNowMonth Get the current month

```
let nowMonth = DateUtil.getNowMonth();
```

##### getNowDay Get the current day

```
let nowDay = DateUtil.getNowDay();
```

##### isLeapYear determines whether it is a leap year

```
let isLeapYear1 = DateUtil.isLeapYear();
let isLeapYear2 = DateUtil.isLeapYear(1999);
let isLeapYear3 = DateUtil.isLeapYear(2000);
let isLeapYear4 = DateUtil.isLeapYear(2026);
```

##### getDaysByYear Gets the number of days for the specified year

```
let day1 = DateUtil.getDaysByYear(2024);
```

##### getDaysByMonth Gets the number of days in the specified month

```
let day2 = DateUtil.getDaysByMonth(2024, 8);
```

##### isSameYear determines whether the two dates are the same year

```
let isSameYear = DateUtil.isSameYear("2024-8-18", DateUtil.getToday());
```

##### isSameMonth determines whether two dates are the same month

```
let isSameMonth = DateUtil.isSameMonth("2024-8-1", "2024年08月18日");
```

##### isSameWeek determines whether two dates are the same week

```
let isSameWeek = DateUtil.isSameWeek("2024-8-12", "2024/08/18");
```

##### isSameDay determines whether it is the same day

```
let isSameDay = DateUtil.isSameDay("2024-08-18", "2024年08月18日");
```

##### isWeekend Determines whether the specified date is a weekend in the calendar

```
let b1 = DateUtil.isWeekend("2024-08-12");
let b2 = DateUtil.isWeekend("2024-08-15");
let b3 = DateUtil.isWeekend("2024-08-17");
let b4 = DateUtil.isWeekend(DateUtil.getToday());
```

##### compareDays Compare the number of days that are different from the specified date

```
let diff1 = DateUtil.compareDays("2024-8-08", DateUtil.getToday());
let diff2 = DateUtil.compareDays("2024-8-21", "2024年08月18日");
```

##### compareDate Compare the number of milliseconds of the specified date difference

```
let diff3 = DateUtil.compareDate("2024-8-22", "2024/08/18");
let diff4 = DateUtil.compareDate("2024-08-18", DateUtil.getToday());
```

##### getAmountDay Get the previous days date or the next few days date

```
let date1 = DateUtil.getAmountDay(DateUtil.getToday(), 2);
let date2 = DateUtil.getAmountDay("2024-8-08", -2);
```

##### getAmountDayStr Gets the date of the previous few days or the date of the next few days, and returns the string

```
let date3 = DateUtil.getAmountDayStr("2024-8-8", 3);
let date4 = DateUtil.getAmountDayStr(DateUtil.getToday(), -3);
```

##### getBeforeDay Get the previous day date

```
let date1 = DateUtil.getBeforeDay(DateUtil.getToday());
```

##### getBeforeDayStr Gets the date of the previous day and returns the string

```
let date2 = DateUtil.getBeforeDayStr("2024-8-08");
```

##### getAfterDay The day after getting

```
let date3 = DateUtil.getAfterDay(DateUtil.getToday());
```

##### getAfterDayStr Gets the date after one day and returns the string

```
let date4 = DateUtil.getAfterDayStr("2024-8-8");
```

##### getWeekOfMonth Gets what week of the given date is the month

```
let n1 = DateUtil.getWeekOfMonth(DateUtil.getToday());
```

##### getWeekDay Gets the given date is the day of the week

```
let n2 = DateUtil.getWeekDay("2024-8-08");
```

##### getLastDayOfMonth Gets what day the last day of a given year and month is

```
let n3 = DateUtil.getLastDayOfMonth(2024, 8);
```

##### getFormatTime Format time Date string (DateTimeFormat)

```
let n1 = DateUtil.getFormatTime(DateUtil.getToday());
let n2 = DateUtil.getFormatTime(DateUtil.getToday(), { dateStyle: "full", timeStyle: "medium", hourCycle: "h24" });
let n3 = DateUtil.getFormatTime(DateUtil.getToday(), { dateStyle: "full", timeStyle: "medium", hourCycle: "h12" });
let n4 = DateUtil.getFormatTime(DateUtil.getToday(), { weekday: "short" });
```

##### getFormatRange Format Time Date field string (DateTimeFormat)

```
let fr = DateUtil.getFormatRange(DateUtil.getAfterDay("2024-05-01"),DateUtil.getToday());
```

##### getFormatRelativeTime Format Relative Time

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

##### getTipDateStr Format the timestamp to get prompt time string

```
let timeStamp = DateUtil.getTodayTime();
let tip1 = DateUtil.getTipDateStr(timeStamp);
let tip2 = DateUtil.getTipDateStr(timeStamp - 60000 * 5);
let tip3 = DateUtil.getTipDateStr(timeStamp - 3600000 * 3);
let tip4 = DateUtil.getTipDateStr(timeStamp - 3600000 * 24 * 2);
let tip5 = DateUtil.getTipDateStr(timeStamp - 3600000 * 24 * 360 * 1);
```

## Creation is not easy, please give Elder Tong a thumbs up 👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   



