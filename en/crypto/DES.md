# DES, DES encryption and decryption

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

## Introduction to DES algorithm

------
DES (Data Encryption Standard) is the first standardized symmetric packet encryption algorithm released by the United States in 1977. It uses 64-bit packets, 56-bit valid keys (including 8-bit check bits) and 16-round Feistel iterative structures to achieve encryption through extended permutation, S-box nonlinear transformation and P-box displacement. Its core is based on the Feistel network, and the plain text is divided into two parts, left and right, and each round is enhanced by subkey and round function operations to enhance confusion and diffusion.
However, DES has significant security flaws: only 2⁵⁶ combinations of 56-bit key spaces, which were confirmed to be brute-forced by 2500 computers in 22 hours in 1999, and the existence of weak keys (such as all 0 keys) makes encryption and decryption equivalent, making it difficult to resist differential/linear cryptographic analysis. In 2001, it was replaced by AES, and the transition solution 3DES increased the key length to 112/168 bits through triple encryption, and was used in scenarios such as financial POS machines.
The historical value of DES lies in promoting the standardization of encryption technology and laying the theoretical foundation of Feistel structure. It is still a classic case of cryptography teaching. Although it has been eliminated in the mainstream field, its design ideas provide an important reference for modern symmetric encryption algorithms such as AES.


## API methods and usage

------

##### generateSymKey generates symmetric key SymKey

```
let symKey1 = await DES.generateSymKey();
let symKeyStr1 = CryptoHelper.dataBlobToStr(symKey1.getEncoded(), 'hex');
LogUtil.error(`对称密钥1：${symKeyStr1}`);

let symKey2 = DES.generateSymKeySync();
let symKeyStr2 = CryptoHelper.dataBlobToStr(symKey2.getEncoded(), 'base64');
LogUtil.error(`对称密钥2：${symKeyStr2}`);
```

##### encryptECB encryption (ECB mode)

```
let str1 = "鸿蒙技术交流QQ群：1029219059";

let smyKeyBase64Str = "bZen8i4KBFVMlomHBNWeExvFydWEXspO"; //base64符串密钥
let symKey = CryptoUtil.getConvertSymKeySync('3DES192', smyKeyBase64Str, 'base64');
let dataBlob = CryptoHelper.strToDataBlob(str1, 'utf-8'); //待加密数据

let encryptDataBlob1 = await DES.encryptECB(dataBlob, symKey); //加密
let encryptStr1 = CryptoHelper.dataBlobToStr(encryptDataBlob1, 'utf-8');
LogUtil.error(`加密（ECB模式）,异步：${encryptStr1}`);

let encryptDataBlob2 = DES.encryptECBSync(dataBlob, symKey); //加密
let encryptStr2 = CryptoHelper.dataBlobToStr(encryptDataBlob2, 'utf-8');
LogUtil.error(`加密（ECB模式）,同步：${encryptStr2}`);
```

##### decryptECB decryption (ECB mode)

```
let str1 = "鸿蒙技术交流QQ群：1029219059";

let smyKeyBase64Str = "bZen8i4KBFVMlomHBNWeExvFydWEXspO"; //base64符串密钥
let symKey = CryptoUtil.getConvertSymKeySync('3DES192', smyKeyBase64Str, 'base64');
let dataBlob = CryptoHelper.strToDataBlob(str1, 'utf-8'); //待加密数据

let encryptDataBlob1 = await DES.encryptECB(dataBlob, symKey); //加密
let decryptDataBlob1 = await DES.decryptECB(encryptDataBlob1, symKey); //解密
let decryptStr1 = CryptoHelper.dataBlobToStr(decryptDataBlob1, 'utf-8');
LogUtil.error(`解密（ECB模式）,异步：${decryptStr1}`);

let encryptDataBlob2 = DES.encryptECBSync(dataBlob, symKey); //加密
let decryptDataBlob2 = DES.decryptECBSync(encryptDataBlob2, symKey); //解密
let decryptStr2 = CryptoHelper.dataBlobToStr(decryptDataBlob2, 'utf-8');
LogUtil.error(`解密（ECB模式）,同步：${decryptStr2}`);
```

##### encryptCBC encryption (CBC mode)

```
let ivParams = CryptoUtil.generateIvParamsSpec();

let str2 = "harmony-utils，一款高效的HarmonyOS工具包，封装了常用工具类，提供一系列简单易用的方法。帮助开发者快速构建鸿蒙应用。";

let smyKeyBase64Str = "bZen8i4KBFVMlomHBNWeExvFydWEXspO"; //base64符串密钥
let symKey = CryptoUtil.getConvertSymKeySync('3DES192', smyKeyBase64Str, 'base64');
let dataBlob = CryptoHelper.strToDataBlob(str2, 'utf-8'); //待加密数据

let encryptDataBlob1 = await DES.encryptCBC(dataBlob, symKey, ivParams); //加密
let encryptStr1 = CryptoHelper.dataBlobToStr(encryptDataBlob1, 'utf-8');
LogUtil.error(`加密（CBC模式）,异步：${encryptStr1}`);

let encryptDataBlob2 = DES.encryptCBCSync(dataBlob, symKey, ivParams); //加密
let encryptStr2 = CryptoHelper.dataBlobToStr(encryptDataBlob2, 'utf-8');
LogUtil.error(`加密（CBC模式）,同步：${encryptStr2}`);
```

##### decryptCBC decryption (CBC mode)

```
let ivParams = CryptoUtil.generateIvParamsSpec();

let str2 = "harmony-utils，一款高效的HarmonyOS工具包，封装了常用工具类，提供一系列简单易用的方法。帮助开发者快速构建鸿蒙应用。";

let smyKeyBase64Str = "bZen8i4KBFVMlomHBNWeExvFydWEXspO"; //base64符串密钥
let symKey = CryptoUtil.getConvertSymKeySync('3DES192', smyKeyBase64Str, 'base64');
let dataBlob = CryptoHelper.strToDataBlob(str2, 'utf-8'); //待加密数据

let encryptDataBlob1 = await DES.encryptCBC(dataBlob, symKey, ivParams); //加密
let decryptDataBlob1 = await DES.decryptCBC(encryptDataBlob1, symKey, ivParams); //解密
let decryptStr1 = CryptoHelper.dataBlobToStr(decryptDataBlob1, 'utf-8');
LogUtil.error(`解密（CBC模式）,异步：${decryptStr1}`);

let encryptDataBlob2 = DES.encryptCBCSync(dataBlob, symKey, ivParams); //加密
let decryptDataBlob2 = DES.decryptCBCSync(encryptDataBlob2, symKey, ivParams); //解密
let decryptStr2 = CryptoHelper.dataBlobToStr(decryptDataBlob2, 'utf-8');
LogUtil.error(`解密（CBC模式）,同步：${decryptStr2}`);
```

##### encrypt encryption

```
let ivParams = CryptoUtil.generateIvParamsSpec();

let str1 = "鸿蒙技术交流QQ群：1029219059";

let smyKeyHexStr = "f1f8d34a21fd62ffb128b1ada4fd8f0758123e7d442b6273"; //16进制字符串密钥
let symKey = await CryptoUtil.getConvertSymKey('3DES192', smyKeyHexStr, 'hex');
let dataBlob = CryptoHelper.strToDataBlob(str1, 'utf-8'); //待加密数据

let encryptDataBlob1 = await DES.encrypt(dataBlob, symKey, ivParams, '3DES192|OFB|PKCS7'); //加密
let encryptStr1 = CryptoHelper.dataBlobToStr(encryptDataBlob1, 'utf-8');
LogUtil.error(`加密（OFB模式）,异步：${encryptStr1}`);

let encryptDataBlob2 = DES.encryptSync(dataBlob, symKey, ivParams, '3DES192|OFB|PKCS7'); //加密
let encryptStr2 = CryptoHelper.dataBlobToStr(encryptDataBlob2, 'utf-8');
LogUtil.error(`加密（OFB模式）,同步：${encryptStr2}`);
```

##### decrypt

```
let ivParams = CryptoUtil.generateIvParamsSpec();

let str1 = "鸿蒙技术交流QQ群：1029219059";

let smyKeyHexStr = "f1f8d34a21fd62ffb128b1ada4fd8f0758123e7d442b6273"; //16进制字符串密钥
let symKey = await CryptoUtil.getConvertSymKey('3DES192', smyKeyHexStr, 'hex');
let dataBlob = CryptoHelper.strToDataBlob(str1, 'utf-8'); //待加密数据

let encryptDataBlob1 = await DES.encrypt(dataBlob, symKey, ivParams, '3DES192|OFB|PKCS7'); //加密
let decryptDataBlob1 = await DES.decrypt(encryptDataBlob1, symKey, ivParams, '3DES192|OFB|PKCS7'); //解密
let decryptStr1 = CryptoHelper.dataBlobToStr(decryptDataBlob1, 'utf-8');
LogUtil.error(`解密（OFB模式）,异步：${decryptStr1}`);

let encryptDataBlob2 = DES.encryptSync(dataBlob, symKey, ivParams, '3DES192|OFB|PKCS7'); //加密
let decryptDataBlob2 = DES.decryptSync(encryptDataBlob2, symKey, ivParams, '3DES192|OFB|PKCS7'); //解密
let decryptStr2 = CryptoHelper.dataBlobToStr(decryptDataBlob2, 'utf-8');
LogUtil.error(`解密（OFB模式）,同步：${decryptStr2}`);
```

## Creation is not easy, please give Elder Tong a thumbs up 👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   
