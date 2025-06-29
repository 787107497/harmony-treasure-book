# harmony-utils之RSA，RSA加解密

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


## RSA 算法简介

------
RSA是1977年提出的非对称加密算法，基于大数分解难题设计，密钥分为公钥(e,n)和私钥(d,n)，其中n为两质数乘积，d是e的模逆元。加密时将明文m通过c=m^e mod n生成密文，解密则用m=c^d mod n。其安全性依赖分解大数n的计算复杂度，常用于HTTPS密钥传输、数字签名等场景。但因计算效率低，不适合加密大量数据，且1024位密钥已可被量子计算威胁，现推荐2048位以上密钥，是公钥加密体系的开创性算法。

## RSA 应用场景

------
RSA作为非对称加密算法，核心应用于需公钥验证、私钥保密的场景。网络通信中，HTTPS用其加密对称会话密钥，PGP加密邮件；数字签名领域，涵盖软件代码签名、区块链交易认证及电子文档签章；密钥管理上，支持SSH无密码登录与VPN密钥协商；金融场景中，银行U盾、CA证书体系依赖其实现身份验证与抗抵赖性。虽计算开销大，不适合海量数据加密，但在密钥安全传输和签名认证中不可或缺，是互联网安全体系的基础算法。


## API方法与使用

------

##### generateKeyPair  生成非对称密钥KeyPair

```
let keyPair1 = await RSA.generateKeyPair();
let pubKeyStr1 = CryptoHelper.dataBlobToStr(keyPair1.pubKey.getEncoded(), 'hex'); //将公钥转换成base64字符串。
LogUtil.error(`pubKeyStr1: ${pubKeyStr1}`);
let priKeyStr1 = CryptoHelper.dataBlobToStr(keyPair1.priKey.getEncoded(), 'hex'); //将私钥转换成base64符符串。
LogUtil.error(`priKeyStr1: ${priKeyStr1}`);
```

##### getConvertKeyPair  获取转换的非对称密钥KeyPair

```
let pubKeyStr = "MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQDDUpsnavHoapoKtOOM9NKqTt6BpPe07ZzxhMcLAm5dtFQ6zRyJwT3czHGnh1BM2FATvLTDGLkmKc/Ww27//lFbrbqBE19R/5y8UPRpbUdACZ28yqzdiaquovUndhTH/CnLzcPM7VnWO0gp3/kbg5WizkZtUTRHL+Nu4OHbbesO1wIDAQAB"; //base64字符串密钥
let priKeyStr = "MIICdgIBADANBgkqhkiG9w0BAQEFAASCAmAwggJcAgEAAoGBAMNSmydq8ehqmgq044z00qpO3oGk97TtnPGExwsCbl20VDrNHInBPdzMcaeHUEzYUBO8tMMYuSYpz9bDbv/+UVutuoETX1H/nLxQ9GltR0AJnbzKrN2Jqq6i9Sd2FMf8KcvNw8ztWdY7SCnf+RuDlaLORm1RNEcv427g4dtt6w7XAgMBAAECgYANvgsii9i3VIDADhgQe80ypFftYTD4btti9seWU7Z2K1Ddzj6axpjWpx+7/L4+md2Qde915pBoSfrQjnGJ21fX7vpqOVdDWS7lseYfM50z8ZMpZewxJNBkSGYQEazMYDfyCFMjZmB4guf/uu0B2JN/YtA8Ed7JJlkXmVLh4ReYSQJBAOIhzozpcIuGOBjylQdN+MokiL14gnAh6hiwnusD9JlTSJbQonUXkhikaf0WphxBVPSngZDdi3FYla/CDUAScBMCQQDdHwsJZ1oShtbJltaUCEsJHTWLwYm8V8tTOpHGJU8/u1mBK3pVZlwnfzzrj2oLl5iBpMHF197TPNi5gjrjM6atAkA/4pMrBixQjqu8iJQHy0R1P1sORER9j2dGcGeFN8nbo0bHrMuozu7sXU7APKzTILXypHwbRCvH6uHnFKiPqGXXAkAUsjEgQjImBcTYvWt8E4Kiab93QzgXDsiTE6pNN3TBbFGmS2F52MjLUZdsHNI6H4hAqiEQ2XGbp9hJFK1aUp1JAkEAjP4fbqrAUjGiG+EbjEffV625kACb6q9Wz+vbspMPqcr5TU2AxxSW65Yilq4pKYq8O+qXnVdOpX7DjrWA1kg2JA=="; //base64字符串密钥
let keyPair1 = await RSA.getConvertKeyPair(pubKeyStr, priKeyStr, 'base64');
let keyPair2 = RSA.getConvertKeyPairSync(pubKeyStr, priKeyStr, 'base64');
```

##### encrypt  加密

```
let keyPair1 = await RSA.generateKeyPair(); //生成密钥

let str1 = "鸿蒙技术交流QQ群：1029219059";
let dataBlob = CryptoHelper.strToDataBlob(str1, 'utf-8'); //待加密数据

let encryptDataBlob = await RSA.encrypt(dataBlob, keyPair1.pubKey); //加密
let encryptStr = CryptoHelper.dataBlobToStr(encryptDataBlob, 'utf-8');
LogUtil.error(`加密，异步：${encryptStr}`);
```

##### decrypt  解密

```
let keyPair1 = await RSA.generateKeyPair(); //生成密钥

let str1 = "鸿蒙技术交流QQ群：1029219059";
let dataBlob = CryptoHelper.strToDataBlob(str1, 'utf-8'); //待加密数据

let encryptDataBlob = await RSA.encrypt(dataBlob, keyPair1.pubKey); //加密
let decryptDataBlob = await RSA.decrypt(encryptDataBlob, keyPair1.priKey); //解密
let decryptStr = CryptoHelper.dataBlobToStr(decryptDataBlob, 'utf-8');
LogUtil.error(`解密，异步：${decryptStr}`);or(`加解密，同步：${decryptStr2}`);
```

##### encryptSegment  加密,分段

```
let keyPair1 = await RSA.generateKeyPair("RSA1024|PRIMES_2"); //生成密钥

let str2 = "harmony-utils，一款高效的HarmonyOS工具包，封装了常用工具类，提供一系列简单易用的方法。帮助开发者快速构建鸿蒙应用。";
let dataBlob = CryptoHelper.strToDataBlob(str2, 'utf-8'); //待加密数据

let encryptDataBlob = await RSA.encryptSegment(dataBlob, keyPair1.pubKey, 'RSA2048|PKCS1'); //加密
let encryptStr = CryptoHelper.dataBlobToStr(encryptDataBlob, 'utf-8');
LogUtil.error(`分段加密，异步：${encryptStr}`);
```

##### decryptSegment  解密,分段

```
let keyPair1 = await RSA.generateKeyPair("RSA1024|PRIMES_2"); //生成密钥

let str2 = "harmony-utils，一款高效的HarmonyOS工具包，封装了常用工具类，提供一系列简单易用的方法。帮助开发者快速构建鸿蒙应用。";
let dataBlob = CryptoHelper.strToDataBlob(str2, 'utf-8'); //待加密数据

let encryptDataBlob = await RSA.encryptSegment(dataBlob, keyPair1.pubKey, 'RSA2048|PKCS1'); //加密
let decryptDataBlob = await RSA.decryptSegment(encryptDataBlob, keyPair1.priKey, 'RSA2048|PKCS1'); //解密
let decryptStr = CryptoHelper.dataBlobToStr(decryptDataBlob, 'utf-8');
LogUtil.error(`分段解密，异步：${decryptStr}`);
```

##### sign  对数据进行签名

```
let keyPair = await RSA.generateKeyPair(); //生成密钥

let str1 = "鸿蒙技术交流QQ群：1029219059";
let dataBlob = CryptoHelper.strToDataBlob(str1, 'utf-8');

let signDataBlob1 = await RSA.sign(dataBlob, keyPair.priKey);
let signStr1 = CryptoHelper.dataBlobToStr(signDataBlob1, 'hex');
LogUtil.error(`签名，异步: ${signStr1}`);
```

##### verify  对数据进行验签

```
let keyPair = await RSA.generateKeyPair(); //生成密钥

let str1 = "鸿蒙技术交流QQ群：1029219059";
let signDataBlob1 = await RSA.sign(dataBlob, keyPair.priKey);
let signStr1 = CryptoHelper.dataBlobToStr(signDataBlob1, 'hex');

let verify1 = await RSA.verify(dataBlob, signDataBlob1, keyPair!.pubKey);
LogUtil.error(`验签，异步: ${verify1}`);
```

##### signSegment  对数据进行分段签名

```
let keyPair1 = await RSA.generateKeyPair(); //生成密钥

let str3 = "harmony-utils，一款高效的HarmonyOS工具包，封装了常用工具类，提供一系列简单易用的方法。帮助开发者快速构建鸿蒙应用。gitee地址：https://gitee.com/tongyuyan/harmony-utils。github主页地址：https://github.com/787107497。";
let data = CryptoHelper.strToUint8Array(str3, 'utf-8')；

let signDataBlob = await RSA.signSegment(data, keyPair.priKey);
let signStr = CryptoHelper.dataBlobToStr(signDataBlob, 'base64');
LogUtil.error(`分段签名，异步: ${signStr}`);

```

##### verifySegment  对数据进行分段验签

```
let keyPair1 = await RSA.generateKeyPair(); //生成密钥

let str3 = "harmony-utils，一款高效的HarmonyOS工具包，封装了常用工具类，提供一系列简单易用的方法。帮助开发者快速构建鸿蒙应用。gitee地址：https://gitee.com/tongyuyan/harmony-utils。github主页地址：https://github.com/787107497。";
let data = CryptoHelper.strToUint8Array(str3, 'utf-8')；
let signDataBlob = await RSA.signSegment(data, keyPair.priKey);

let verify = await RSA.verifySegment(data, signDataBlob, keyPair.pubKey);
LogUtil.error(`分段验签，异步: ${verify}`);
```

##### recover  对数据进行签名恢复原始数据，目前仅RSA支持

```
let keyPair1 = await RSA.generateKeyPair(); //生成密钥

let str1 = "鸿蒙技术交流QQ群：1029219059";
let dataBlob = CryptoHelper.strToDataBlob(str1, 'utf-8');
let signDataBlob = RSA.signSync(dataBlob, keyPair.priKey, 'RSA1024|PKCS1|NoHash|OnlySign');

let recoverDataBlob = await RSA.recover(signDataBlob, keyPair.pubKey);
if (recoverDataBlob != null) {
  let recoverStr = CryptoHelper.dataBlobToStr(recoverDataBlob, 'utf-8');
  LogUtil.error(`签名恢复，异步: ${recoverStr}`);
} else {
  LogUtil.error(`签名恢复，异步: 恢复数据为空！`);
}
```

## 创作不易，请给童长老点赞👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   
