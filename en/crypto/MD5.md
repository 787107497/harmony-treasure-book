# Harmony-utils MD5, MD5 tool class

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


## Introduction to MD5 algorithm

------
MD5 (Message-Digest Algorithm 5) is a password hash function designed by Ronald Rivest in 1991. It can generate a fixed-length hash value of 128 bits (16 bytes) from any length data. Its core is realized through the ‌filling-blocking-cyclic compression process: first fill the input to a 512-bit multiple, then perform 4 rounds of nonlinear operations in chunks (16 operations per round), and finally output a unique summary.
This algorithm has been widely used in file integrity verification (such as software package verification), password storage and digital certificate signature. However, due to the existence of collision vulnerabilities (different data with the same hash can be artificially constructed), since it was proven that it is not resistant to collision attacks in 2004, it has been gradually replaced by more secure algorithms such as SHA-256. It is still seen in non-sensitive scenarios such as cache identifiers or data deduplication. Because MD5 has a collision attack risk (cracked by Wang Xiaoyun's team in 2004), key areas such as finance and government affairs have been banned. It is recommended to switch to SM3/SHA-256.


## API methods and usage

------

##### digest MD5 summary

```
let str1 = "鸿蒙技术交流QQ群：1029219059";

let digest1 = await MD5.digest(str1);
LogUtil.error(`摘要，异步: ${digest1}`);

let digest2 = MD5.digestSync(str1);
LogUtil.error(`摘要，同步1: ${digest2}`);

let digest3 = MD5.digestSync(str1, 'base64');
LogUtil.error(`摘要，同步2: ${digest3}`);
```

##### digestSegment MD5 summary, segmented

```
let str3 = "harmony-utils，一款高效的HarmonyOS工具包，封装了常用工具类，提供一系列简单易用的方法。帮助开发者快速构建鸿蒙应用。gitee地址：https://gitee.com/tongyuyan/harmony-utils。github主页地址：https://github.com/787107497。";

let digest1 = await MD5.digestSegment(str3);
LogUtil.error(`分段摘要，异步: ${digest1}`);

let digest2 = MD5.digestSegmentSync(str3);
LogUtil.error(`分段摘要，同步1: ${digest2}`);

let digest3 = MD5.digestSegmentSync(str3, 'base64', 256);
LogUtil.error(`分段摘要，同步2: ${digest3}`);
```

##### hmac message authentication code calculation

```
let symKey = CryptoUtil.generateSymKeySync("AES256");
let str1 = "鸿蒙技术交流QQ群：1029219059";

let digest1 = await MD5.hmac(str1, symKey);
LogUtil.error(`消息认证码计算，异步: ${digest1}`);

let digest2 = MD5.hmacSync(str1, symKey);
LogUtil.error(`消息认证码计算，同步1: ${digest2}`);

let digest3 = MD5.hmacSync(str1, symKey, 'base64');
LogUtil.error(`消息认证码计算，同步2: ${digest3}`);
```

##### hmacSegment message authentication code calculation, segmented

```
let symKey = CryptoUtil.generateSymKeySync("AES256");
let str3 = "harmony-utils，一款高效的HarmonyOS工具包，封装了常用工具类，提供一系列简单易用的方法。帮助开发者快速构建鸿蒙应用。gitee地址：https://gitee.com/tongyuyan/harmony-utils。github主页地址：https://github.com/787107497。";

let digest1 = await MD5.hmacSegment(str3, symKey);
LogUtil.error(`分段消息认证码计算，异步: ${digest1}`);

let digest2 = MD5.hmacSegmentSync(str3, symKey);
LogUtil.error(`分段消息认证码计算，同步1: ${digest2}`);

let digest3 = MD5.hmacSegmentSync(str3, symKey, 'hex', 256);
LogUtil.error(`分段消息认证码计算，同步2: ${digest3}`);
```

## Creation is not easy, please give Elder Tong a thumbs up 👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   

