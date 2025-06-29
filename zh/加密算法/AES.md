# harmony-utils之AES，AES加解密

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

## AES 算法简介

------

AES（高级加密标准）是 NIST 于 2001 年发布的对称分组加密算法，用以替代 DES。它支持 128/192/256 位密钥，对应 10/12/14 轮加密，分组长度固定为 128 位。算法通过密钥扩展生成多轮子密钥，加密流程含字节替换、行移位、列混淆（末轮省略）和轮密钥加等操作，利用 S 盒非线性变换与矩阵运算实现混淆扩散，抵御差分分析等攻击。其优势在于对称加密效率高、密钥灵活性强，且硬件友好（如 AES - NI 指令集加速），广泛应用于 HTTPS、硬盘加密等场景，是当前主流安全加密标准。

## AES 应用场景

------

AES作为主流对称加密算法，因高安全性与效率广泛应用于多场景。网络通信中，HTTPS、VPN及加密通讯工具用其保障数据传输安全；数据存储领域，硬盘加密、数据库敏感字段保护及云文件加密均依赖AES；物联网中，智能家居、工业控制设备借其加密通信；移动设备系统与SIM卡通信亦用AES保障安全。此外，金融支付、电子政务、硬件加速（如AES - NI）等场景也离不开AES，它是信息安全领域的核心技术。

## API方法与使用

------

##### generateSymKey  生成对称密钥SymKey

```
let symKey1 = await AES.generateSymKey();
let symKeyStr1 = CryptoHelper.dataBlobToStr(symKey1.getEncoded(), 'hex');
LogUtil.error(`对称密钥1：${symKeyStr1}`);

let symKey2 = AES.generateSymKeySync();
let symKeyStr2 = CryptoHelper.dataBlobToStr(symKey2.getEncoded(), 'base64');
LogUtil.error(`对称密钥2：${symKeyStr2}`);
```

##### encryptGCM  加密（GCM模式）

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

##### decryptGCM  解密（GCM模式）

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

##### encryptCBC  加密（CBC模式）

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

##### decryptCBC  解密（CBC模式）

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

##### encryptECB  加密（ECB模式）

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

##### decryptECB  解密（ECB模式）

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

##### encryptGCMSegment  加密（GCM模式）分段

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

##### decryptGCMSegment  解密（GCM模式）分段

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

## 创作不易，请给童长老点赞👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   