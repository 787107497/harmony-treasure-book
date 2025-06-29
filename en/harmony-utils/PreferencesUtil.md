# PreferencesUtils, PreferencesUtil, Preferences Tool Class

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

##### init initialization

```
 PreferencesUtil.init("my_app_preferences");
```

##### put caches data

```
PreferencesUtil.put("id", 10000018);
PreferencesUtil.putSync("name", "张三叁");
PreferencesUtil.putSync("bl_nuv", false);
```

##### get get cached value

```
 let id = await PreferencesUtil.get("id", "");
```

##### getString Gets the cached value of type string

```
let name1 = await PreferencesUtil.getString("name");
let name2 = PreferencesUtil.getStringSync('name');
```

##### getNumber Gets the cached value of type number

```
let id1 = await PreferencesUtil.getNumber("id");
let id2 = PreferencesUtil.getNumberSync('id');
```

##### getBoolean Gets the cached value of boolean type

```
let bl1 = await PreferencesUtil.getBoolean("bl_nut");
let bl2 = PreferencesUtil.getBooleanSync('bl_nuv');
```

##### has Check whether the cache instance contains the stored key-value pair of the given key

```
let bl1 = await PreferencesUtil.has("id");
let bl2 = PreferencesUtil.hasSync('name');
```

##### delete delete cached value

```
PreferencesUtil.delete("id");
PreferencesUtil.deleteSync("name");
```

##### clear clear cache

```
PreferencesUtil.clear();
PreferencesUtil.clearSync();
```

##### deletePreferences Removes the specified Preferences instance from the cache. If the Preferences instance has a corresponding persistent file, its persistent file will be deleted at the same time.

```
 PreferencesUtil.deletePreferences(getContext(), "SP_PREFERENCES_MSG");
```

##### onChange Subscribe to data change. After the value of the subscribed Key is changed, the callback callback is triggered after the flush method is executed.

```
  private callback: Callback<string> = (value) => {
    LogUtil.error("onChange: " + value);
  }
  
 PreferencesUtil.onChange(callback);
```

##### offChange Unsubscribe to data changes

```
 PreferencesUtil.offChange(callback);
```

##### onDataChange precisely subscribes to data changes. Only after the subscribed key value changes, the callback callback is triggered after the flush method is executed.

```
  private dataCallback = (data: Record<string, preferences.ValueType>) => {
    for (const keyValue of Object.entries(data)) {
      LogUtil.error("onDataChange: " + keyValue);
    }
  }
  
  PreferencesUtil.onDataChange(["id", "name"], dataCallback);
```

##### offDataChange Cancel the exact subscription data change

```
PreferencesUtil.offDataChange(["id", "name"], dataCallback);
```

## Creation is not easy, please give Elder Tong a thumbs up 👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   



