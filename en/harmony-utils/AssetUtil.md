# AssetUtil, a key asset storage service tool class

## Introduction and description of harmony-utils

------
[harmony-utils](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)A HarmonyOS tool library with rich features and extremely easy to use, with the help of many practical tools, is committed to helping developers quickly build Hongmeng applications. Its encapsulated tools cover APP, device, screen, authorization, notification, inter-thread communication, pop-up frames, toast, biometric authentication, user preferences, taking photos, albums, scanning codes, files, logs, exception capture, characters, strings, numbers, collections, dates, random, base64, encryption, decryption, JSON and other functions, which can meet various development needs.   
[picker_utils](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fpicker_utils)It is a sub-store split by harmony-utils, including PickerUtil, PhotoHelper, and ScanUtil.   
[harmony-dialog](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-dialog)
An extremely simple and easy-to-use zero-invasion pop-up window, which can be easily implemented with just one line of code, and can be easily popped up no matter where you are. It covers
AlertDialog, TipsDialog, ConfirmDialog, SelectDialog, CustomContentDialog, TextInputDialog, TextAreaDialog, BottomSheetDialog, ActionSheetDialog, TextPickerDialog, DatePickerDialog, CustomDialog, BindSheet, LoadingDialog, LoadingProgress, Toast, ToastTip
Various types can meet various pop-up development needs.

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

## Creation is not easy, please give Elder Tong a thumbs up 👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   

