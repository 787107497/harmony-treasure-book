# ECDSA, ECDSA tool class for harmony-utils

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


## Introduction to ECDSA algorithm

------
ECDSA (Eelliptic Curve Digital Signature Algorithm) is a digital signature scheme based on elliptic curve cryptography, and the core is to ensure safety through the difficulty of solving the discrete logarithmic problem of elliptic curve. The principle is: after selecting the elliptic curve parameters, the private key (d) and public key (Q = d times G) are generated ((G) are the base point of the curve); when signing, the signature pair ((r, s) is calculated ((r, s)) is combined with the message hash value and random number, and the point coordinates are restored and compared through the public key and signature.

## ECDSA application scenarios

------
ECDSA (Eelliptic Curve Digital Signature Algorithm) is based on the elliptic curve discrete logarithmic problem and plays a key role in multiple scenarios with short keys, high security and low computing overhead. In the field of blockchain, it is used for transaction signatures and address generation of Bitcoin and Ethereum, ensuring that transactions cannot be tampered with; in terms of network security, it supports TLS/SSL certificate signatures, reduces handshake computing overhead, and is also applicable to identity authentication of VPNs and IoT devices. In compliance and resource-constrained scenarios, it complies with international standards, is used for electronic certificates, etc., and is suitable for low-computing equipment such as smart cards and mobile banking. Compared with RSA, 256-bit ECDSA security is equivalent to 3072-bit RSA, with small signed data and high efficiency, making it more suitable for blockchain, edge computing and other scenarios. Although it faces the threat of quantum computing, it is still the mainstream signature solution before the post-quantum cryptography transition and occupies an important position in the field of digital signatures.


## API methods and usage

------

##### sign Sign the data

```
let keyPair = await CryptoUtil.generateKeyPair('ECC256'); //生成密钥

let str1 = "鸿蒙技术交流QQ群：1029219059";
let dataBlob = CryptoHelper.strToDataBlob(str1, 'utf-8');

let signDataBlob = await ECDSA.sign(dataBlob, keyPair.priKey);
let signStr = CryptoHelper.dataBlobToStr(signDataBlob, 'hex');
LogUtil.error(`签名，异步: ${signStr}`);
```

##### verify the data verification

```
let keyPair = await CryptoUtil.generateKeyPair('ECC256'); //生成密钥

let str1 = "鸿蒙技术交流QQ群：1029219059";
let dataBlob = CryptoHelper.strToDataBlob(str1, 'utf-8');

let signDataBlob = await ECDSA.sign(dataBlob, keyPair.priKey);;
let verify = await ECDSA.verify(dataBlob, signDataBlob, keyPair.pubKey);
LogUtil.error(`验签，异步: ${verify}`);
```

##### signSegment Signs the data in segmentation

```
let keyPair = await CryptoUtil.generateKeyPair('ECC256'); //生成密钥

let str3 = "harmony-utils，一款高效的HarmonyOS工具包，封装了常用工具类，提供一系列简单易用的方法。帮助开发者快速构建鸿蒙应用。gitee地址：https://gitee.com/tongyuyan/harmony-utils。github主页地址：https://github.com/787107497。";
let data = CryptoHelper.strToUint8Array(str3, 'utf-8');

let signDataBlob = await ECDSA.signSegment(data, keyPair.priKey);
let signStr = CryptoHelper.dataBlobToStr(signDataBlob, 'base64');
LogUtil.error(`分段签名，异步: ${signStr}`);

```

##### verifySegment performs segmented verification of data

```
let keyPair = await CryptoUtil.generateKeyPair('ECC256'); //生成密钥

let str3 = "harmony-utils，一款高效的HarmonyOS工具包，封装了常用工具类，提供一系列简单易用的方法。帮助开发者快速构建鸿蒙应用。gitee地址：https://gitee.com/tongyuyan/harmony-utils。github主页地址：https://github.com/787107497。";
let data = CryptoHelper.strToUint8Array(str3, 'utf-8');

let signDataBlob = await ECDSA.signSegment(data, keyPair.priKey);
let verify = await ECDSA.verifySegment(data, signDataBlob, keyPair.pubKey);
LogUtil.error(`分段验签，异步: ${verify}`);
```

## Creation is not easy, please give Elder Tong a thumbs up 👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   

