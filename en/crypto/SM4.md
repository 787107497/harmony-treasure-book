# Harmony-utils SM4, SM4 encryption and decryption

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


## Introduction to SM4 algorithm

------
SM4 is a commercial symmetric encryption algorithm independently developed by China. It was released by the State Cryptography Administration in 2006 and became the national cryptography industry standard in 2012 (GM/T 0002-2012). This algorithm uses a 128-bit packet length and a 128-bit key length to realize data encryption through 32 rounds of nonlinear iterative structures, and the security strength is comparable to that of AES-128. Its core design includes S-box replacement, cyclic shifting and other operations, and supports standard working modes such as ECB and CBC. As the core component of China's cryptographic system (SM series), SM4 is widely used in financial payment, e-government, Internet of Things and other fields, meeting domestic cryptographic compliance requirements. The algorithm has the characteristics of efficient software and hardware implementation, and has passed the ISO/IEC international standard certification (18033-3), becoming an important basic algorithm in the field of information security in my country.

## SM4 application scenarios

------
Financial payment: Encrypt sensitive data (such as transaction amount and account information) in bank card transactions, mobile payments and online banking to ensure the security of transmission and comply with the password compliance requirements of China's financial industry;
E-government: used for data transmission and encryption of electronic ID cards and government affairs systems, and combined with SM2 signature algorithm to achieve identity authentication and data integrity protection;
Internet of Things Security: Encrypt communication data between smart devices to prevent data leakage in industrial-grade SSDs, smart homes and other scenarios;
Replacement of localized innovation and innovation: replace AES algorithm in information technology application innovation projects to meet the independent and controllable needs of party and government organs and key infrastructure.


## API methods and usage

------

##### generateSymKey generates symmetric key SymKey

```
let symKey1 = await SM4.generateSymKey();
let symKeyStr1 = CryptoHelper.dataBlobToStr(symKey1.getEncoded(), 'hex');
LogUtil.error(`对称密钥1：${symKeyStr1}`);

let symKey2 = SM4.generateSymKeySync();
let symKeyStr2 = CryptoHelper.dataBlobToStr(symKey2.getEncoded(), 'base64');
LogUtil.error(`对称密钥2：${symKeyStr2}`);
```

##### encryptGCM encryption (GCM mode)

```
let gcmParams = CryptoUtil.generateGcmParamsSpec();

let str1 = "鸿蒙技术交流QQ群：1029219059";

let smyKeyHexStr = "da4eed5a22f8883e2339c0b563161c38"; //16进制字符串密钥
let symKey = await CryptoUtil.getConvertSymKey('SM4_128', smyKeyHexStr, 'hex');
let dataBlob = CryptoHelper.strToDataBlob(str1, 'utf-8'); //待加密数据

let encryptDataBlob1 = await SM4.encryptGCM(dataBlob, symKey, gcmParams); //加密
let encryptStr1 = CryptoHelper.dataBlobToStr(encryptDataBlob1, 'utf-8');
LogUtil.error(`加密（GCM模式）,异步：${encryptStr1}`);

let encryptDataBlob2 = SM4.encryptGCMSync(dataBlob, symKey, gcmParams!); //加密
let encryptStr2 = CryptoHelper.dataBlobToStr(encryptDataBlob2, 'utf-8');
LogUtil.error(`加密（GCM模式）,同步：${encryptStr2}`);
```

##### decryptGCM decryption (GCM mode)

```
let gcmParams = CryptoUtil.generateGcmParamsSpec();

let str1 = "鸿蒙技术交流QQ群：1029219059";

let smyKeyHexStr = "da4eed5a22f8883e2339c0b563161c38"; //16进制字符串密钥
let symKey = await CryptoUtil.getConvertSymKey('SM4_128', smyKeyHexStr, 'hex');
let dataBlob = CryptoHelper.strToDataBlob(str1, 'utf-8'); //待加密数据

let encryptDataBlob1 = await SM4.encryptGCM(dataBlob, symKey, gcmParams!); //加密
let decryptDataBlob1 = await SM4.decryptGCM(encryptDataBlob1, symKey, gcmParams!); //解密
let decryptStr1 = CryptoHelper.dataBlobToStr(decryptDataBlob1, 'utf-8');
LogUtil.error(`解密（GCM模式）,异步：${decryptStr1}`);

let encryptDataBlob2 = SM4.encryptGCMSync(dataBlob, symKey, gcmParams!); //加密
let decryptDataBlob2 = SM4.decryptGCMSync(encryptDataBlob2, symKey, gcmParams!); //解密
let decryptStr2 = CryptoHelper.dataBlobToStr(decryptDataBlob2, 'utf-8');
LogUtil.error(`解密（GCM模式）,同步：${decryptStr2}`);
```

##### encryptCBC encryption (CBC mode)

```
let ivParams = CryptoUtil.generateIvParamsSpec();

let str2 = "harmony-utils，一款高效的HarmonyOS工具包，封装了常用工具类，提供一系列简单易用的方法。帮助开发者快速构建鸿蒙应用。";
let smyKeyBase64Str = "2k7tWiL4iD4jOcC1YxYcOA=="; //base64符串密钥
let symKey = CryptoUtil.getConvertSymKeySync('SM4_128', smyKeyBase64Str, 'base64');
let dataBlob = CryptoHelper.strToDataBlob(str2, 'utf-8'); //待加密数据

let encryptDataBlob1 = await SM4.encryptCBC(dataBlob, symKey, ivParams); //加密
let encryptStr1 = CryptoHelper.dataBlobToStr(encryptDataBlob1, 'utf-8');
LogUtil.error(`加密（CBC模式）,异步：${encryptStr1}`);

let encryptDataBlob2 = SM4.encryptCBCSync(dataBlob, symKey, ivParams); //加密
let encryptStr2 = CryptoHelper.dataBlobToStr(encryptDataBlob2, 'utf-8');
LogUtil.error(`加密（CBC模式）,同步：${encryptStr2}`);

```

##### decryptCBC decryption (CBC mode)

```
let ivParams = CryptoUtil.generateIvParamsSpec();

let str2 = "harmony-utils，一款高效的HarmonyOS工具包，封装了常用工具类，提供一系列简单易用的方法。帮助开发者快速构建鸿蒙应用。";
et smyKeyBase64Str = "2k7tWiL4iD4jOcC1YxYcOA=="; //base64符串密钥
let symKey = CryptoUtil.getConvertSymKeySync('SM4_128', smyKeyBase64Str, 'base64');
let dataBlob = CryptoHelper.strToDataBlob(str2, 'utf-8'); //待加密数据

let encryptDataBlob1 = await SM4.encryptCBC(dataBlob, symKey, ivParams); //加密
let decryptDataBlob1 = await SM4.decryptCBC(encryptDataBlob1, symKey, ivParams); //解密
let decryptStr1 = CryptoHelper.dataBlobToStr(decryptDataBlob1, 'utf-8');
LogUtil.error(`解密（CBC模式）,异步：${decryptStr1}`);

let encryptDataBlob2 = SM4.encryptCBCSync(dataBlob, symKey, ivParams); //加密
let decryptDataBlob2 = SM4.decryptCBCSync(encryptDataBlob2, symKey, ivParams); //解密
let decryptStr2 = CryptoHelper.dataBlobToStr(decryptDataBlob2, 'utf-8');
LogUtil.error(`解密（CBC模式）,同步：${decryptStr2}`);
```

##### encryptECB encryption (ECB mode)

```
let str1 = "鸿蒙技术交流QQ群：1029219059";

let smyKeyBase64Str = "2k7tWiL4iD4jOcC1YxYcOA=="; //base64符串密钥
let symKey = CryptoUtil.getConvertSymKeySync('SM4_128', smyKeyBase64Str, 'base64');
let dataBlob = CryptoHelper.strToDataBlob(str1, 'utf-8'); //待加密数据

let encryptDataBlob1 = await SM4.encryptECB(dataBlob, symKey); //加密
let encryptStr1 = CryptoHelper.dataBlobToStr(encryptDataBlob1, 'utf-8');
LogUtil.error(`加密（ECB模式）,异步：${encryptStr1}`);

let encryptDataBlob2 = SM4.encryptECBSync(dataBlob, symKey); //加密
let encryptStr2 = CryptoHelper.dataBlobToStr(encryptDataBlob2, 'utf-8');
LogUtil.error(`加密（ECB模式）,同步：${encryptStr2}`);
```

##### decryptECB decryption (ECB mode)

```
let str1 = "鸿蒙技术交流QQ群：1029219059";

let smyKeyBase64Str = "2k7tWiL4iD4jOcC1YxYcOA=="; //base64符串密钥
let symKey = CryptoUtil.getConvertSymKeySync('SM4_128', smyKeyBase64Str, 'base64');
let dataBlob = CryptoHelper.strToDataBlob(str1, 'utf-8'); //待加密数据

let encryptDataBlob1 = await SM4.encryptECB(dataBlob, symKey); //加密
let decryptDataBlob1 = await SM4.decryptECB(encryptDataBlob1, symKey); //解密
let decryptStr1 = CryptoHelper.dataBlobToStr(decryptDataBlob1, 'utf-8');
LogUtil.error(`解密（ECB模式）,异步：${decryptStr1}`);

let encryptDataBlob2 = SM4.encryptECBSync(dataBlob, symKey); //加密
let decryptDataBlob2 = SM4.decryptECBSync(encryptDataBlob2, symKey); //解密
let decryptStr2 = CryptoHelper.dataBlobToStr(decryptDataBlob2, 'utf-8');
LogUtil.error(`解密（ECB模式）,同步：${decryptStr2}`);
```

##### encryptGCMSegment encryption (GCM mode) segmentation

```
let gcmParams = CryptoUtil.generateGcmParamsSpec();

let str3 = "harmony-utils，一款高效的HarmonyOS工具包，封装了常用工具类，提供一系列简单易用的方法。帮助开发者快速构建鸿蒙应用。gitee地址：https://gitee.com/tongyuyan/harmony-utils。github主页地址：https://github.com/787107497。";

let smyKeyHexStr = "da4eed5a22f8883e2339c0b563161c38"; //16进制字符串密钥
let symKey = await CryptoUtil.getConvertSymKey('SM4_128', smyKeyHexStr, 'hex');
let dataBlob = CryptoHelper.strToDataBlob(str3, 'utf-8'); //待加密数据


let encryptDataBlob1 = await SM4.encryptGCMSegment(dataBlob, symKey, gcmParams!); //加密
let encryptStr1 = CryptoHelper.dataBlobToStr(encryptDataBlob1, 'utf-8');
LogUtil.error(`分段加密（GCM模式）,异步：${encryptStr1}`);

let encryptDataBlob2 = SM4.encryptGCMSegmentSync(dataBlob, symKey, gcmParams!); //加密
let encryptStr2 = CryptoHelper.dataBlobToStr(encryptDataBlob2, 'utf-8');
LogUtil.error(`分段加密（GCM模式）,同步：${encryptStr2}`);
```

##### decryptGCMSegment Decrypt (GCM mode) segmentation

```
let gcmParams = CryptoUtil.generateGcmParamsSpec();

let str3 = "harmony-utils，一款高效的HarmonyOS工具包，封装了常用工具类，提供一系列简单易用的方法。帮助开发者快速构建鸿蒙应用。gitee地址：https://gitee.com/tongyuyan/harmony-utils。github主页地址：https://github.com/787107497。";

let smyKeyHexStr = "da4eed5a22f8883e2339c0b563161c38"; //16进制字符串密钥
let symKey = await CryptoUtil.getConvertSymKey('SM4_128', smyKeyHexStr, 'hex');
let dataBlob = CryptoHelper.strToDataBlob(str3, 'utf-8'); //待加密数据

let encryptDataBlob1 = await SM4.encryptGCMSegment(dataBlob, symKey, gcmParams!); //加密);
let decryptDataBlob1 = await SM4.decryptGCMSegment(encryptDataBlob1, symKey, gcmParams!); //解密
let decryptStr1 = CryptoHelper.dataBlobToStr(decryptDataBlob1, 'utf-8');
LogUtil.error(`分段解密（GCM模式）,异步：${decryptStr1}`);

let encryptDataBlob2 = SM4.encryptGCMSegmentSync(dataBlob, symKey, gcmParams!); //加密
let decryptDataBlob2 = SM4.decryptGCMSegmentSync(encryptDataBlob2, symKey, gcmParams!); //解密
let decryptStr2 = CryptoHelper.dataBlobToStr(decryptDataBlob2, 'utf-8');
LogUtil.error(`分段解密（GCM模式）,同步：${decryptStr2}`);
```

## Creation is not easy, please give Elder Tong a thumbs up 👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   
