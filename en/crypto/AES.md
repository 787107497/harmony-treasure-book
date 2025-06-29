# AES, AES encryption and decryption

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

## Introduction to AES algorithm

------

AES (Advanced Encryption Standard) is a symmetric packet encryption algorithm released by NIST in 2001 to replace DES. It supports 128/192/256-bit keys, corresponding to 10/12/14 rounds of encryption, and the packet length is fixed to 128 bits. The algorithm generates multi-wheel keys through key expansion. The encryption process includes operations such as byte replacement, row shift, column obfuscation (last wheel omitted) and wheel key addition. It uses S-box nonlinear transformation and matrix operations to achieve obfuscation diffusion and resists attacks such as differential analysis. Its advantages are high symmetric encryption efficiency, strong key flexibility, and hardware-friendly (such as AES-NI instruction set acceleration), which is widely used in HTTPS, hard disk encryption and other scenarios, and is the current mainstream security encryption standard.

## AES application scenarios

------

As the mainstream symmetric encryption algorithm, AES is widely used in multiple scenarios due to its high security and efficiency. In network communication, HTTPS, VPN and encrypted communication tools use it to ensure the security of data transmission; in the field of data storage, hard disk encryption, database sensitive field protection and cloud file encryption all rely on AES; in the Internet of Things, smart home and industrial control devices use it to communicate encrypted; mobile device systems and SIM cards also use AES to ensure security. In addition, financial payment, e-government, hardware acceleration (such as AES - NI) and other scenarios are also inseparable from AES, which is the core technology in the field of information security.

## API methods and usage

------

##### generateSymKey generates symmetric key SymKey

```
let symKey1 = await AES.generateSymKey();
let symKeyStr1 = CryptoHelper.dataBlobToStr(symKey1.getEncoded(), 'hex');
LogUtil.error(`对称密钥1：${symKeyStr1}`);

let symKey2 = AES.generateSymKeySync();
let symKeyStr2 = CryptoHelper.dataBlobToStr(symKey2.getEncoded(), 'base64');
LogUtil.error(`对称密钥2：${symKeyStr2}`);
```

##### encryptGCM encryption (GCM mode)

```
let gcmParams = CryptoUtil.generateGcmParamsSpec();

let str1 = "鸿蒙技术交流QQ群：1029219059";
let smyKeyHexStr = "bf77a17b498a6e808048a734f2e992ab452c4c5f1c37f901a5a58f566b6b01d0"; //16进制字符串密钥
let symKey = await CryptoUtil.getConvertSymKey('AES256', smyKeyHexStr, 'hex');
let dataBlob = CryptoHelper.strToDataBlob(str1, 'utf-8'); //待加密数据

let encryptDataBlob1 = await AES.encryptGCM(dataBlob, symKey, gcmParams); //加密
let encryptStr1 = CryptoHelper.dataBlobToStr(encryptDataBlob1, 'utf-8');
LogUtil.error(`加密（GCM模式）,异步：${encryptStr1}`);

let encryptDataBlob2 = AES.encryptGCMSync(dataBlob, symKey, gcmParams); //加密
let encryptStr2 = CryptoHelper.dataBlobToStr(encryptDataBlob2, 'utf-8');
LogUtil.error(`加密（GCM模式）,同步：${encryptStr2}`);
```

##### decryptGCM decryption (GCM mode)

```
let gcmParams = CryptoUtil.generateGcmParamsSpec();

let str1 = "鸿蒙技术交流QQ群：1029219059";
let smyKeyHexStr = "bf77a17b498a6e808048a734f2e992ab452c4c5f1c37f901a5a58f566b6b01d0"; //16进制字符串密钥
let symKey = await CryptoUtil.getConvertSymKey('AES256', smyKeyHexStr, 'hex');
let dataBlob = CryptoHelper.strToDataBlob(str1, 'utf-8'); //待加密数据

let encryptDataBlob1 = await AES.encryptGCM(dataBlob, symKey, gcmParams); //加密
let decryptDataBlob1 = await AES.decryptGCM(encryptDataBlob1, symKey, gcmParams); //解密
let decryptStr1 = CryptoHelper.dataBlobToStr(decryptDataBlob1, 'utf-8');
LogUtil.error(`解密（GCM模式）,异步：${decryptStr1}`);

let encryptDataBlob2 = AES.encryptGCMSync(dataBlob, symKey, gcmParams); //加密
let decryptDataBlob2 = AES.decryptGCMSync(encryptDataBlob2, symKey, gcmParams); //解密
let decryptStr2 = CryptoHelper.dataBlobToStr(decryptDataBlob2, 'utf-8');
LogUtil.error(`解密（GCM模式）,同步：${decryptStr2}`);
```

##### encryptCBC encryption (CBC mode)

```
let ivParams = CryptoUtil.generateIvParamsSpec();

let str2 = "harmony-utils，一款高效的HarmonyOS工具包，封装了常用工具类，提供一系列简单易用的方法。帮助开发者快速构建鸿蒙应用。";
let smyKeyBase64Str = "tlDExo6TzfIGyl36+BNEqR+Xxg83sAlvbzrvr3Seqlk="; //base64符串密钥
let symKey = CryptoUtil.getConvertSymKeySync('AES256', smyKeyBase64Str, 'base64');
let dataBlob = CryptoHelper.strToDataBlob(str2, 'utf-8'); //待加密数据

let encryptDataBlob1 = await AES.encryptCBC(dataBlob, symKey, ivParams); //加密
let encryptStr1 = CryptoHelper.dataBlobToStr(encryptDataBlob1, 'utf-8');
LogUtil.error(`加密（CBC模式）,异步：${encryptStr1}`);

let encryptDataBlob2 = AES.encryptCBCSync(dataBlob, symKey, ivParams); //加密
let encryptStr2 = CryptoHelper.dataBlobToStr(encryptDataBlob2, 'utf-8');
LogUtil.error(`加密（CBC模式）,同步：${encryptStr2}`);
```

##### decryptCBC decryption (CBC mode)

```
let ivParams = CryptoUtil.generateIvParamsSpec();

let str2 = "harmony-utils，一款高效的HarmonyOS工具包，封装了常用工具类，提供一系列简单易用的方法。帮助开发者快速构建鸿蒙应用。";
let smyKeyBase64Str = "tlDExo6TzfIGyl36+BNEqR+Xxg83sAlvbzrvr3Seqlk="; //base64符串密钥
let symKey = CryptoUtil.getConvertSymKeySync('AES256', smyKeyBase64Str, 'base64');
let dataBlob = CryptoHelper.strToDataBlob(str2, 'utf-8'); //待加密数据

let encryptDataBlob1 = await AES.encryptCBC(dataBlob, symKey, ivParams); //加密
let decryptDataBlob1 = await AES.decryptCBC(encryptDataBlob1, symKey, ivParams); //解密
let decryptStr1 = CryptoHelper.dataBlobToStr(decryptDataBlob1, 'utf-8');
LogUtil.error(`解密（CBC模式）,异步：${decryptStr1}`);

let encryptDataBlob2 = AES.encryptCBCSync(dataBlob, symKey, ivParams); //加密
let decryptDataBlob2 = AES.decryptCBCSync(encryptDataBlob2, symKey, ivParams); //解密
let decryptStr2 = CryptoHelper.dataBlobToStr(decryptDataBlob2, 'utf-8');
LogUtil.error(`解密（CBC模式）,同步：${decryptStr2}`);
```

##### encryptECB encryption (ECB mode)

```
let str1 = "鸿蒙技术交流QQ群：1029219059";

let smyKeyBase64Str = "tlDExo6TzfIGyl36+BNEqR+Xxg83sAlvbzrvr3Seqlk="; //base64符串密钥
let symKey = CryptoUtil.getConvertSymKeySync('AES256', smyKeyBase64Str, 'base64');
let dataBlob = CryptoHelper.strToDataBlob(str1, 'utf-8'); //待加密数据

let encryptDataBlob1 = await AES.encryptECB(dataBlob, symKey); //加密
let encryptStr1 = CryptoHelper.dataBlobToStr(encryptDataBlob1, 'utf-8');
LogUtil.error(`加密（ECB模式）,异步：${encryptStr1}`);

let encryptDataBlob2 = AES.encryptECBSync(dataBlob, symKey); //加密
let encryptStr2 = CryptoHelper.dataBlobToStr(encryptDataBlob2, 'utf-8');
LogUtil.error(`加密（ECB模式）,同步：${encryptStr2}`);
```

##### decryptECB decryption (ECB mode)

```
let str1 = "鸿蒙技术交流QQ群：1029219059";

let smyKeyBase64Str = "tlDExo6TzfIGyl36+BNEqR+Xxg83sAlvbzrvr3Seqlk="; //base64符串密钥
let symKey = CryptoUtil.getConvertSymKeySync('AES256', smyKeyBase64Str, 'base64');
let dataBlob = CryptoHelper.strToDataBlob(str1, 'utf-8'); //待加密数据

let encryptDataBlob1 = await AES.encryptECB(dataBlob, symKey); //加密
let decryptDataBlob1 = await AES.decryptECB(encryptDataBlob1, symKey); //解密
let decryptStr1 = CryptoHelper.dataBlobToStr(decryptDataBlob1, 'utf-8');
LogUtil.error(`解密（ECB模式）,异步：${decryptStr1}`);

let encryptDataBlob2 = AES.encryptECBSync(dataBlob, symKey); //加密
let decryptDataBlob2 = AES.decryptECBSync(encryptDataBlob2, symKey); //解密
let decryptStr2 = CryptoHelper.dataBlobToStr(decryptDataBlob2, 'utf-8');
LogUtil.error(`解密（ECB模式）,同步：${decryptStr2}`);
```

##### encryptGCMSegment encryption (GCM mode) segmentation

```
let gcmParams = CryptoUtil.generateGcmParamsSpec();

let str3 = "harmony-utils，一款高效的HarmonyOS工具包，封装了常用工具类，提供一系列简单易用的方法。帮助开发者快速构建鸿蒙应用。gitee地址：https://gitee.com/tongyuyan/harmony-utils。github主页地址：https://github.com/787107497。";

let smyKeyHexStr = "bf77a17b498a6e808048a734f2e992ab452c4c5f1c37f901a5a58f566b6b01d0"; //16进制字符串密钥
let symKey = await CryptoUtil.getConvertSymKey('AES256', smyKeyHexStr, 'hex');
let dataBlob = CryptoHelper.strToDataBlob(str3, 'utf-8'); //待加密数据

let encryptDataBlob1 = await AES.encryptGCMSegment(dataBlob, symKey, gcmParams); //加密
let encryptStr1 = CryptoHelper.dataBlobToStr(encryptDataBlob1, 'utf-8');
LogUtil.error(`分段加密（GCM模式）,异步：${encryptStr1}`);

let encryptDataBlob2 = AES.encryptGCMSegmentSync(dataBlob, symKey, gcmParams); //加密
let encryptStr2 = CryptoHelper.dataBlobToStr(encryptDataBlob2, 'utf-8');
LogUtil.error(`分段加密（GCM模式）,同步：${encryptStr2}`);
```

##### decryptGCMSegment Decrypt (GCM mode) segmentation

```
let gcmParams = CryptoUtil.generateGcmParamsSpec();

let str3 = "harmony-utils，一款高效的HarmonyOS工具包，封装了常用工具类，提供一系列简单易用的方法。帮助开发者快速构建鸿蒙应用。gitee地址：https://gitee.com/tongyuyan/harmony-utils。github主页地址：https://github.com/787107497。";

let smyKeyHexStr = "bf77a17b498a6e808048a734f2e992ab452c4c5f1c37f901a5a58f566b6b01d0"; //16进制字符串密钥
let symKey = await CryptoUtil.getConvertSymKey('AES256', smyKeyHexStr, 'hex');
let dataBlob = CryptoHelper.strToDataBlob(str3, 'utf-8'); //待加密数据

let encryptDataBlob1 = await AES.encryptGCMSegment(dataBlob, symKey, gcmParams); //加密
let decryptDataBlob1 = await AES.decryptGCMSegment(encryptDataBlob1, symKey, gcmParams); //解密
let decryptStr1 = CryptoHelper.dataBlobToStr(decryptDataBlob1, 'utf-8');
LogUtil.error(`分段解密（GCM模式）,异步：${decryptStr1}`);

let encryptDataBlob2 = AES.encryptGCMSegmentSync(dataBlob, symKey, gcmParams); //加密
let decryptDataBlob2 = AES.decryptGCMSegmentSync(encryptDataBlob2, symKey, gcmParams); //解密
let decryptStr2 = CryptoHelper.dataBlobToStr(decryptDataBlob2, 'utf-8');
LogUtil.error(`分段解密（GCM模式）,同步：${decryptStr2}`);
```

## Creation is not easy, please give Elder Tong a thumbs up 👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   