# harmony-utils之ResUtil，资源相关工具类

## harmony-utils 简介与说明

------
[harmony-utils](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils) 一款功能丰富且极易上手的HarmonyOS工具库，借助众多实用工具类，致力于助力开发者迅速构建鸿蒙应用。其封装的工具涵盖了APP、设备、屏幕、授权、通知、线程间通信、弹框、吐司、生物认证、用户首选项、拍照、相册、扫码、文件、日志，异常捕获、字符、字符串、数字、集合、日期、随机、base64、加密、解密、JSON等一系列的功能和操作，能够满足各种不同的开发需求。    
[picker_utils](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fpicker_utils) 是harmony-utils拆分出来的一个子库，包含PickerUtil、PhotoHelper、ScanUtil。

下载安装  
`ohpm i @pura/harmony-utils`  
`ohpm i @pura/picker_utils`

 ```
  //全局初始化方法，在UIAbility的onCreate方法中初始化 AppUtil.init()a
  onCreate(want: Want, launchParam: AbilityConstant.LaunchParam): void {
    AppUtil.init(this.context);
  }
 ```

## API方法与使用

------

##### getResourceManager  获取提供访问应用资源的能力

```
let resourceManager = ResUtil.getResourceManager();
```

##### getBoolean  获取指定资源对应的布尔结果

```
let b1 = ResUtil.getBoolean($r('app.boolean.bl_debug'));
let b2 = ResUtil.getBoolean($r('app.boolean.bl_debug').id);
```

##### getBooleanByName  获取指定资源名称对应的布尔结果

```
 let b4 = ResUtil.getBooleanByName('bl_agree');
```

##### getNumber  获取指定资源对应的integer数值或者float数值

```
let num1 = ResUtil.getNumber($r('app.integer.count'));
let num2 = ResUtil.getNumber($r('app.integer.age').id);
```

##### getNumberByName  获取指定资源名称对应的integer数值或者float数值

```
let num3 = ResUtil.getNumberByName('count');
```

##### getStringValue  获取指定资源对应的字符串

```
let str3 = await ResUtil.getStringValue($r('app.string.app_name'));
```

##### getStringSync  获取指定资源名称对应的字符串

```
let str1 = ResUtil.getStringSync($r('app.string.str_desc'));
let str2 = ResUtil.getStringSync($r('app.string.module_desc').id);
```

##### getStringByName  获取指定资源名称对应的字符串

```
let str5 = ResUtil.getStringByNameSync('module_desc');
let str6 = await ResUtil.getStringByName('app_name');
```

##### getStringArrayValue  获取指定资源对应的字符串数组

```
let strArray1 = ResUtil.getStringArrayValueSync($r('app.strarray.font_size'));
let strArray2 = await ResUtil.getStringArrayValue($r('app.strarray.font_size').id);
```

##### getStringArrayByName  获取指定资源名称对应的字符串数组

```
let strArray3 = ResUtil.getStringArrayByNameSync("font_size");
let strArray4 = await ResUtil.getStringArrayByName("font_size");
```

##### getPluralStringValue  根据指定数量获取指定resource对象表示的单复数字符串

```
let str1 = ResUtil.getPluralStringValueSync($r('app.plural.eat_apple'), 1);
let str2 = await ResUtil.getPluralStringValue($r('app.plural.eat_apple'), 2);
```

##### getPluralStringByName  根据指定数量获取指定资源名称表示的单复数字符串

```
let str3 = ResUtil.getPluralStringByNameSync("eat_apple", 11);
let str4 = await ResUtil.getPluralStringByName("eat_apple", 0);
```

##### getColor  获取指定资源对应的颜色值（十进制）

```
let color1 = ResUtil.getColorSync($r('app.color.color_main'));
let color2 = await ResUtil.getColor($r('app.color.color_99'));
```

##### getColorByName   获取指定资源名称对应的颜色值（十进制）

```
let color3 = ResUtil.getColorByNameSync("color_main");
let color4 = await ResUtil.getColorByName("color_99");
```

##### getMediaContent  获取指定资源对应的默认或指定的屏幕密度媒体文件内容

```
let uint8Array1 = ResUtil.getMediaContentSync($r('app.media.test_as1'));
let uint8Array2 = await ResUtil.getMediaContent($r('app.media.test_as4'));
```

##### getMediaByName  获取指定资源名称对应的默认或指定的屏幕密度媒体文件内容

```
let uint8Array3 = ResUtil.getMediaByNameSync("test_as2");
let uint8Array4 = await ResUtil.getMediaByName("test_as5");
```

##### getMediaContentBase64  获取指定资源ID对应的默认或指定的屏幕密度图片资源Base64编码

```
let str1 = ResUtil.getMediaContentBase64Sync($r('app.media.test_as1'));
let str2 = await ResUtil.getMediaContentBase64($r('app.media.test_as4'));
```

##### getMediaBase64ByName  获取指定资源名称对应的默认或指定的屏幕密度图片资源Base64编码

```
let str3 = ResUtil.getMediaBase64ByNameSync("test_as2");
let str4 = await ResUtil.getMediaBase64ByName("test_as5");
```

##### getRawFileContent  获取resources/rawfile目录下对应的rawfile文件内容

```
let uint8Array1 = ResUtil.getRawFileContentSync('demo/demo.txt');
let uint8Array2 = await ResUtil.getRawFileContent('data_utils.json');
```

##### getRawFileContentStr  获取resources/rawfile目录下对应的rawfile文件内容（字符串）

```
let str3 = ResUtil.getRawFileContentStrSync("demo/demo.txt");
let str4 = await ResUtil.getRawFileContentStr("demo/test.txt");
```

##### getRawFileList  获取resources/rawfile目录下文件夹及文件列表（若文件夹中无文件，则不返回；若文件夹中有文件，则返回文件夹及文件列表）

```
let list1 = ResUtil.getRawFileListSync('demo');
let list2 = await ResUtil.getRawFileList("");
```

##### getRawFd  用户获取resources/rawfile目录下对应rawfile文件所在hap的descriptor信息

```
 let rawFileDescriptor = await ResUtil.getRawFd("test.txt");
```

##### closeRawFd  用户关闭resources/rawfile目录下rawfile文件所在hap的descriptor信息

```
ResUtil.closeRawFd("test.txt");
```

##### addResource  应用运行时，加载指定的资源路径，实现资源覆盖

```
let path = AppUtil.getContext().bundleCodeDir + "/library-default-signed.hsp";
ResUtil.addResource(path);
```

##### removeResource  用户运行时，移除指定的资源路径，还原被覆盖前的资源

```
let path = AppUtil.getContext().bundleCodeDir + "/library-default-signed.hsp";
ResUtil.removeResource(path);
```

##### isRawDir  用户判断指定路径是否是rawfile下的目录（true：表示是rawfile下的目录，false：表示不是rawfile下的目录）

```
let isRawDir = ResUtil.isRawDir("demo");
let isRawDir2 = ResUtil.isRawDir("test.txt");
```

##### getConfiguration  获取设备的Configuration

```
 let configuration = ResUtil.getConfigurationSync();
```

##### getDeviceCapability  获取设备的DeviceCapability

```
let deviceCapability = ResUtil.getDeviceCapabilitySync();
```

## 创作不易，请给童长老点赞👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   



