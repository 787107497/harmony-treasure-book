# Harmony-utils SHA, SHA tool class

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


## Introduction to SHA algorithm

------
SHA (Secure Hash Algorithm) is a family of cryptographic hash functions published by the National Institute of Standards and Technology (NIST) to generate a unique summary of data.
Its core version includes:
SHA-1: 160-bit summary, which was widely used in SSL/TLS and file verification, but has been eliminated due to collision vulnerabilities (actual attack cases in 2017).
SHA-2: (including SHA-256/384/512): adopts a block compression structure, which is highly collision-resistant and is now the mainstream choice for blockchain (such as Bitcoin) and digital certificates.
SHA-3: A new generation algorithm based on sponge structure, different from SHA-2 in design and has the potential to resist quantum computing.

## SHA application scenarios

------
Data integrity verification: Verify whether file transfers have been tampered with;
Digital signature: combined with public key encryption to achieve identity authentication (SHA-256 replaces SHA-1 and becomes mainstream);
Password storage: The system stores the hash value of the user's password instead of plain text (it needs to be combined with salt value to enhance security).


## API methods and usage

------

##### digest SHA summary

```
let str1 = "鸿蒙技术交流QQ群：1029219059";

let digest1 = await SHA.digest(str1);
LogUtil.error(`摘要，异步: ${digest1}`);

let digest2 = SHA.digestSync(str1);
LogUtil.error(`摘要，同步: ${digest2}`);

let digest3 = SHA.digestSync(str1, 'SHA512');
LogUtil.error(`摘要:\t ${digest3}`);

let digest4 = SHA.digestSync(str1, 'SHA512', 'base64');
LogUtil.error(`摘要:\t ${digest4}`);
```

##### digestSegment SHA summary, segmented

```
let str3 = "harmony-utils，一款高效的HarmonyOS工具包，封装了常用工具类，提供一系列简单易用的方法。帮助开发者快速构建鸿蒙应用。gitee地址：https://gitee.com/tongyuyan/harmony-utils。github主页地址：https://github.com/787107497。";

let digest1 = await SHA.digestSegment(str3);
LogUtil.error(`分段摘要，异步: ${digest1}`);

let digest2 = SHA.digestSegmentSync(str3);
LogUtil.error(`分段摘要，同步: ${digest2}`);

let digest3 = SHA.digestSegmentSync(str3, 'SHA256', 'base64', 256);
LogUtil.error(`分段摘要:\t ${digest3}`);
```

##### hmac message authentication code calculation

```
let symKey = CryptoUtil.generateSymKeySync("HMAC|SHA256");

let str1 = "鸿蒙技术交流QQ群：1029219059";

let digest1 = await SHA.hmac(str1);
LogUtil.error(`消息认证码计算，异步: ${digest1}`);

let digest2 = SHA.hmacSync(str1);
LogUtil.error(`消息认证码计算，同步: ${digest2}`);

let digest3 = SHA.hmacSync(str1, 'SHA256', symKey);
LogUtil.error(`消息认证码计算:\t ${digest3}`);
```

##### hmacSegment message authentication code calculation, segmented

```
let symKey = CryptoUtil.generateSymKeySync("HMAC|SHA256");

let str3 = "harmony-utils，一款高效的HarmonyOS工具包，封装了常用工具类，提供一系列简单易用的方法。帮助开发者快速构建鸿蒙应用。gitee地址：https://gitee.com/tongyuyan/harmony-utils。github主页地址：https://github.com/787107497。";

let digest1 = await SHA.hmacSegment(str3);
LogUtil.error(`分段消息认证码计算，异步: ${digest1}`);

let digest2 = SHA.hmacSegmentSync(str3);
LogUtil.error(`分段消息认证码计算，同步: ${digest2}`);

let digest3 = SHA.hmacSegmentSync(str3, 'SHA256', symKey, 'hex', 256);
LogUtil.error(`分段消息认证码计算:\t ${digest3}`);
```

## Creation is not easy, please give Elder Tong a thumbs up 👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   

