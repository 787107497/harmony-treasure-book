# harmony-utils之NumberUtil，Number工具类

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

##### isNaN  检查值是否为NaN

```
let isNaN1 = NumberUtil.isNaN(112);
let isNaN2 = NumberUtil.isNaN(Number.NaN);
```

##### isFinite  检查值是否为有限数字

```
let isFinite1 = NumberUtil.isFinite(112);
let isFinite2 = NumberUtil.isFinite(Number.MAX_VALUE);
```

##### isInteger  检查值是否为整数

```
let isInteger1 = NumberUtil.isInteger(112);
let isInteger2 = NumberUtil.isInteger(11.2);
```

##### isSafeInteger  检查值是否为安全整数

```
let isSafeInteger1 = NumberUtil.isSafeInteger(-112);
let isSafeInteger2 = NumberUtil.isSafeInteger(112);
```

##### isNumber  判断是否是数值

```
let bl1 = NumberUtil.isNumber(12345);
let bl2 = NumberUtil.isNumber("12345");
let bl3 = NumberUtil.isNumber(1.212345);
let bl4 = NumberUtil.isNumber(true);
let bl5 = NumberUtil.isNumber(null);
let bl6 = NumberUtil.isNumber(undefined);
```

##### isEven 检查数字是否为偶数

```
let isEven = NumberUtil.isEven(112);
```

##### isOdd  检查数字是否为奇数

```
let isOdd = NumberUtil.isOdd(112);
```

##### toNumber  将字符串转换为Number

```
let n1 = NumberUtil.toNumber("0.12579AB");
let n2 = NumberUtil.toNumber("123456");
let n3 = NumberUtil.toNumber("128.15624");
let n4 = NumberUtil.toNumber("哈哈");
```

##### toInt  将字符串转换为整数

```
let n1 = NumberUtil.toInt("0.12579");
let n2 = NumberUtil.toInt("12345");
let n3 = NumberUtil.toInt("128.15624");
let n4 = NumberUtil.toInt("哈哈");
```

##### toFloat  将字符串转换为浮点数

```
let f1 = NumberUtil.toFloat("0.12579");
let f2 = NumberUtil.toFloat("12345");
let f3 = NumberUtil.toFloat("128.15624");
let f4 = NumberUtil.toFloat("呵呵");
```

##### average  计算数字的平均值

```
let average1 = NumberUtil.average(1, 2, 3, 4, 5, 6, 7, 8, 9);
let average2 = NumberUtil.average(...[1, 3, 5, 7, 9, 11, 13, 15, 17, 19]);
```

##### add  加法

```
let add = NumberUtil.add(112, 200);
```

##### sub  减法

```
let sub = NumberUtil.sub(200, 112);
```

##### sum  求和

```
let sum = NumberUtil.sum(10, 12, 16, 18, 36, 22);
```

##### toDecimal  构造Decimal

```
let n1 = NumberUtil.toDecimal(112).toNumber();
let n2 = NumberUtil.toDecimal("200").toNumber();
let n3 = NumberUtil.toDecimal("0200").toNumber();
let n4 = NumberUtil.toDecimal("0.20").toNumber();
let n5 = NumberUtil.toDecimal(0.2222).toNumber();
```

##### addDecimal  加法Decimal

```
let n1 = NumberUtil.addDecimal(112, 200).toNumber();
let n2 = NumberUtil.addDecimal("200", "300").toNumber();
let n3 = NumberUtil.addDecimal("200", 600).toNumber();
```

##### subDecimal  减法Decimal

```
let n1 = NumberUtil.subDecimal(112, 20).toNumber();
let n2 = NumberUtil.subDecimal("200", 100).toNumber();
let n3 = NumberUtil.subDecimal("200", 55).toNumber();
```

##### sumDecimal  求和Decimal

```
let n1 = NumberUtil.sumDecimal(1, 3, 5, 7, 9).toNumber();
let n2 = NumberUtil.sumDecimal("1", "3", "5", "7", "9").toNumber();
let n3 = NumberUtil.sumDecimal("10", 15, "25", "35", 45).toNumber();
```

## 创作不易，请给童长老点赞👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   
