# harmony-utils之PreferencesUtil，首选项工具类

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

##### init  初始化

```
 PreferencesUtil.init("my_app_preferences");
```

##### put  将数据缓存

```
PreferencesUtil.put("id", 10000018);
PreferencesUtil.putSync("name", "张三叁");
PreferencesUtil.putSync("bl_nuv", false);
```

##### get  获取缓存值

```
 let id = await PreferencesUtil.get("id", "");
```

##### getString  获取string类型的缓存值

```
let name1 = await PreferencesUtil.getString("name");
let name2 = PreferencesUtil.getStringSync('name');
```

##### getNumber  获取number类型的缓存值

```
let id1 = await PreferencesUtil.getNumber("id");
let id2 = PreferencesUtil.getNumberSync('id');
```

##### getBoolean  获取boolean类型的缓存值

```
let bl1 = await PreferencesUtil.getBoolean("bl_nut");
let bl2 = PreferencesUtil.getBooleanSync('bl_nuv');
```

##### has  检查缓存实例中是否包含给定Key的存储键值对

```
let bl1 = await PreferencesUtil.has("id");
let bl2 = PreferencesUtil.hasSync('name');
```

##### delete  删除缓存值

```
PreferencesUtil.delete("id");
PreferencesUtil.deleteSync("name");
```

##### clear  清空缓存

```
PreferencesUtil.clear();
PreferencesUtil.clearSync();
```

##### deletePreferences  从缓存中移出指定的Preferences实例，若Preferences实例有对应的持久化文件，则同时删除其持久化文件。

```
 PreferencesUtil.deletePreferences(getContext(), "SP_PREFERENCES_MSG");
```

##### onChange  订阅数据变更，订阅的Key的值发生变更后，在执行flush方法后，触发callback回调

```
  private callback: Callback<string> = (value) => {
    LogUtil.error("onChange: " + value);
  }
  
 PreferencesUtil.onChange(callback);
```

##### offChange  取消订阅数据变更

```
 PreferencesUtil.offChange(callback);
```

##### onDataChange  精确订阅数据变更，只有被订阅的key值发生变更后，在执行flush方法后，触发callback回调

```
  private dataCallback = (data: Record<string, preferences.ValueType>) => {
    for (const keyValue of Object.entries(data)) {
      LogUtil.error("onDataChange: " + keyValue);
    }
  }
  
  PreferencesUtil.onDataChange(["id", "name"], dataCallback);
```

##### offDataChange  取消精确订阅数据变更

```
PreferencesUtil.offDataChange(["id", "name"], dataCallback);
```

## 创作不易，请给童长老点赞👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   



