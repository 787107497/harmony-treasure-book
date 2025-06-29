# ToastUtils, toast tool class

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

##### setDefaultConfig Set the default uniform style

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

##### showToast pops up toast, the default duration is 2s

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

##### showShort pops up short toast, the default duration is: 1.5s

```
ToastUtil.showShort("弹出短土司，时长为:1.5s");
```

##### showLong pops up long toast, default duration is: 10s

```
ToastUtil.showLong("弹出短土司，时长为:10s");
```

## Creation is not easy, please give Elder Tong a thumbs up 👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   

