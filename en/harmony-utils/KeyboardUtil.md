# Harmony-utils KeyboardUtil, keyboard tool class

## Introduction and description of harmony-utils

------
[harmony-utils](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)A HarmonyOS tool library with rich features and extremely easy to use, with the help of many practical tools, is committed to helping developers quickly build Hongmeng applications. Its encapsulated tools cover APP, device, screen, authorization, notification, inter-thread communication, pop-up frames, toast, biometric authentication, user preferences, taking photos, albums, scanning codes, files, logs, exception capture, characters, strings, numbers, collections, dates, random, base64, encryption, decryption, JSON and other functions, which can meet various development needs.
[picker_utils](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fpicker_utils)It is a sub-store split by harmony-utils, including PickerUtil, PhotoHelper, and ScanUtil.

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

##### show Pull up the keyboard

```
KeyboardUtil.show("id_input_1000");
```

##### hide hidden keyboard

```
 KeyboardUtil.hide();
```

##### onKeyboardListener Subscribe to input method soft keyboard to show and hide events

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

##### removeKeyboardListener Unsubscribe from input method soft keyboard to display or hide events

```
KeyboardUtil.removeKeyboardListener(); //移除所有
KeyboardUtil.removeKeyboardListener(callback); //移除指定
```

## Creation is not easy, please give Elder Tong a thumbs up 👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   

