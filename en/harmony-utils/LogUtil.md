# LogUtil, log tool class

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

##### init initialize log parameters (this method is recommended to be called in Ability

```
 LogUtil.init(0x1010, 'Pura', true, true);  //该方法建议在Ability里调用
```

##### setShowLog prints the log (this method is recommended to be called in Ability)

```
LogUtil.setShowLog(true);  //该方法建议在Ability里调用
```

##### setDomain Sets the domain identifier corresponding to the log, the range is 0x0~0xFFFF. (This method is recommended to be called in Ability)

```
LogUtil.setDomain(0x0010);  //该方法建议在Ability里调用
```

##### setTag Set the log flag (this method is recommended to be called in Ability)

```
LogUtil.setTag("童长老"); //该方法建议在Ability里调用
```

##### setHilog log printing method (this method is recommended to be called in Ability)

```
 LogUtil.setHilog(true);  //该方法建议在Ability里调用
```

##### debug Print DEBUG level log

```
LogUtil.debug("我是一个debug日志-日志工具类-*…^·^…*-哈哈哈哈哈哈!");
```

##### info Print INFO level log

```
LogUtil.info("我是一个info日志-*￥…^·^…￥*—我是一个日志。");
```

##### warn Print WARN level log

```
LogUtil.warn("我是一个warn日志\t", "日志工具类^·^…￥…&!。");
```

##### error Print ERROR level log

```
LogUtil.error("我是一个error日志\t", "我是一个日志工具类-·-。", "你是谁？", "我在哪？", "嘿嘿嘿嘿嘿嘿嘿嘿！");
```

##### fatal prints FATAL level log

```
LogUtil.fatal("我是一个fatal日志^·^\t", "我是一个日志工具类^·^。");
```

##### print Print log without borders.

```
LogUtil.print("打印日志，无边框。harmony-utils之LogUtil，日志工具类。");
```

## Creation is not easy, please give Elder Tong a thumbs up 👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   




