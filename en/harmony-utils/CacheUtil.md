# CacheUtil, caching tool class

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

##### has Whether the data in the cache exists

```
  let pwd = CacheUtil.has("pwd");
  ToastUtil.showToast(`缓存是否存在：${pwd}`);
```

##### put Save data into cache

```
 CacheUtil.put("pwd", "ABCD@12345");
 ToastUtil.showToast("缓存密码成功");
```

##### get get the cached data

```
 let pwd = CacheUtil.get<string>("pwd");
 ToastUtil.showToast(`取值：${pwd}`);
```

##### remove delete the cache corresponding to the key

```
 CacheUtil.remove("pwd");
 ToastUtil.showToast(`缓存移除成功！`);
```

##### isEmpty determines whether the cache is empty

```
 let blEmpty = CacheUtil.isEmpty();
 ToastUtil.showToast(`缓存是否为空：${blEmpty}`);
```

##### clear clear cached data

```
 CacheUtil.clear();
 ToastUtil.showToast(`清除缓存数据成功`);
```

## Creation is not easy, please give Elder Tong a thumbs up 👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   

