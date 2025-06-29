# harmony-utils之StrUtil，字符串工具类

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

##### isNull  判断字符串是否为空(undefined、null)

```
let str0 = '哈哈哈哈';
let str1 = '';
let str2 = null;
let str3 = undefined;
let bl0 = StrUtil.isNull(str0);
let bl1 = StrUtil.isNull(str1);
let bl2 = StrUtil.isNull(str2);
let bl3 = StrUtil.isNull(str3);
```

##### isNotNull  判断字符串是否为非空(undefined、null)

```
let str0 = '哈哈哈哈';
let str1 = '';
let str2 = null;
let str3 = undefined;
let bn0 = StrUtil.isNotNull(str0);
let bn1 = StrUtil.isNotNull(str1);
let bn2 = StrUtil.isNotNull(str2);
let bn3 = StrUtil.isNotNull(str3);
```

##### isEmpty  判断字符串是否为空(undefined、null、字符串长度为0)

```
let str0 = '哈哈哈哈';
let str1 = '';
let str2 = null;
let str3 = undefined;
let bl0 = StrUtil.isEmpty(str0);
let bl1 = StrUtil.isEmpty(str1);
let bl2 = StrUtil.isEmpty(str2);
let bl3 = StrUtil.isEmpty(str3);
```

##### isNotEmpty  判断字符串是否为非空(undefined、null、字符串长度为0)

```
let str0 = '哈哈哈哈';
let str1 = '';
let str2 = null;
let str3 = undefined;
let bn0 = StrUtil.isNotEmpty(str0);
let bn1 = StrUtil.isNotEmpty(str1);
let bn2 = StrUtil.isNotEmpty(str2);
let bn3 = StrUtil.isNotEmpty(str3);
```

##### isBlank  判断字符串是否为空和空白符(空白符包括空格、制表符、全角空格和不间断空格)

```
let str0 = '\t\n  ';
let str1 = '      ';
let str2 = " \t \t ";
let str3 = " 哈 哈 ";
let bl0 = StrUtil.isBlank(str0);
let bl1 = StrUtil.isBlank(str1);
let bl2 = StrUtil.isBlank(str2);
let bl3 = StrUtil.isBlank(str3);
```

##### isNotBlank  判断字符串是否为非空

```
let str0 = '\t\n  ';
let str1 = '      ';
let str2 = " \t \t ";
let str3 = " 哈 哈 ";
let bn0 = StrUtil.isNotBlank(str0);
let bn1 = StrUtil.isNotBlank(str1);
let bn2 = StrUtil.isNotBlank(str2);
let bn3 = StrUtil.isNotBlank(str3);
```

##### trim  去除字符串两端的空格

```
let str1 = " 　 H e llo  　 World \t ";
let str2 = "   呵呵\n嘿\t嘿   哈哈 ";
let trimStr1 = StrUtil.trim(str1);
let trimStr2 = StrUtil.trim(str2);
```

##### trimAll  去除字符串里的所有空格

```
let str1 = " 　 H e llo  　 World \t ";
let str2 = "   呵呵\n嘿\t嘿   哈哈 ";
let trimStr1 = StrUtil.trimAll(str1);
let trimStr2 = StrUtil.trimAll(str2);
```

##### replace  替换字符串中匹配的正则为给定的字符串

```
let str1 = "阿超是一个好人,小阿超也是一个好人";
let str = StrUtil.replace(str1, "阿超", "张三");
```

##### replaceAll  替换字符串中所有匹配的正则为给定的字符串

```
let str1 = "阿超是一个好人,小阿超也是一个好人";
let strAll = StrUtil.replaceAll(str1, "好人", " HAO-REN ");
```

##### startsWith  判断字符串是否以给定的字符串开头

```
let str1 = "大聪明是一个好人,DSB也是一个好人";
let startsWith = StrUtil.startsWith(str1, "大聪明");
```

##### endsWith  判断字符串是否以给定的字符串结尾

```
let str1 = "大聪明是一个好人,DSB也是一个好人";
let endsWith = StrUtil.endsWith(str1, "好人");
```

##### repeat  将字符串重复指定次数

```
let str2 = "千秋万代";
let strs = StrUtil.repeat(str2, 6);
```

##### toLower  将整个字符串转换为小写

```
let str = "anima,For generations to come, Forever Immortal,IT is SB";
let str1 = StrUtil.toLower(str);
```

##### toUpper  将整个字符串转换为大写

```
let str = "anima,For generations to come, Forever Immortal,IT is SB";
let str2 = StrUtil.toUpper(str);
```

##### capitalize  将字符串首字母转换为大写，剩下为小写

```
let str = "anima,For generations to come, Forever Immortal,IT is SB";
let str3 = StrUtil.capitalize(str);
```

##### equal  判断两个传入的数值或者是字符串是否相等

```
let bl1 = StrUtil.equal("ASX1", "ASX1");
let bl2 = StrUtil.equal("ASX1", "AS1");
let bl4 = StrUtil.equal(26, 26);
let bl5 = StrUtil.equal(26, 29);
```

##### notEqual  判断两个传入的数值或者是字符串是否不相等

```
let bl3 = StrUtil.notEqual("AS1", "ASX1");
let bl6 = StrUtil.notEqual(22, 32);
```

##### strToUint8Array  字符串转Uint8Array

```
let str1 = "我是笑哈哈";
let unit8Array = StrUtil.strToUint8Array(str1);
```

##### unit8ArrayToStr  Uint8Array转字符串

```
let str1 = "我是笑哈哈";
let unit8Array = StrUtil.strToUint8Array(str1);
let str = StrUtil.unit8ArrayToStr(unit8Array);
```

##### strToBase64  字符串转Base64字符串

```
let str1 = "我是笑面虎";
let base64Str = StrUtil.strToBase64(str1);
```

##### base64ToStr  Base64字符串转字符串

```
let str1 = "我是笑面虎";
let base64Str = StrUtil.strToBase64(str1);
let str = StrUtil.base64ToStr(base64Str);
```

##### strToBuffer  字符串转ArrayBuffer

```
let str1 = "我是乐哈哈";
let buff = StrUtil.strToBuffer(str1);
```

##### bufferToStr  ArrayBuffer转字符串

```
let str1 = "我是乐哈哈";
let buff = StrUtil.strToBuffer(str1);
let str = StrUtil.bufferToStr(buff);
```

##### bufferToUint8Array  ArrayBuffer转Uint8Array

```
let str1 = "我是甜啦啦";
let buff1 = StrUtil.strToBuffer(str1);
let unit8Array = StrUtil.bufferToUint8Array(buff1);
```

##### unit8ArrayToBuffer  Uint8Array转ArrayBuffer

```
let str1 = "我是甜啦啦";
let buff1 = StrUtil.strToBuffer(str1);
let unit8Array = StrUtil.bufferToUint8Array(buff1);
let buff = StrUtil.unit8ArrayToBuffer(unit8Array);
```

##### getErrorStr  获取Error的JSON字符串

```
let error = new Error("未知异常！");
let errorStr = StrUtil.getErrorStr(error as BusinessError);
```

##### getErrnoToString  获取系统错误码对应的详细信息

```
let errStr1 = StrUtil.getErrnoToString(202);
let errStr2 = StrUtil.getErrnoToString(1600004);
```

## 创作不易，请给童长老点赞👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   

