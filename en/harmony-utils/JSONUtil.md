# Harmony-utils JSONUtil, JSON tool class

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

##### jsonToBean JSON string to object

```
let objStr: string = '{"id":"No_1060701","name":"张三","age":20,"addr":"乌市天山区","work":"工程师","salary":9223372036854775807.2512,"user":{"id":"No_1060701","name":"张三","age":20,"addr":"乌市天山区","work":"工程师"}}';
let user = JSONUtil.jsonToBean(objStr, User);
```

##### beanToJsonStr object to JSON string

```
let user: User = new User();
let str = JSONUtil.beanToJsonStr(user);
```

##### jsonToArray JSON string to Array

```
let arrayStr = ResUtil.getRawFileContentStrSync('data_utils.json');
let array = JSONUtil.jsonToArray<DescribeBean>(this.arrayStr);
array.forEach((item, index) => {
  LogUtil.error(`${index} - ${JSON.stringify(item)}`);
});
```

##### jsonToMap JSON string to Map

```
let mapStr: string = '{"id":"NO_10000011","name":"王五五","age":"30","addr":"乌市天山区","work":"攻城狮","salary":9223372036854775807.2512}';
let map = JSONUtil.jsonToMap(mapStr);
map.forEach((value, key) => {
  LogUtil.error(`${key} - ${value}`);
});
```

##### mapToJsonStr Map to JSON string

```
let mapStr: string = '{"id":"NO_10000011","name":"王五五","age":"30","addr":"乌市天山区","work":"攻城狮","salary":9223372036854775807.2512}';
let map = JSONUtil.jsonToMap(mapStr);
```

##### isJSONStr determines whether it is in string format json

```
let objStr: string = '{"id":"No_1060701","name":"张三","age":20,"addr":"乌市天山区","work":"工程师","salary":9223372036854775807.2512,"user":{"id":"No_1060701","name":"张三","age":20,"addr":"乌市天山区","work":"工程师"}}';
let b1 = JSONUtil.isJSONStr(objStr);
let b2 = JSONUtil.isJSONStr("abcd1234");
```

## Creation is not easy, please give Elder Tong a thumbs up 👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   