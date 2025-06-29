# Harmony-utils SM2, SM2 encryption and decryption

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


## Introduction to SM2 algorithm

------
SM2 is an elliptic curve public key cryptography algorithm released by the State Cryptography Administration in 2010, and is a core component of my country's commercial cryptography system. The algorithm is based on elliptic curve cryptography (ECC), adopts a 256-bit key length, which is equivalent to RSA-3072 in terms of security, but has higher computing efficiency and lower computing resource consumption.
As an asymmetric algorithm, SM2 supports three major functions: digital signature, key exchange, and public key encryption. Its security depends on the difficulty of discrete logarithmic problems of elliptic curves and can withstand brute-force cracking and quantum computing threats. Compared with RSA algorithm, SM2 has shorter keys and faster signature speeds under the same security strength. It has been widely used in financial payments, electronic certification, government affairs systems and Internet of Things security, and has become an integral part of the international standard ISO/IEC 14888-3.

## SM2 application scenarios

------
SM2 algorithm has a wide range of applications in key areas such as finance, government affairs, and electricity in my country. For example, in online banking and electronic payment scenarios in the financial field, it is used to ensure the secure transmission and integrity protection of user identity authentication, transaction data; in the electronic document transmission and government system login in the government field, it is used to ensure the security and reliability of government information.
In practical applications, the SM2 algorithm is usually used in conjunction with national secret algorithms such as SM3 and SM4. Generally, SM4 is used to encrypt the data content, SM3 is used to digest the content, and then SM2 is used to sign the digest. The receiving end first uses SM2 to verify the digest. After the verification is successful, the sent content will be SM3 to check whether the generated digest and the digest after verification are consistent to prevent tampering.


## API methods and usage

------

##### generateKeyPair generates asymmetric key KeyPair

```
let keyPair = SM2.generateKeyPairSync();
let pubKey = keyPair.pubKey; //公钥
let priKey = keyPair.priKey; //私钥
let pubKeyStr = CryptoHelper.dataBlobToStr(pubKey.getEncoded(), 'base64'); //将公钥转换成base64字符串。
LogUtil.error(`pubKeyStr2: ${pubKeyStr}`);
let priKeyStr = CryptoHelper.dataBlobToStr(priKey.getEncoded(), 'base64'); //将私钥转换成base64符符串。
LogUtil.error(`priKeyStr2: ${priKeyStr}`);
```

##### getConvertKeyPair Get the converted asymmetric key KeyPair

```
let pubKeyStr = "3059301306072a8648ce3d020106082a811ccf5501822d034200045417bebc296d14ebed6b6d0298019935677c5a8549150adf82e5c51f567066a7e8186915b10d3a8f0c544b2c03ee39ff3063125b53b906cc4da2232ae127c178"; //16进制字符串密钥
let priKeyStr = "3031020101042035ae8b8faec0e80e64b26d5239d60c7a694aaa84bd106ed12f4600d9fe2cbd09a00a06082a811ccf5501822d"; //16进制字符串密钥
let keyPair = await SM2.getConvertKeyPair(pubKeyStr, priKeyStr, 'hex');
let pubKey = keyPair.pubKey; //公钥
let priKey = keyPair.priKey; //私钥
let pubKeyStr3 = CryptoHelper.dataBlobToStr(pubKey.getEncoded(), 'hex'); //将公钥转换成16进制字符串。
LogUtil.error(`pubKeyStr3: ${pubKeyStr3}`);
let priKeyStr3 = CryptoHelper.dataBlobToStr(priKey.getEncoded(), 'hex'); //将私钥转换成16进制字符串。
LogUtil.error(`priKeyStr3: ${priKeyStr3}`);
```

##### getSM2PubKey gets the convert SM2 public key, converts the SM2 public key in C1C2C3 format to the ASN.1 format required by Hongmeng

```
//16进制的C1C2C3格式的SM2公钥
let pubKeyStr = "04FB40A51A9D6E9333A73B3633BA72B0989BD69F54420108E7036C8FA0E6C6142C422F70D75063AC98EC9E2D2CB82B847C51979A1485DAB5573ABCC0FC69B5988E";
let pubKey = SM2.getSM2PubKey(pubKeyStr); //将16进制的C1C2C3格式的SM2公钥转换为鸿蒙所需的ASN.1格式公钥
let pubKeyStr1 = CryptoHelper.dataBlobToStr(pubKey.getEncoded(), 'hex'); //将公钥转换成16进制字符串。
LogUtil.error(`转换后的公钥: ${pubKeyStr1}`);
```

##### getSM2PriKey gets the convert SM2 private key

```
let priKeyStr="6330B599ECD23ABDC74B9A5B7B5E00E553005F72743101C5FAB83AEB579B7074";
let priKey = SM2.getSM2PriKey(priKeyStr);
let priKeyStr1 = CryptoHelper.dataBlobToStr(priKey.getEncoded(), 'hex'); //将私钥转换成base64符符串。
LogUtil.error(`转换后的私钥: ${priKeyStr1}`);
```

##### encrypt encryption

```
let pubKeyStr = "MFkwEwYHKoZIzj0CAQYIKoEcz1UBgi0DQgAEYIZ4YCxXfIKvy3Fzmpl43hk7ojUsZqoZyww1YYtw4bICcaD/KmKy+OO4bMTnbrjbjNfJQaVApDTOW9a+PvazXQ=="; //base64字符串公钥
let priKeyStr = "MDECAQEEIKu8PGHEU4Wxiw6xwb0loj0NVLlR7vGe5jYgan8u+hKboAoGCCqBHM9VAYIt"; //base64字符串私钥
let keyPair = SM2.getConvertKeyPairSync(pubKeyStr, priKeyStr, 'base64');

let msg = "鸿蒙技术交流QQ群：1029219059"; //待加密字符串
let msgDataBlob = CryptoHelper.strToDataBlob(msg, 'utf-8');
let encryptDataBlob = await SM2.encrypt(msgDataBlob, keyPair!.pubKey); //加密
let encryptStr = CryptoHelper.dataBlobToStr(encryptDataBlob, 'utf-8');
LogUtil.error(`加密后: ${encryptStr}`);
```

##### decrypt

```
let pubKeyStr = "MFkwEwYHKoZIzj0CAQYIKoEcz1UBgi0DQgAEYIZ4YCxXfIKvy3Fzmpl43hk7ojUsZqoZyww1YYtw4bICcaD/KmKy+OO4bMTnbrjbjNfJQaVApDTOW9a+PvazXQ=="; //base64字符串公钥
let priKeyStr = "MDECAQEEIKu8PGHEU4Wxiw6xwb0loj0NVLlR7vGe5jYgan8u+hKboAoGCCqBHM9VAYIt"; //base64字符串私钥
let keyPair = SM2.getConvertKeyPairSync(pubKeyStr, priKeyStr, 'base64');

let msg = "鸿蒙技术交流QQ群：1029219059"; //待加密字符串
let msgDataBlob = CryptoHelper.strToDataBlob(msg, 'utf-8');
let encryptDataBlob = await SM2.encrypt(msgDataBlob, keyPair!.pubKey); //加密
let decryptDataBlob = await SM2.decrypt(encryptDataBlob, keyPair!.priKey); //解密
let decryptStr = CryptoHelper.dataBlobToStr(decryptDataBlob, 'utf-8');
LogUtil.error(`加解密后: ${decryptStr}`);
```

##### getCipherTextSpec Get the conversion SM2 ciphertext format, ASN.1 format to C1C2C3 or C1C3C2

```
let pubKeyStr = "MFkwEwYHKoZIzj0CAQYIKoEcz1UBgi0DQgAEYIZ4YCxXfIKvy3Fzmpl43hk7ojUsZqoZyww1YYtw4bICcaD/KmKy+OO4bMTnbrjbjNfJQaVApDTOW9a+PvazXQ=="; //base64字符串公钥
let priKeyStr = "MDECAQEEIKu8PGHEU4Wxiw6xwb0loj0NVLlR7vGe5jYgan8u+hKboAoGCCqBHM9VAYIt"; //base64字符串私钥
let keyPair = SM2.getConvertKeyPairSync(pubKeyStr, priKeyStr, 'base64');

let msg = "鸿蒙技术交流QQ群：1029219059"; //待加密字符串
let msgDataBlob = CryptoHelper.strToDataBlob(msg, 'utf-8');
let encryptDataBlob = SM2.encryptSync(msgDataBlob, keyPair!.pubKey); //加密
let c1c2c3Str = SM2.getCipherTextSpec(encryptDataBlob, 0); //转换密文
LogUtil.error(`C1C2C3密文: ${c1c2c3Str}`);
let c1c3c2Str = SM2.getCipherTextSpec(encryptDataBlob, 1); //转换密文
LogUtil.error(`C1C3C2密文: ${c1c3c2Str}`);
```

##### sign Sign the data

```
let pubKeyStr = "MFkwEwYHKoZIzj0CAQYIKoEcz1UBgi0DQgAEYIZ4YCxXfIKvy3Fzmpl43hk7ojUsZqoZyww1YYtw4bICcaD/KmKy+OO4bMTnbrjbjNfJQaVApDTOW9a+PvazXQ=="; //base64字符串公钥
let priKeyStr = "MDECAQEEIKu8PGHEU4Wxiw6xwb0loj0NVLlR7vGe5jYgan8u+hKboAoGCCqBHM9VAYIt"; //base64字符串私钥
let keyPair = SM2.getConvertKeyPairSync(pubKeyStr, priKeyStr, 'base64');

let msg = "harmony-utils，一款高效的HarmonyOS工具包，封装了常用工具类，提供一系列简单易用的方法。帮助开发者快速构建鸿蒙应用。";
let dataBlob = CryptoHelper.strToDataBlob(msg, 'utf-8');
let signDataBlob =await SM2.sign(dataBlob, keyPair!.priKey);
let signStr = CryptoHelper.dataBlobToStr(signDataBlob, 'hex');
LogUtil.error(`签名，异步: ${signStr}`);
```

##### verify the data verification

```
let pubKeyStr = "MFkwEwYHKoZIzj0CAQYIKoEcz1UBgi0DQgAEYIZ4YCxXfIKvy3Fzmpl43hk7ojUsZqoZyww1YYtw4bICcaD/KmKy+OO4bMTnbrjbjNfJQaVApDTOW9a+PvazXQ=="; //base64字符串公钥
let priKeyStr = "MDECAQEEIKu8PGHEU4Wxiw6xwb0loj0NVLlR7vGe5jYgan8u+hKboAoGCCqBHM9VAYIt"; //base64字符串私钥
let keyPair = SM2.getConvertKeyPairSync(pubKeyStr, priKeyStr, 'base64');

let msg = "harmony-utils，一款高效的HarmonyOS工具包，封装了常用工具类，提供一系列简单易用的方法。帮助开发者快速构建鸿蒙应用。";
let dataBlob = CryptoHelper.strToDataBlob(msg, 'utf-8');
let signDataBlob =await SM2.sign(dataBlob, keyPair!.priKey);

let verify = await SM2.verify(dataBlob, signDataBlob, keyPair!.pubKey);
LogUtil.error(`验签，异步: ${verify}`);
```

##### signSegment Signs the data in segmentation

```
let pubKeyStr = "MFkwEwYHKoZIzj0CAQYIKoEcz1UBgi0DQgAEYIZ4YCxXfIKvy3Fzmpl43hk7ojUsZqoZyww1YYtw4bICcaD/KmKy+OO4bMTnbrjbjNfJQaVApDTOW9a+PvazXQ=="; //base64字符串公钥
let priKeyStr = "MDECAQEEIKu8PGHEU4Wxiw6xwb0loj0NVLlR7vGe5jYgan8u+hKboAoGCCqBHM9VAYIt"; //base64字符串私钥
let keyPair = SM2.getConvertKeyPairSync(pubKeyStr, priKeyStr, 'base64');

let dataStr = "harmony-utils，一款高效的HarmonyOS工具包，封装了常用工具类，提供一系列简单易用的方法。帮助开发者快速构建鸿蒙应用。gitee地址：https://gitee.com/tongyuyan/harmony-utils。github主页地址：https://github.com/787107497。";
let data = CryptoHelper.strToUint8Array(dataStr, 'utf-8');
let signDataBlob = await SM2.signSegment(data, keyPair!.priKey);
let signStr = CryptoHelper.dataBlobToStr(signDataBlob, 'base64');
LogUtil.error(`分段签名，异步: ${signStr}`);
```

##### verifySegment performs segmented verification of data

```
let pubKeyStr = "MFkwEwYHKoZIzj0CAQYIKoEcz1UBgi0DQgAEYIZ4YCxXfIKvy3Fzmpl43hk7ojUsZqoZyww1YYtw4bICcaD/KmKy+OO4bMTnbrjbjNfJQaVApDTOW9a+PvazXQ=="; //base64字符串公钥
let priKeyStr = "MDECAQEEIKu8PGHEU4Wxiw6xwb0loj0NVLlR7vGe5jYgan8u+hKboAoGCCqBHM9VAYIt"; //base64字符串私钥
let keyPair = SM2.getConvertKeyPairSync(pubKeyStr, priKeyStr, 'base64');

let dataStr = "harmony-utils，一款高效的HarmonyOS工具包，封装了常用工具类，提供一系列简单易用的方法。帮助开发者快速构建鸿蒙应用。gitee地址：https://gitee.com/tongyuyan/harmony-utils。github主页地址：https://github.com/787107497。";
let data = CryptoHelper.strToUint8Array(dataStr, 'utf-8');
let signDataBlob = await SM2.signSegment(data, keyPair!.priKey);

let verify = await SM2.verifySegment(data, signDataBlob, keyPair!.pubKey);
LogUtil.error(`分段验签，异步: ${verify}`);
```

## Creation is not easy, please give Elder Tong a thumbs up 👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   



