# AssetUtil, a key asset storage service tool class

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

## Introduction and Explanation

------

The asset store service (ASSET) provides secure storage and management of sensitive data less than 1024 bytes in size, including passwords, app tokens, and other critical data (such as bank card numbers).    
AssetUtil is a utility class based on the Asset Store Kit encapsulation, which can be used for secure storage of users' short sensitive data, such as accounts, passwords, etc Token、 Device ID, etc.


## API methods and usage

------

##### canIUse Whether the current device supports this module

```
let canIUse = AssetUtil.canIUse();
ToastUtil.showToast(`当前设备是否支持该模块：${canIUse}`);
```

##### add a new key asset

```
AssetUtil.add("key_harmony", "我是异步知产X!").then(() => {
  ToastUtil.showToast(`新增资产成功！`);
});

AssetUtil.addSync("key_harmony_sync", "我是同步知产X!");
ToastUtil.showToast(`新增资产成功！`);
```

##### get query key assets

```
let rStr = await AssetUtil.get("key_harmony");
ToastUtil.showToast(`取值: ${rStr}`);

let sStr = AssetUtil.getSync("key_harmony_sync");
ToastUtil.showToast(`同步：${sStr}`);
```

##### remove key assets

```
AssetUtil.remove("key_harmony").then(() => {
  ToastUtil.showToast("移除成功！");
});

AssetUtil.removeSync("key_harmony_sync");
ToastUtil.showToast("移除成功!");
```


## Full Code Example

------

```
import { router } from '@kit.ArkUI';
import { DescribeBean } from '../../model/DescribeBean';
import { MockSetup } from '@ohos/hamock';
import { AssetUtil, LogUtil, ToastUtil } from '@pura/harmony-utils';
import { TitleBarView } from '../../component/TitleBarView';

/**
 * 关键资产存储服务工具类
 */
@Entry
@Component
struct Index {
  private scroller: Scroller = new Scroller();
  @State describe: DescribeBean = router.getParams() as DescribeBean;
  @State readonly rkey: string = "key_harmony"
  @State readonly skey: string = "key_harmony_sync"

  @MockSetup
  mock() {
    this.describe = new DescribeBean("AssetUtil", "关键资产存储服务工具类");
  }

  build() {
    Column() {
      TitleBarView({ describe: this.describe })
      Divider()
      Scroll(this.scroller) {
        Column() {
          Button("canIUse")
            .btnStyle()
            .onClick(() => {
              let canIUse = AssetUtil.canIUse();
              ToastUtil.showToast(`当前设备是否支持该模块：${canIUse}`);
            })
          Button("add")
            .btnStyle()
            .onClick(() => {
              AssetUtil.add(this.rkey, "我是异步知产X!").then(() => {
                ToastUtil.showToast(`新增资产成功！`);
              });
            })
          Button("get")
            .btnStyle()
            .onClick(async () => {
              let rStr = await AssetUtil.get(this.rkey);
              ToastUtil.showToast(`取值: ${rStr}`);
              LogUtil.error(`取值: ${rStr}`);
            })
          Button("addSync")
            .btnStyle()
            .onClick(() => {
              AssetUtil.addSync(this.skey, "我是同步知产X!");
              ToastUtil.showToast(`新增资产成功！`);
            })
          Button("getSync")
            .btnStyle()
            .onClick(() => {
              let sStr = AssetUtil.getSync(this.skey);
              ToastUtil.showToast(`同步：${sStr}`);
            })
          Button("remove")
            .btnStyle()
            .onClick(() => {
              AssetUtil.remove(this.rkey).then(() => {
                ToastUtil.showToast("移除成功！");
              });
            })
          Button("removeSync")
            .btnStyle()
            .onClick(() => {
              AssetUtil.removeSync(this.skey);
              ToastUtil.showToast("移除成功!");
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


## Creation is not easy, please give Elder Tong a thumbs up 👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   

