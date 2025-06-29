# china_area

## 🏆Introduction and Recommendations

[china_area](https://ohpm.openharmony.cn/#/cn/detail/@nutpi%2Fchina_area)China's regional data, provincial, municipal and county data.

[harmony-utils](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)
A HarmonyOS tool library with rich features and extremely easy to use, with the help of many practical tools, is committed to helping developers quickly build Hongmeng applications.

[harmony-dialog](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-dialog)
An extremely simple and easy-to-use zero-invasion pop-up window, which can be easily implemented with just one line of code, and can be easily popped up no matter where you are.

## 🌞Download and install

`ohpm i @nutpi/china_area`
OpenHarmony ohpm
For more information, please refer to[如何安装 OpenHarmony ohpm 包](https://ohpm.openharmony.cn/#/cn/help/downloadandinstall)

## 📚API detailed explanation[使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/plug/ChinaAreaPage.ets)

| AreaHelper Method | Introduction |
|:-------------------------------------------|:--------------|
| getAreaStrSync<br/>getAreaStr | Get JSON strings for provinces, cities and counties |
| getAreaSync<br>getArea | Get data from provinces, cities and counties |
| getCityByNameSync<br>getCityByName | Get the following city according to the provincial name |
| getDintrictByNameSync<br>getDintrictByName | Get the following district and county based on the city name |

## 📚Sample code

```
//获取省市县的JSON字符串
let txtStr = await AreaHelper.getAreaStr();
let areaList = JSONUtil.jsonToArray<AreaEntity>(txtStr);


//获取省市县的数据
let areas = AreaHelper.getAreaSync();


//根据省名获取下面的市
let citys = await AreaHelper.getCityByName("安徽省");


//根据市名获取下面的区县
let list = AreaHelper.getDistrictByNameSync("合肥市");


//配合‘@pura/harmony-dialog’的\nshowTextPickerDialog()方法使用
let data = AreaHelper.getAreaSync();
DialogHelper.showTextPickerDialog({
  title: "请选择",
  range: data,
  onChange: (value: string | string[], index: number | number[]) => {
    LogUtil.error(`value: ${value} --- index: ${index}`);
  },
  onAction: (action: number, dialogId: string, value: string | string[]) => {
    if (action === DialogAction.SURE) {
      DialogHelper.showToast(`已选择：${value}`);
    }
  }
});
```

## 🍎Communication and communication 🙏

Any problems found during use can be asked[Issue](https://gitee.com/tongyuyan/harmony-utils/issues)Give us;
Of course, we also welcome you to send us a message[PR](https://gitee.com/tongyuyan/harmony-utils/pulls) 。


## 🌏Open Source Protocol

This project is based on[Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0.html), when copying and borrowing codes, please be sure to indicate the source.
