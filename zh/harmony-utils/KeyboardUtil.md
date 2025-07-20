# harmony-utils之KeyboardUtil，键盘工具类

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

##### show  拉起键盘

```
KeyboardUtil.show("id_input_1000");
```

##### hide  隐藏键盘

```
 KeyboardUtil.hide();
```

##### onKeyboardListener  订阅输入法软键盘显示和隐藏事件

```
KeyboardUtil.onKeyboardListener((show, height) => {
  LogUtil.error("onKeyboardListener-B: " + height);
  if (show) {
    ToastUtil.showToast(`键盘显示，高度为：${height}`);
  } else {
    ToastUtil.showToast(`键盘已关闭！`);
  }
});
```

##### removeKeyboardListener  取消订阅输入法软键盘显示或隐藏事件

```
KeyboardUtil.removeKeyboardListener(); //移除所有
KeyboardUtil.removeKeyboardListener(callback); //移除指定
```


## 示例代码

------

```
import { router } from '@kit.ArkUI';
import { MockSetup } from '@ohos/hamock';
import { KeyboardCallBack, KeyboardUtil, LogUtil, ToastUtil } from '@pura/harmony-utils';
import { TitleBarView } from '../../component/TitleBarView';
import { DescribeBean } from '../../model/DescribeBean';

/**
 * 键盘工具类
 */
@Entry
@Component
struct Index {
  private scroller: Scroller = new Scroller();
  private controller: TextInputController = new TextInputController()
  @State describe: DescribeBean = router.getParams() as DescribeBean;
  private callback: KeyboardCallBack = (show, height) => {
    LogUtil.error("onKeyboardListener-A: " + height);
    if (show) {
      ToastUtil.showToast(`键盘显示！高度为：${height}`);
    } else {
      ToastUtil.showToast(`键盘已关闭！`);
    }
  };

  @MockSetup
  mock() {
    this.describe = new DescribeBean("KeyboardUtil", "键盘工具类");
  }

  build() {
    Column() {
      TitleBarView({ describe: this.describe })
      Divider()
      Scroll(this.scroller) {
        Column() {
          Button("show()，主动拉起键盘")
            .btnStyle()
            .onClick(() => {
              KeyboardUtil.show("id_input_1000");
            })
          Button("hide()，关闭键盘")
            .btnStyle()
            .onClick(() => {
              KeyboardUtil.hide();
            })
          Button("onKeyboardListener()")
            .btnStyle()
            .onClick(() => {
              KeyboardUtil.onKeyboardListener((show, height) => {
                LogUtil.error("onKeyboardListener-B: " + height);
                if (show) {
                  ToastUtil.showToast(`键盘显示，高度为：${height}`);
                } else {
                  ToastUtil.showToast(`键盘已关闭！`);
                }
              });
            })
          Button("removeKeyboardListener()")
            .btnStyle()
            .onClick(() => {
              KeyboardUtil.removeKeyboardListener(); //移除所有
            })
          Button("onKeyboardListener()-指定")
            .btnStyle()
            .onClick(() => {
              KeyboardUtil.onKeyboardListener(this.callback);
            })
          Button("removeKeyboardListener()-指定")
            .btnStyle()
            .onClick(() => {
              KeyboardUtil.removeKeyboardListener(this.callback); //移除指定
            })

          TextInput({ placeholder: '请输入', controller: this.controller })
            .margin({ top: 30 })
            .width('90%')
            .id("id_input_1000")

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
   

