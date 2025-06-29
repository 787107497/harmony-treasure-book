# harmony-utils之JSONUtil，JSON工具类

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

##### jsonToBean  JSON字符串转对象

```
let objStr: string = '{"id":"No_1060701","name":"张三","age":20,"addr":"乌市天山区","work":"工程师","salary":9223372036854775807.2512,"user":{"id":"No_1060701","name":"张三","age":20,"addr":"乌市天山区","work":"工程师"}}';
let user = JSONUtil.jsonToBean(objStr, User);
```

##### beanToJsonStr  对象转JSON字符串

```
let user: User = new User();
let str = JSONUtil.beanToJsonStr(user);
```

##### jsonToArray  JSON字符串转Array

```
let arrayStr = ResUtil.getRawFileContentStrSync('data_utils.json');
let array = JSONUtil.jsonToArray<DescribeBean>(this.arrayStr);
array.forEach((item, index) => {
  LogUtil.error(`${index} - ${JSON.stringify(item)}`);
});
```

##### jsonToMap  JSON字符串转Map

```
let mapStr: string = '{"id":"NO_10000011","name":"王五五","age":"30","addr":"乌市天山区","work":"攻城狮","salary":9223372036854775807.2512}';
let map = JSONUtil.jsonToMap(mapStr);
map.forEach((value, key) => {
  LogUtil.error(`${key} - ${value}`);
});
```

##### mapToJsonStr  Map转JSON字符串

```
let mapStr: string = '{"id":"NO_10000011","name":"王五五","age":"30","addr":"乌市天山区","work":"攻城狮","salary":9223372036854775807.2512}';
let map = JSONUtil.jsonToMap(mapStr);
```

##### isJSONStr  判断是否是字符串格式json

```
let objStr: string = '{"id":"No_1060701","name":"张三","age":20,"addr":"乌市天山区","work":"工程师","salary":9223372036854775807.2512,"user":{"id":"No_1060701","name":"张三","age":20,"addr":"乌市天山区","work":"工程师"}}';
let b1 = JSONUtil.isJSONStr(objStr);
let b2 = JSONUtil.isJSONStr("abcd1234");
```

## 创作不易，请给童长老点赞👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   