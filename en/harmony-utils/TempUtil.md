# Harmony-utils: TempUtil, temperature conversion tool class

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

##### C2F degrees Celsius to Fahrenheit

```
let f = TempUtil.C2F(27.5);
ToastUtil.showToast(`转换后的华氏度：${f}`);
```

##### F2C Fahrenheit to Celsius

```
let c = TempUtil.F2C(81.5)
ToastUtil.showToast(`转换后的摄氏度：${c}`);
```

##### C2K degrees Celsius to Kelvin

```
let k = TempUtil.C2K(25);
ToastUtil.showToast(`转换后的开尔文：${k}`);
```

##### Kelvin to Celsius

```
let c = TempUtil.K2C(298.15);
ToastUtil.showToast(`转换后的摄氏度：${c}`);
```

##### F2K Fahrenheit to Kelvin

```
let k = TempUtil.F2K(77);
ToastUtil.showToast(`转换后的开尔文：${k}`);
```

##### K2F Kelvin to Fahrenheit

```
let f = TempUtil.K2F(298.15);
ToastUtil.showToast(`转换后的华氏度：${f}`);
```

## Creation is not easy, please give Elder Tong a thumbs up 👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   

