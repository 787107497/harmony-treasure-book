# harmony-utils之ToastUtil，吐司工具类

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

##### setDefaultConfig  设置默认统一样式

```
ToastUtil.setDefaultConfig((config) => {
  config.alignment = Alignment.Top
  config.offset = { dx: 0, dy: 80 }
  config.backgroundColor = Color.Red
  config.textColor = Color.White
  config.enableHoverMode = true
  config.hoverModeArea = HoverModeAreaType.BOTTOM_SCREEN
});

ToastUtil.setDefaultConfig((config) => {
  config.alignment = Alignment.Center
  config.offset = { dx: 0, dy: 0 }
  config.showMode = promptAction.ToastShowMode.DEFAULT
  config.duration = 2600
  config.backgroundColor = Color.Blue
  config.textColor = Color.White
  config.enableHoverMode = true
  config.hoverModeArea = HoverModeAreaType.TOP_SCREEN
});
```

##### showToast  弹出吐司，默认时长为2s

```
ToastUtil.showToast("弹出土司，默认时长为2s");

ToastUtil.showToast("弹出土司，当前样式", {
  alignment: Alignment.Center,
  offset: { dx: 0, dy: -100 },
  backgroundColor: '#669900'
});

ToastUtil.showToast("弹出土司，当前样式", {
  alignment: Alignment.Center,
  backgroundColor: '#00AA88',
  textColor: Color.Pink,
  duration: 6000
});
```

##### showShort  弹出短吐司，默认时长为:1.5s

```
ToastUtil.showShort("弹出短土司，时长为:1.5s");
```

##### showLong  弹出长吐司，默认时长为:10s

```
ToastUtil.showLong("弹出短土司，时长为:10s");
```


## 示例代码

------

```
import { promptAction, router } from '@kit.ArkUI';
import { MockSetup } from '@ohos/hamock';
import { ToastUtil } from '@pura/harmony-utils';
import { TitleBarView } from '../../component/TitleBarView';
import { DescribeBean } from '../../model/DescribeBean';

/**
 * 土司工具类（promptAction）
 */
@Preview
@Entry
@Component
struct Index {
  private scroller: Scroller = new Scroller();
  @State describe: DescribeBean = router.getParams() as DescribeBean;

  @MockSetup
  mock() {
    this.describe = new DescribeBean("ToastUtil", "土司工具类（promptAction）");
  }


  build() {
    Column() {
      TitleBarView({ describe: this.describe })
      Divider()
      Scroll(this.scroller) {
        Column() {
          Button("showToast()")
            .btnStyle()
            .onClick(() => {
              ToastUtil.showToast("弹出土司，默认时长为2s");
            })
          Button("showShort()")
            .btnStyle()
            .onClick(() => {
              ToastUtil.showShort("弹出短土司，时长为:1.5s");
            })
          Button("showLong()")
            .btnStyle()
            .onClick(() => {
              ToastUtil.showLong("弹出短土司，时长为:10s");
            })
          Button("showToast()，当前样式")
            .btnStyle()
            .onClick(() => {
              ToastUtil.showToast("弹出土司，当前样式", {
                alignment: Alignment.Top,
                offset: { dx: 0, dy: 30 },
                textColor: Color.Pink,
                backgroundColor: '#00AA88',
                duration: 6000
              });
            })
          Button("设置默认样式(一)")
            .btnStyle()
            .onClick(() => {
              ToastUtil.setDefaultConfig((config) => {
                config.alignment = Alignment.Top
                config.offset = { dx: 0, dy: 80 }
                config.backgroundColor = Color.Red
                config.textColor = Color.White
                config.enableHoverMode = true
                config.hoverModeArea = HoverModeAreaType.BOTTOM_SCREEN
              });
              ToastUtil.showLong("样式(一)设置成功");
            })
          Button("设置默认样式(二)")
            .btnStyle()
            .onClick(() => {
              ToastUtil.setDefaultConfig((config) => {
                config.alignment = Alignment.Center
                config.offset = { dx: 0, dy: 0 }
                config.showMode = promptAction.ToastShowMode.DEFAULT
                config.duration = 2600
                config.backgroundColor = Color.Blue
                config.textColor = Color.White
                config.enableHoverMode = true
                config.hoverModeArea = HoverModeAreaType.TOP_SCREEN
              });
              ToastUtil.showLong("样式(二)设置成功");
            })
          Button("设置默认样式(三)")
            .btnStyle()
            .onClick(() => {
              ToastUtil.setDefaultConfig((config) => {
                config.alignment = Alignment.Bottom
                config.offset = { dx: 0, dy: -80 }
                config.textColor = Color.Red
                config.backgroundColor = Color.Black
                config.enableHoverMode = false
              });
              ToastUtil.showLong("样式(三)设置成功");
            })

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
   

