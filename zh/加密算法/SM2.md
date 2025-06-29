# harmony-utils之SM2，SM2加解密

## harmony-utils 简介与说明

------
[harmony-utils](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils) 一款功能丰富且极易上手的HarmonyOS工具库，借助众多实用工具类，致力于助力开发者迅速构建鸿蒙应用。其封装的工具涵盖了APP、设备、屏幕、授权、通知、线程间通信、弹框、吐司、生物认证、用户首选项、拍照、相册、扫码、文件、日志，异常捕获、字符、字符串、数字、集合、日期、随机、base64、加密、解密、JSON等一系列的功能和操作，能够满足各种不同的开发需求。    
[picker_utils](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fpicker_utils) 是harmony-utils拆分出来的一个子库，包含PickerUtil、PhotoHelper、ScanUtil。

下载安装  
`ohpm i @pura/harmony-utils`  
`ohpm i @pura/picker_utils`

 ```
  //全局初始化方法，在UIAbility的onCreate方法中初始化 AppUtil.init()
  onCreate(want: Want, launchParam: AbilityConstant.LaunchParam): void {
    AppUtil.init(this.context);
  }
 ```


## SM2 算法简介

------
SM2是由中国国家密码管理局于2010年发布的椭圆曲线公钥密码算法，属于我国商用密码体系的核心组成部分。该算法基于椭圆曲线密码学（ECC），采用256位密钥长度，在安全性上等同RSA-3072，但具有更高的运算效率和更低的计算资源消耗。
作为非对称算法，SM2支持‌数字签名‌、‌密钥交换‌和‌公钥加密‌三大功能，其安全性依赖于椭圆曲线离散对数问题的难解性，可抵御暴力破解和量子计算威胁。相较于RSA算法，SM2在相同安全强度下密钥更短、签名速度更快，已广泛应用于金融支付、电子认证、政务系统及物联网安全等领域，并成为国际标准ISO/IEC 14888-3的组成部分。

## SM2 应用场景

------
SM2 算法在我国的金融、政务、电力等关键领域有着广泛的应用。例如，在金融领域的网上银行、电子支付等场景中，用于保障用户身份认证、交易数据的安全传输和完整性保护；在政务领域的电子公文传输、政务系统登录等方面，确保政务信息的安全和可靠。
在实际应用中，SM2 算法通常会与 SM3、SM4 等国密算法配合使用。一般用 SM4 对数据内容进行加密，使用 SM3 对内容进行摘要，再使用 SM2 对摘要进行签名。接收端先用 SM2 对摘要进行验签，验签成功后，对发送过来的内容进行 SM3 摘要，查看生成的摘要和验签后的摘要是否一致，以防止篡改。


## API方法与使用

------

##### generateKeyPair  生成非对称密钥KeyPair

```
let keyPair = SM2.generateKeyPairSync();
let pubKey = keyPair.pubKey; //公钥
let priKey = keyPair.priKey; //私钥
let pubKeyStr = CryptoHelper.dataBlobToStr(pubKey.getEncoded(), 'base64'); //将公钥转换成base64字符串。
LogUtil.error(`pubKeyStr2: ${pubKeyStr}`);
let priKeyStr = CryptoHelper.dataBlobToStr(priKey.getEncoded(), 'base64'); //将私钥转换成base64符符串。
LogUtil.error(`priKeyStr2: ${priKeyStr}`);
```

##### getConvertKeyPair  获取转换的非对称密钥KeyPair

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

##### getSM2PubKey  获取转换SM2公钥, 将C1C2C3格式的SM2公钥转换为鸿蒙所需的ASN.1格式

```
//16进制的C1C2C3格式的SM2公钥
let pubKeyStr = "04FB40A51A9D6E9333A73B3633BA72B0989BD69F54420108E7036C8FA0E6C6142C422F70D75063AC98EC9E2D2CB82B847C51979A1485DAB5573ABCC0FC69B5988E";
let pubKey = SM2.getSM2PubKey(pubKeyStr); //将16进制的C1C2C3格式的SM2公钥转换为鸿蒙所需的ASN.1格式公钥
let pubKeyStr1 = CryptoHelper.dataBlobToStr(pubKey.getEncoded(), 'hex'); //将公钥转换成16进制字符串。
LogUtil.error(`转换后的公钥: ${pubKeyStr1}`);
```

##### getSM2PriKey  获取转换SM2私钥

```
let priKeyStr="6330B599ECD23ABDC74B9A5B7B5E00E553005F72743101C5FAB83AEB579B7074";
let priKey = SM2.getSM2PriKey(priKeyStr);
let priKeyStr1 = CryptoHelper.dataBlobToStr(priKey.getEncoded(), 'hex'); //将私钥转换成base64符符串。
LogUtil.error(`转换后的私钥: ${priKeyStr1}`);
```

##### encrypt  加密

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

##### decrypt  解密

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

##### getCipherTextSpec  获取转换SM2密文格式，ASN.1格式转换为C1C2C3或C1C3C2

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

##### sign  对数据进行签名

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

##### verify  对数据进行验签

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

##### signSegment  对数据进行分段签名

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

##### verifySegment  对数据进行分段验签

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

## 创作不易，请给童长老点赞👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   



