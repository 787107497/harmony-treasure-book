# No. Utils, Number tool class

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

##### isNaN Check whether the value is NaN

```
let isNaN1 = NumberUtil.isNaN(112);
let isNaN2 = NumberUtil.isNaN(Number.NaN);
```

##### isFinite Check whether the value is a finite number

```
let isFinite1 = NumberUtil.isFinite(112);
let isFinite2 = NumberUtil.isFinite(Number.MAX_VALUE);
```

##### isInteger Checks whether the value is an integer

```
let isInteger1 = NumberUtil.isInteger(112);
let isInteger2 = NumberUtil.isInteger(11.2);
```

##### isSafeInteger Checks whether the value is a safe integer

```
let isSafeInteger1 = NumberUtil.isSafeInteger(-112);
let isSafeInteger2 = NumberUtil.isSafeInteger(112);
```

##### isNumber determines whether it is a numeric value

```
let bl1 = NumberUtil.isNumber(12345);
let bl2 = NumberUtil.isNumber("12345");
let bl3 = NumberUtil.isNumber(1.212345);
let bl4 = NumberUtil.isNumber(true);
let bl5 = NumberUtil.isNumber(null);
let bl6 = NumberUtil.isNumber(undefined);
```

##### isEven Check whether the number is even

```
let isEven = NumberUtil.isEven(112);
```

##### isOdd Check whether the number is an odd number

```
let isOdd = NumberUtil.isOdd(112);
```

##### toNumber Converts a string to Number

```
let n1 = NumberUtil.toNumber("0.12579AB");
let n2 = NumberUtil.toNumber("123456");
let n3 = NumberUtil.toNumber("128.15624");
let n4 = NumberUtil.toNumber("哈哈");
```

##### toInt converts a string to an integer

```
let n1 = NumberUtil.toInt("0.12579");
let n2 = NumberUtil.toInt("12345");
let n3 = NumberUtil.toInt("128.15624");
let n4 = NumberUtil.toInt("哈哈");
```

##### toFloat converts a string to a floating point number

```
let f1 = NumberUtil.toFloat("0.12579");
let f2 = NumberUtil.toFloat("12345");
let f3 = NumberUtil.toFloat("128.15624");
let f4 = NumberUtil.toFloat("呵呵");
```

##### average calculates the average of the numbers

```
let average1 = NumberUtil.average(1, 2, 3, 4, 5, 6, 7, 8, 9);
let average2 = NumberUtil.average(...[1, 3, 5, 7, 9, 11, 13, 15, 17, 19]);
```

##### add

```
let add = NumberUtil.add(112, 200);
```

##### sub subtraction

```
let sub = NumberUtil.sub(200, 112);
```

##### sum

```
let sum = NumberUtil.sum(10, 12, 16, 18, 36, 22);
```

##### toDecimal Construct Decimal

```
let n1 = NumberUtil.toDecimal(112).toNumber();
let n2 = NumberUtil.toDecimal("200").toNumber();
let n3 = NumberUtil.toDecimal("0200").toNumber();
let n4 = NumberUtil.toDecimal("0.20").toNumber();
let n5 = NumberUtil.toDecimal(0.2222).toNumber();
```

##### addDecimal Addition Decimal

```
let n1 = NumberUtil.addDecimal(112, 200).toNumber();
let n2 = NumberUtil.addDecimal("200", "300").toNumber();
let n3 = NumberUtil.addDecimal("200", 600).toNumber();
```

##### subDecimal Subtraction Decimal

```
let n1 = NumberUtil.subDecimal(112, 20).toNumber();
let n2 = NumberUtil.subDecimal("200", 100).toNumber();
let n3 = NumberUtil.subDecimal("200", 55).toNumber();
```

##### sumDecimal sumDecimal

```
let n1 = NumberUtil.sumDecimal(1, 3, 5, 7, 9).toNumber();
let n2 = NumberUtil.sumDecimal("1", "3", "5", "7", "9").toNumber();
let n3 = NumberUtil.sumDecimal("10", 15, "25", "35", 45).toNumber();
```

## Creation is not easy, please give Elder Tong a thumbs up 👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   
