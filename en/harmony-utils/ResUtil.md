# ResUtils of harmony-utils, resource-related tool class

## Introduction and description of harmony-utils

------
[harmony-utils](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)A HarmonyOS tool library with rich features and extremely easy to use, with the help of many practical tools, is committed to helping developers quickly build Hongmeng applications. Its encapsulated tools cover APP, device, screen, authorization, notification, inter-thread communication, pop-up frames, toast, biometric authentication, user preferences, taking photos, albums, scanning codes, files, logs, exception capture, characters, strings, numbers, collections, dates, random, base64, encryption, decryption, JSON and other functions, which can meet various development needs.
[picker_utils](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fpicker_utils)It is a sub-store split by harmony-utils, including PickerUtil, PhotoHelper, and ScanUtil.

Download and install
`ohpm i @pura/harmony-utils`  
`ohpm i @pura/picker_utils`

 ```
  //全局初始化方法，在UIAbility的onCreate方法中初始化 AppUtil.init()a
  onCreate(want: Want, launchParam: AbilityConstant.LaunchParam): void {
    AppUtil.init(this.context);
  }
 ```

## API methods and usage

------

##### getResourceManager gets the ability to provide access to application resources

```
let resourceManager = ResUtil.getResourceManager();
```

##### getBoolean Gets the boolean result corresponding to the specified resource

```
let b1 = ResUtil.getBoolean($r('app.boolean.bl_debug'));
let b2 = ResUtil.getBoolean($r('app.boolean.bl_debug').id);
```

##### getBooleanByName Gets the boolean result corresponding to the specified resource name

```
 let b4 = ResUtil.getBooleanByName('bl_agree');
```

##### getNumber Gets the integer value or float value corresponding to the specified resource

```
let num1 = ResUtil.getNumber($r('app.integer.count'));
let num2 = ResUtil.getNumber($r('app.integer.age').id);
```

##### getNumberByName Gets the integer value or float value corresponding to the specified resource name

```
let num3 = ResUtil.getNumberByName('count');
```

##### getStringValue Gets the string corresponding to the specified resource

```
let str3 = await ResUtil.getStringValue($r('app.string.app_name'));
```

##### getStringSync Gets the string corresponding to the specified resource name

```
let str1 = ResUtil.getStringSync($r('app.string.str_desc'));
let str2 = ResUtil.getStringSync($r('app.string.module_desc').id);
```

##### getStringByName Gets the string corresponding to the specified resource name

```
let str5 = ResUtil.getStringByNameSync('module_desc');
let str6 = await ResUtil.getStringByName('app_name');
```

##### getStringArrayValue Gets the string array corresponding to the specified resource

```
let strArray1 = ResUtil.getStringArrayValueSync($r('app.strarray.font_size'));
let strArray2 = await ResUtil.getStringArrayValue($r('app.strarray.font_size').id);
```

##### getStringArrayByName Gets the string array corresponding to the specified resource name

```
let strArray3 = ResUtil.getStringArrayByNameSync("font_size");
let strArray4 = await ResUtil.getStringArrayByName("font_size");
```

##### getPluralStringValue Gets a single-plural numeric string represented by the specified resource object based on the specified number

```
let str1 = ResUtil.getPluralStringValueSync($r('app.plural.eat_apple'), 1);
let str2 = await ResUtil.getPluralStringValue($r('app.plural.eat_apple'), 2);
```

##### getPluralStringByName Gets a single-plural string represented by the specified resource name based on the specified number

```
let str3 = ResUtil.getPluralStringByNameSync("eat_apple", 11);
let str4 = await ResUtil.getPluralStringByName("eat_apple", 0);
```

##### getColor Gets the color value corresponding to the specified resource (decimal)

```
let color1 = ResUtil.getColorSync($r('app.color.color_main'));
let color2 = await ResUtil.getColor($r('app.color.color_99'));
```

##### getColorByName Gets the color value corresponding to the specified resource name (decimal)

```
let color3 = ResUtil.getColorByNameSync("color_main");
let color4 = await ResUtil.getColorByName("color_99");
```

##### getMediaContent Gets the default or specified screen density media file content for the specified resource

```
let uint8Array1 = ResUtil.getMediaContentSync($r('app.media.test_as1'));
let uint8Array2 = await ResUtil.getMediaContent($r('app.media.test_as4'));
```

##### getMediaByName Gets the default or specified screen density media file content corresponding to the specified resource name

```
let uint8Array3 = ResUtil.getMediaByNameSync("test_as2");
let uint8Array4 = await ResUtil.getMediaByName("test_as5");
```

##### getMediaContentBase64 Get the default or specified screen density picture resource Base64 encoding corresponding to the specified resource ID

```
let str1 = ResUtil.getMediaContentBase64Sync($r('app.media.test_as1'));
let str2 = await ResUtil.getMediaContentBase64($r('app.media.test_as4'));
```

##### getMediaBase64ByName Gets the default or specified screen density picture resource Base64 encoding corresponding to the specified resource name

```
let str3 = ResUtil.getMediaBase64ByNameSync("test_as2");
let str4 = await ResUtil.getMediaBase64ByName("test_as5");
```

##### getRawFileContent Get the content of the corresponding rawfile file in the resources/rawfile directory

```
let uint8Array1 = ResUtil.getRawFileContentSync('demo/demo.txt');
let uint8Array2 = await ResUtil.getRawFileContent('data_utils.json');
```

##### getRawFileContentStr Gets the content of the corresponding rawfile file in the resources/rawfile directory (string)

```
let str3 = ResUtil.getRawFileContentStrSync("demo/demo.txt");
let str4 = await ResUtil.getRawFileContentStr("demo/test.txt");
```

##### getRawFileList Gets the folder and file list in the resources/rawfile directory (if there is no file in the folder, it will not be returned; if there is a file in the folder, it will return the folder and file list)

```
let list1 = ResUtil.getRawFileListSync('demo');
let list2 = await ResUtil.getRawFileList("");
```

##### getRawFd user obtains the descriptor information of the corresponding rawfile file in the resources/rawfile directory

```
 let rawFileDescriptor = await ResUtil.getRawFd("test.txt");
```

##### closeRawFd User closes the descriptor information of the rawfile file in the resources/rawfile directory

```
ResUtil.closeRawFd("test.txt");
```

##### addResource When the application is running, the specified resource path is loaded to achieve resource coverage

```
let path = AppUtil.getContext().bundleCodeDir + "/library-default-signed.hsp";
ResUtil.addResource(path);
```

##### When the removeResource user runs, removes the specified resource path and restores the resource before being overwritten.

```
let path = AppUtil.getContext().bundleCodeDir + "/library-default-signed.hsp";
ResUtil.removeResource(path);
```

##### isRawDir User determines whether the specified path is a directory under rawfile (true: means it is a directory under rawfile, false: means it is not a directory under rawfile)

```
let isRawDir = ResUtil.isRawDir("demo");
let isRawDir2 = ResUtil.isRawDir("test.txt");
```

##### getConfiguration Gets the configuration of the device

```
 let configuration = ResUtil.getConfigurationSync();
```

##### getDeviceCapability Get the DeviceCapability of the device

```
let deviceCapability = ResUtil.getDeviceCapabilitySync();
```

## Creation is not easy, please give Elder Tong a thumbs up 👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   



