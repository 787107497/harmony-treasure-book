# harmony-utils之DES，DES加解密

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

## DES 算法简介

------
DES（数据加密标准）作为 1977 年美国发布的首个标准化对称分组加密算法，采用 64 位分组、56 位有效密钥（含 8 位校验位）及 16 轮 Feistel 迭代结构，通过扩展置换、S 盒非线性变换和 P 盒置换实现加密。其核心基于 Feistel 网络，将明文分为左右两部分迭代处理，每轮通过子密钥与轮函数运算增强混淆扩散。
但 DES 存在显著安全缺陷：56 位密钥空间仅 2⁵⁶种组合，1999 年被证实可通过 2500 台计算机在 22 小时内暴力破解，且存在弱密钥（如全 0 密钥）使加密解密等价，难以抵御差分 / 线性密码分析。2001 年其被 AES 取代，过渡方案 3DES 通过三重加密将密钥长度提升至 112/168 位，曾用于金融 POS 机等场景。
DES 的历史价值在于推动加密技术标准化，奠定 Feistel 结构理论基础，至今仍是密码学教学的经典案例。尽管在主流领域已淘汰，但其设计思想为现代对称加密算法（如 AES）提供了重要参考。


## API方法与使用

------

##### generateSymKey  生成对称密钥SymKey

```
let symKey1 = await DES.generateSymKey();
let symKeyStr1 = CryptoHelper.dataBlobToStr(symKey1.getEncoded(), 'hex');
LogUtil.error(`对称密钥1：${symKeyStr1}`);

let symKey2 = DES.generateSymKeySync();
let symKeyStr2 = CryptoHelper.dataBlobToStr(symKey2.getEncoded(), 'base64');
LogUtil.error(`对称密钥2：${symKeyStr2}`);
```

##### encryptECB  加密（ECB模式）

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

##### decryptECB  解密（ECB模式）

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

##### encryptCBC  加密（CBC模式）

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

##### decryptCBC  解密（CBC模式）

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

##### encrypt  加密

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

##### decrypt  解密

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

## 创作不易，请给童长老点赞👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   
