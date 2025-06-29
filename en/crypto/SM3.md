# Harmony-utils SM3, SM3 tool class

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


## Introduction to SM3 algorithm

------
SM3 is the commercial cryptographic hash algorithm standard (GM/T 0004-2012) issued by the China National Cryptography Administration in 2010. It outputs a 256-bit fixed-length hash value, and its security strength is equivalent to that of SHA-256. This algorithm adopts the Merkle-Damgard structure design, and achieves data obfuscation through message filling, grouping expansion and 32 rounds of iterative compression, and has anti-collision attack and original image attack capabilities. As the core component of the domestic cryptographic system, SM3 is widely used in digital signatures, electronic certification, financial payments, and Internet of Things security, and has been included in the ISO/IEC 10118-3 international standard. Its efficiency is adapted to ordinary computers and embedded devices, and supports the formulation of more than 30 domestic cryptographic industry standards.

## SM3 application scenarios

------
Digital signature: Used in conjunction with SM2 asymmetric algorithm to generate hash summary and sign electronic contracts, government documents, etc. to ensure data integrity and non-repudiation;
Financial security: used for online banking transaction verification and payment packet integrity protection. More than 80% of domestic financial institutions deploy this algorithm in key systems;
Internet of Things Authentication: Generate message authentication code (HMAC-SM3) for smart device communication data to prevent data tampering in industrial-grade SSDs, smart grids and other scenarios;
Crypto protocol basis: Support key derivation and verification of security protocols such as SSL/TLS, VPN, etc. to meet the needs of domestic substitution.


## API methods and usage

------

##### digest SM3 summary

```
let str1 = "鸿蒙技术交流QQ群：1029219059";

let digest1 = await SM3.digest(str1);
LogUtil.error(`摘要，异步: ${digest1}`);

let digest2 = SM3.digestSync(str1,'hex');
LogUtil.error(`摘要，同步1: ${digest2}`);

let digest3 = SM3.digestSync(str1, 'base64');
LogUtil.error(`摘要，同步2:  ${digest3}`);
```

##### digestSegment SM3 segment summary

```
let str3 = "harmony-utils，一款高效的HarmonyOS工具包，封装了常用工具类，提供一系列简单易用的方法。帮助开发者快速构建鸿蒙应用。";

let digest1 = await SM3.digestSegment(str3);
LogUtil.error(`分段摘要，异步: ${digest1}`);

let digest2 = SM3.digestSegmentSync(str3);
LogUtil.error(`分段摘要，同步1: ${digest2}`);

let digest3 = SM3.digestSegmentSync(str3, 'base64', 256);
LogUtil.error(`分段摘要，同步2: ${digest3}`);
```

##### hmac SM3 message authentication code calculation

```
let str1 = "鸿蒙技术交流QQ群：1029219059";
let symKey = CryptoUtil.generateSymKeySync("HMAC|SM3");

let digest1 = await SM3.hmac(str1, symKey);
LogUtil.error(`消息认证码计算，异步: ${digest1}`);

let digest2 = SM3.hmacSync(str1, symKey);
LogUtil.error(`消息认证码计算，同步1: ${digest2}`);

let digest3 = SM3.hmacSync(str1, symKey, 'base64');
LogUtil.error(`消息认证码计算，同步2: ${digest3}`);
```

##### hmacSegment SM3 message authentication code calculation, segmented

```
let str2 = "harmony-utils，一款高效的HarmonyOS工具包，封装了常用工具类，提供一系列简单易用的方法。帮助开发者快速构建鸿蒙应用。";
let symKey = CryptoUtil.generateSymKeySync("HMAC|SM3");

let digest1 = await SM3.hmacSegment(str2, symKey);
LogUtil.error(`分段消息认证码计算，异步: ${digest1}`);

let digest2 = SM3.hmacSegmentSync(str2, symKey);
LogUtil.error(`分段消息认证码计算，同步1: ${digest2}`);

let digest3 = SM3.hmacSegmentSync(str2, symKey, 'hex', 256);
LogUtil.error(`分段消息认证码计算，同步2: ${digest3}`);
```

## Creation is not easy, please give Elder Tong a thumbs up 👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   
