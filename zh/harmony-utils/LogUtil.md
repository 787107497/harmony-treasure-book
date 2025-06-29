# harmony-utils之LogUtil，日志工具类

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

##### init   初始化日志参数（该方法建议在Ability里调用

```
 LogUtil.init(0x1010, 'Pura', true, true);  //该方法建议在Ability里调用
```

##### setShowLog  是否打印日志（该方法建议在Ability里调用）

```
LogUtil.setShowLog(true);  //该方法建议在Ability里调用
```

##### setDomain  设置日志对应的领域标识，范围是0x0~0xFFFF。（该方法建议在Ability里调用）

```
LogUtil.setDomain(0x0010);  //该方法建议在Ability里调用
```

##### setTag  设置日志标识（该方法建议在Ability里调用）

```
LogUtil.setTag("童长老"); //该方法建议在Ability里调用
```

##### setHilog  日志打印方式（该方法建议在Ability里调用）

```
 LogUtil.setHilog(true);  //该方法建议在Ability里调用
```

##### debug  打印DEBUG级别日志

```
LogUtil.debug("我是一个debug日志-日志工具类-*…^·^…*-哈哈哈哈哈哈!");
```

##### info  打印INFO级别日志

```
LogUtil.info("我是一个info日志-*￥…^·^…￥*—我是一个日志。");
```

##### warn  打印WARN级别日志

```
LogUtil.warn("我是一个warn日志\t", "日志工具类^·^…￥…&!。");
```

##### error  打印ERROR级别日志

```
LogUtil.error("我是一个error日志\t", "我是一个日志工具类-·-。", "你是谁？", "我在哪？", "嘿嘿嘿嘿嘿嘿嘿嘿！");
```

##### fatal  打印FATAL级别日志

```
LogUtil.fatal("我是一个fatal日志^·^\t", "我是一个日志工具类^·^。");
```

##### print  打印日志，无边框。

```
LogUtil.print("打印日志，无边框。harmony-utils之LogUtil，日志工具类。");
```

## 创作不易，请给童长老点赞👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   




