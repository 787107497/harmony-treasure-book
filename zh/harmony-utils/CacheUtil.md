# harmony-utils之CacheUtil，缓存工具类

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

##### has  缓存中的数据是否存在

```
  let pwd = CacheUtil.has("pwd");
  ToastUtil.showToast(`缓存是否存在：${pwd}`);
```

##### put  将数据存入缓存中

```
 CacheUtil.put("pwd", "ABCD@12345");
 ToastUtil.showToast("缓存密码成功");
```

##### get  获取缓存中的数据

```
 let pwd = CacheUtil.get<string>("pwd");
 ToastUtil.showToast(`取值：${pwd}`);
```

##### remove  删除key对应的缓存

```
 CacheUtil.remove("pwd");
 ToastUtil.showToast(`缓存移除成功！`);
```

##### isEmpty  判断缓存是否为空

```
 let blEmpty = CacheUtil.isEmpty();
 ToastUtil.showToast(`缓存是否为空：${blEmpty}`);
```

##### clear  清除缓存数据

```
 CacheUtil.clear();
 ToastUtil.showToast(`清除缓存数据成功`);
```


## 示例代码

------

```
import { router } from '@kit.ArkUI';
import { MockSetup } from '@ohos/hamock';
import { CacheUtil, ToastUtil } from '@pura/harmony-utils';
import { TitleBarView } from '../../component/TitleBarView';
import { DescribeBean } from '../../model/DescribeBean';

/**
 * "缓存工具类
 */
@Entry
@Component
struct Index {
  private scroller: Scroller = new Scroller();
  @State describe: DescribeBean = router.getParams() as DescribeBean;

  @MockSetup
  mock() {
    this.describe = new DescribeBean("CacheUtil", "缓存工具类");
  }

  build() {
    Column() {
      TitleBarView({ describe: this.describe })
      Divider()
      Scroll(this.scroller) {
        Column() {
          Button("put()")
            .btnStyle()
            .onClick(() => {
              CacheUtil.put("pwd", "ABCD@12345");
              ToastUtil.showToast("缓存密码成功");
            })
          Button("get()")
            .btnStyle()
            .onClick(() => {
              let pwd = CacheUtil.get<string>("pwd");
              ToastUtil.showToast(`取值：${pwd}`);
            })
          Button("has()")
            .btnStyle()
            .onClick(() => {
              let pwd = CacheUtil.has("pwd");
              ToastUtil.showToast(`缓存是否存在：${pwd}`);
            })
          Button("remove()")
            .btnStyle()
            .onClick(() => {
              CacheUtil.remove("pwd");
              ToastUtil.showToast(`缓存移除成功！`);
            })
          Button("isEmpty()")
            .btnStyle()
            .onClick(() => {
              let blEmpty = CacheUtil.isEmpty();
              ToastUtil.showToast(`缓存是否为空：${blEmpty}`);
            })
          Button("clear()")
            .btnStyle()
            .onClick(() => {
              CacheUtil.clear();
              ToastUtil.showToast(`清除缓存数据成功`);
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
   

