# harmony-utils: FormatUtil, formatting tool class

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

##### isPhone determines whether the incoming phone number format is correct

```
let phone: string = "19869062586";
let bl = FormatUtil.isPhone(phone);
```

##### getPhoneFormat formats phone numbers

```
let phone: string = "19869062586";
let format = FormatUtil.getPhoneFormat(phone);
```

##### getPhoneLocationName Get the phone number home location

```
let phone: string = "19869062586";
let locationName = FormatUtil.getPhoneLocationName(phone);
```

##### Transliterator converts the input string from the source format to the target format (Chinese characters to pinyin)

```
let str = FormatUtil.transliterator("中国");
```

##### getFormatPercentage Format percentage, convert numbers from percentage strings

```
let percentage = FormatUtil.getFormatPercentage(0.491);
LogUtil.error(`percentage: ${percentage}`);
```

##### getFormatPhone formats the phone number and hides the middle four digits

```
let phone: string = "18969062528";
let str = FormatUtil.getFormatPhone(phone);
```

##### getFormatCardNo Format ID number, hide the middle part of the number

```
let str = FormatUtil.getFormatCardNo("110101199001011234");
LogUtil.error(`格式化后的身份证号: ${str}`);
```

##### getFormatFileSize format file size

```
let str = FormatUtil.getFormatFileSize(1024102400);
LogUtil.error(`文件大小: ${str}`);
```

##### getTruncateText shortens the long text, and the excess is represented by an ellipsis

```
let str = FormatUtil.getTruncateText("女人什么年龄是最好？任何年龄都可以。因为每个年龄段都有不一样的美。看XX的穿搭你就会发现成熟女性的魅力，反而会更加的吸引人。", 20);
LogUtil.error(`缩短长文本: ${str}`);
```

##### getIconFont parses iconFont characters

```
let str = FormatUtil.getIconFont("e631");
LogUtil.error(`getIconFont: ${str}`);
```

##### getQueryValue Gets the parameters in the url, and the value corresponding to the Key is

```
let url = "https://blog.csdn.net/article?spm=blog1024&name=李斯";
let value1 = FormatUtil.getQueryValue(url, 'spm');
let value2 = FormatUtil.getQueryValue(url, 'name');
let value3 = FormatUtil.getQueryValue(url, 'mona');
```

##### getParamsUrl splice parameters on the url and return the new url

```
let map = new Map<string, Any>();
map.set("id", 100011);
map.set("name", '王五');
map.set("sex", undefined);
let url1 = FormatUtil.getParamsUrl("https://blog.csdn.net?id=100012", map);

let obj: Record<string, Object> = {};
obj['key'] = 'show';
obj['user'] = '王五';
obj['pd'] = 0;
obj['type'] = 'csaitab';
let url2 = FormatUtil.getParamsUrl("https://blog.csdn.net?id=100012", obj);
```

## Creation is not easy, please give Elder Tong a thumbs up 👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   

