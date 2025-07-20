# harmony-utils之SnapshotUtil，截图相关工具类

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

##### get  获取已加载的组件的截图，传入组件的组件id，找到对应组件进行截图

```
let pixelMap1 = await SnapshotUtil.get('snapshot_id1');
let pixelMap2 = SnapshotUtil.getSync('snapshot_id2');
```

##### createFromBuilder  在应用后台渲染CustomBuilder自定义组件，并输出其截图

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

##### snapshot  获取窗口截图，使用Promise异步回调

```
let pixelMap3 = await SnapshotUtil.snapshot();
```

##### onSnapshotListener  开启系统截屏事件的监听

```
SnapshotUtil.onSnapshotListener(() => {
  ToastUtil.showToast("系统截图了！");
  LogUtil.error("系统截图了！");
});
```

##### removeSnapshotListener  关闭系统截屏事件的监听

```
 SnapshotUtil.removeSnapshotListener();
 SnapshotUtil.removeSnapshotListener(snapshotCallBack);
```


## 示例代码

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


## 创作不易，请给童长老点赞👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   

