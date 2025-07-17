# Harmony-utils: SnapshotUtil, screenshot related tool class

## Introduction and description of harmony-utils

------
[harmony-utils](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils) A HarmonyOS tool library with rich features and extremely easy to use, with the help of many practical tools, is committed to helping developers quickly build Hongmeng applications. Its encapsulated tools cover APP, device, screen, authorization, notification, inter-thread communication, pop-up frames, toast, biometric authentication, user preferences, taking photos, albums, scanning codes, files, logs, exception capture, characters, strings, numbers, collections, dates, random, base64, encryption, decryption, JSON and other functions, which can meet various development needs.   
[picker_utils](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fpicker_utils) It is a sub-store split by harmony-utils, including PickerUtil, PhotoHelper, and ScanUtil.

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

##### get get a screenshot of the loaded component, pass in the component id of the component, find the corresponding component to take a screenshot

```
let pixelMap1 = await SnapshotUtil.get('snapshot_id1');
let pixelMap2 = SnapshotUtil.getSync('snapshot_id2');
```

##### createFromBuilder renders CustomBuilder custom components in the application background and outputs screenshots

```
SnapshotUtil.createFromBuilder(() => {
  this.RandomBuilder()
}).then((pixelMap) => {
  Utils.showSheetImg(pixelMap);
}).catch((err: BusinessError) => {
  ToastUtil.showToast("组件生成图片异常！");
});

@Builder
RandomBuilder() {
  Column() {
    Text("Builder截图")
      .fontSize(20)
      .fontWeight(FontWeight.Bold)
      .fontStyle(FontStyle.Italic)
      .margin({ top: 20 })
    Image($r("app.media.test_as4"))
      .margin({ top: 30, bottom: 10 })
      .padding(10)
      .width('95%')
      .backgroundColor(Color.Pink)
  }
  .backgroundColor(Color.Blue)
  .padding(10)
  .width('100%')
  .aspectRatio(1)
  .margin({ top: 50 })
  .id("rBuilder")
}
```

##### snapshot to get window screenshot and use Promise asynchronous callback

```
let pixelMap3 = await SnapshotUtil.snapshot();
```

##### onSnapshotListener enables monitoring of system screenshot events

```
SnapshotUtil.onSnapshotListener(() => {
  ToastUtil.showToast("系统截图了！");
  LogUtil.error("系统截图了！");
});
```

##### removeSnapshotListener Close listening of system screenshot events

```
 SnapshotUtil.removeSnapshotListener();
 SnapshotUtil.removeSnapshotListener(snapshotCallBack);
```

## Full Code Example

------

```
import { router } from '@kit.ArkUI';
import { LogUtil, SnapshotUtil, ToastUtil } from '@pura/harmony-utils';
import { DescribeBean } from '../../model/DescribeBean';
import { BusinessError } from '@kit.BasicServicesKit';
import { MockSetup } from '@ohos/hamock';
import { TitleBarView } from '../../component/TitleBarView';
import { Utils } from '../../utils/Utils';

/**
 * 组件截图和窗口截图工具类
 */
@Entry
@Component
struct Index {
  private scroller: Scroller = new Scroller();
  @State describe: DescribeBean = router.getParams() as DescribeBean;
  private snapshotCallBack: VoidCallback = () => { //系统截图监听回调
    ToastUtil.showToast("您已成功截图！");
    LogUtil.error("您已成功截图！");
  }

  @MockSetup
  mock() {
    this.describe = new DescribeBean("SnapshotUtil", "组件截图和窗口截图工具类");
  }

  build() {
    Column() {
      TitleBarView({ describe: this.describe })
      Divider()
      Scroll(this.scroller) {
        Column() {
          Button("get()")
            .btnStyle()
            .onClick(async () => {
              let pixelMap1 = await SnapshotUtil.get('snapshot_id1');
              Utils.showSheetImg(pixelMap1);
            })
          Button("getSync()")
            .btnStyle()
            .onClick(() => {
              let pixelMap1 = SnapshotUtil.getSync('snapshot_id2');
              Utils.showSheetImg(pixelMap1);
            })
          Button("createFromBuilder()")
            .btnStyle()
            .onClick(() => {
              SnapshotUtil.createFromBuilder(() => {
                this.RandomBuilder()
              }).then((pixelMap) => {
                Utils.showSheetImg(pixelMap);
              }).catch((err: BusinessError) => {
                LogUtil.error("createFromBuilder-异常信息：\n" + JSON.stringify(err));
                ToastUtil.showToast("组件生成图片异常！");
              });
            })
          Button("snapshot()")
            .btnStyle()
            .onClick(async () => {
              let pixelMap3 = await SnapshotUtil.snapshot();
              Utils.showSheetImg(pixelMap3);
            })
          Button("onSnapshotListener()")
            .btnStyle()
            .onClick(() => {
              SnapshotUtil.onSnapshotListener(() => {
                ToastUtil.showToast("系统截图了！");
                LogUtil.error("系统截图了！");
              });
            })
          Button("removeSnapshotListener()")
            .btnStyle()
            .onClick(() => {
              SnapshotUtil.removeSnapshotListener();
            })
          
          Button("onSnapshotListener()-指定")
            .btnStyle()
            .onClick(() => {
              SnapshotUtil.onSnapshotListener(this.snapshotCallBack);
            })
          Button("removeSnapshotListener()-指定")
            .btnStyle()
            .onClick(() => {
              SnapshotUtil.removeSnapshotListener(this.snapshotCallBack);
            })

          Column() {
            Text("id组件截图1")
              .fontSize(16)
              .fontWeight(FontWeight.Bold)
              .fontStyle(FontStyle.Italic)
              .margin({ top: 10 })
            Column() {
              Text("id组件截图2")
                .fontSize(12)
                .fontWeight(FontWeight.Bold)
                .fontStyle(FontStyle.Italic)
                .margin({ top: 10 })
              Image($r("app.media.test_as3"))
                .margin({ top: 10, bottom: 10 })
                .borderRadius(6)
            }
            .backgroundColor(Color.Pink)
            .borderRadius(10)
            .padding(10)
            .margin({ top: 10 })
            .width('95%')
            .id('snapshot_id2')
          }
          .backgroundColor(Color.Brown)
          .border({
            width: 5,
            radius: 5,
            color: Color.Orange,
            style: BorderStyle.Dashed
          })
          .padding(10)
          .width('90%')
          .margin({ top: 50 })
          .id('snapshot_id1')

          Blank().layoutWeight(1)
        }
        .margin({ top: 5, bottom: 5 })
      }
      .layoutWeight(1)
    }
    .width('100%')
    .height('100%')
    .justifyContent(FlexAlign.Start)
    .backgroundColor($r('app.color.main_background'))
  }

  @Builder
  RandomBuilder() {
    Column() {
      Text("Builder截图")
        .fontSize(20)
        .fontWeight(FontWeight.Bold)
        .fontStyle(FontStyle.Italic)
        .margin({ top: 20 })
      Image($r("app.media.test_as4"))
        .margin({ top: 30, bottom: 10 })
        .padding(10)
        .width('95%')
        .backgroundColor(Color.Pink)
    }
    .backgroundColor(Color.Blue)
    .padding(10)
    .width('100%')
    .aspectRatio(1)
    .margin({ top: 50 })
    .id("rBuilder")
  }

}


@Styles
function btnStyle() {
  .width('90%')
  .margin({ top: 10, bottom: 5 })
}
```

## Creation is not easy, please give Elder Tong a thumbs up 👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   

