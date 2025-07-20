# china_area

## 🏆简介与推荐

[china_area](https://ohpm.openharmony.cn/#/cn/detail/@nutpi%2Fchina_area) 中国区域数据，省市县三级数据。

[harmony-utils](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)
一款功能丰富且极易上手的HarmonyOS工具库，借助众多实用工具类，致力于助力开发者迅速构建鸿蒙应用。

[harmony-dialog](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-dialog)
一款极为简单易用的零侵入弹窗，仅需一行代码即可轻松实现，无论在何处都能够轻松弹出。

## 🌞下载安装

`ohpm i @nutpi/china_area`
OpenHarmony ohpm
环境配置等更多内容，请参考[如何安装 OpenHarmony ohpm 包](https://ohpm.openharmony.cn/#/cn/help/downloadandinstall)

## 📚API详解 [使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/plug/ChinaAreaPage.ets)

| AreaHelper方法                               | 介绍            |
|:-------------------------------------------|:--------------|
| getAreaStrSync<br/>getAreaStr              | 获取省市县的JSON字符串 |
| getAreaSync<br>getArea                     | 获取省市县的数据      |
| getCityByNameSync<br>getCityByName         | 根据省名获取下面的市    |
| getDistrictByNameSync<br>getDistrictByName | 根据市名获取下面的区县   |

## 📚示例代码

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

```
import { router } from '@kit.ArkUI';
import { AreaEntity, AreaHelper } from '@nutpi/china_area';
import { JSONUtil, LogUtil, StrUtil } from '@pura/harmony-utils';
import { TitleBarView } from '../../component/TitleBarView';
import { DescribeBean } from '../../model/DescribeBean';
import { JSON } from '@kit.ArkTS';
import { DialogAction, DialogHelper } from '@pura/harmony-dialog';

/**
 * @nutpi/china_area，使用案例
 */
@Entry
@ComponentV2
export struct ChinaAreaPage {
  private scroller: Scroller = new Scroller();
  @Local describe: DescribeBean = router.getParams() as DescribeBean;
  @Local txtStr: string = "";


  build() {
    Column() {
      TitleBarView({ describe: this.describe })
      Divider()
      Scroll(this.scroller) {
        Column({ space: 5 }) {
          Button("getAreaStr()")
            .btnStyle()
            .onClick(async () => {
              this.txtStr = await AreaHelper.getAreaStr();
              let data = JSONUtil.jsonToArray<AreaEntity>(this.txtStr);
              DialogHelper.showToast(`${data.length}`);
            })
          Button("getAreaStr()")
            .btnStyle()
            .onClick(async () => {
              let list = await AreaHelper.getArea();
              LogUtil.error(`长度：${list.length}`);
              this.txtStr = JSON.stringify(list,null,2);
            })
          Button("getCityByName()")
            .btnStyle()
            .onClick(async () => {
              let citys = await AreaHelper.getCityByName("安徽省");
              this.txtStr = JSON.stringify(citys, null, 2);
            })
          Button("getDistrictByNameSync()")
            .btnStyle()
            .onClick(() => {
              let list = AreaHelper.getDistrictByNameSync("合肥市");
              this.txtStr = JSON.stringify(list, null, 2);
            })
          Button("配合‘@pura/harmony-dialog’的\nshowTextPickerDialog()方法使用")
            .labelStyle({ maxLines: 3 })
            .padding({ top: 10, bottom: 10 })
            .btnStyle()
            .onClick(() => {
              this.txtStr = "";
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
            })

          Blank().layoutWeight(1)

          Text(this.txtStr)
            .visibility(StrUtil.isNotEmpty(this.txtStr) ? Visibility.Visible : Visibility.None)
            .textStyle()

          Blank().layoutWeight(1)
        }
        .margin({ top: 5, bottom: 5 })
      }
      .layoutWeight(1)
    }
    .width('100%')
    .height('100%')
    .backgroundColor($r('app.color.main_background'))
  }
}


@Styles
function btnStyle() {
  .width('90%')
  .margin({ top: 10, bottom: 5 })
}

@Styles
function textStyle() {
  .width('95%')
  .padding(10)
  .shadow(ShadowStyle.OUTER_DEFAULT_XS)
  .margin({ top: 5, bottom: 10 })
  .border({
    width: 1,
    color: Color.Grey,
    radius: 10,
    style: BorderStyle.Dashed
  })
}
```



## 🍎沟通与交流🙏

使用过程中发现任何问题都可以提 [Issue](https://gitee.com/tongyuyan/harmony-utils/issues)给我们；   
当然，我们也非常欢迎你给我们发 [PR](https://gitee.com/tongyuyan/harmony-utils/pulls) 。


## 🌏开源协议

本项目基于 [Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0.html) ，在拷贝和借鉴代码时，请大家务必注明出处。
