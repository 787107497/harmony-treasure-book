# harmony-utils RandomUtil, random tool class

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

##### getRandomBoolean generates random Boolean values

```
let bl = RandomUtil.getRandomBoolean();
```

##### getRandomInt generates random integers (the range can be specified)

```
let n1 = RandomUtil.getRandomInt();
```

##### getRandomNumber Generates a random number within a specified range

```
let n3 = RandomUtil.getRandomNumber(10000, 1000000);
```

##### getRandomLimit generates a random number within the specified range [0,limit)

```
let n2 = RandomUtil.getRandomLimit(1000);
```

##### getRandomChineseChar generates a random Chinese character

```
let str1 = RandomUtil.getRandomChineseChar();
```

##### getRandomChinese generates random Chinese characters

```
let str2 = RandomUtil.getRandomChinese(12);
```

##### getRandomStr randomly generates strings of specified length according to the specified string.

```
let r1 = RandomUtil.getRandomStr(15, "ACCDEFGHIJKMNL");
```

##### getRandomDataBlob Generates DataBlob of randomly specified length

```
let dataBlob = RandomUtil.getRandomDataBlob(8);
```

##### getRandomUint8Array generates a Uint8Array of randomly specified length

```
let unit8Array = RandomUtil.getRandomUint8Array(8);
```

##### getRandomColor generates random colors in hexadecimal

```
let c3 = RandomUtil.getRandomColor();
```

##### generateUUID36 generates 36-bit UUID with -

```
let uuid36 = RandomUtil.generateUUID36();
```

##### generateUUID32 generates 32-bit UUID with -

```
let uuid32 = RandomUtil.generateUUID32();
```

##### generateRandomUUID generates a random RFC 4122 version 4 string type UUID using the Encrypted Secure Random Number Generator

```
let uuid1 = RandomUtil.generateRandomUUID();
```

##### generateRandomBinaryUUID generates random RFC 4122 version 4 Uint8Array type UUID using Encrypted Secure Random Number Generator

```
let uuid2 = RandomUtil.generateRandomBinaryUUID();
```

## Creation is not easy, please give Elder Tong a thumbs up 👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   



