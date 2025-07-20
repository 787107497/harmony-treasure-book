# harmony-utils之TempUtil，温度转换工具类

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

##### C2F  摄氏度转华氏度

```
let f = TempUtil.C2F(27.5);
ToastUtil.showToast(`转换后的华氏度：${f}`);
```

##### F2C  华氏度转摄氏度

```
let c = TempUtil.F2C(81.5)
ToastUtil.showToast(`转换后的摄氏度：${c}`);
```

##### C2K  摄氏度转开尔文

```
let k = TempUtil.C2K(25);
ToastUtil.showToast(`转换后的开尔文：${k}`);
```

##### K2C  开尔文转摄氏度

```
let c = TempUtil.K2C(298.15);
ToastUtil.showToast(`转换后的摄氏度：${c}`);
```

##### F2K  华氏度转开尔文

```
let k = TempUtil.F2K(77);
ToastUtil.showToast(`转换后的开尔文：${k}`);
```

##### K2F  开尔文转华氏度

```
let f = TempUtil.K2F(298.15);
ToastUtil.showToast(`转换后的华氏度：${f}`);
```


## 示例代码

------

```
import { router } from '@kit.ArkUI';
import { MockSetup } from '@ohos/hamock';
import { TempUtil, ToastUtil } from '@pura/harmony-utils';
import { TitleBarView } from '../../component/TitleBarView';
import { DescribeBean } from '../../model/DescribeBean';

/**
 * 温度转换工具类
 */
@Entry
@Component
struct Index {
  private scroller: Scroller = new Scroller();
  @State describe: DescribeBean = router.getParams() as DescribeBean;

  @MockSetup
  mock() {
    this.describe = new DescribeBean("TempUtil", "温度转换工具类");
  }

  build() {
    Column() {
      TitleBarView({ describe: this.describe })
      Divider()
      Scroll(this.scroller) {
        Column() {
          Button("C2F()")
            .btnStyle()
            .onClick(() => {
              let f = TempUtil.C2F(27.5);
              ToastUtil.showToast(`转换后的华氏度：${f}`);
            })
          Button("F2C()")
            .btnStyle()
            .onClick(() => {
              let c = TempUtil.F2C(81.5)
              ToastUtil.showToast(`转换后的摄氏度：${c}`);
            })
          Button("C2K()")
            .btnStyle()
            .onClick(() => {
              let k = TempUtil.C2K(25);
              ToastUtil.showToast(`转换后的开尔文：${k}`);
            })
          Button("K2C()")
            .btnStyle()
            .onClick(() => {
              let c = TempUtil.K2C(298.15);
              ToastUtil.showToast(`转换后的摄氏度：${c}`);
            })
          Button("F2K()")
            .btnStyle()
            .onClick(() => {
              let k = TempUtil.F2K(77);
              ToastUtil.showToast(`转换后的开尔文：${k}`);
            })
          Button("K2F()")
            .btnStyle()
            .onClick(() => {
              let f = TempUtil.K2F(298.15);
              ToastUtil.showToast(`转换后的华氏度：${f}`);
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
   

