# harmony-utils之SM4，SM4加解密

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


## SM4 算法简介

------
SM4是中国自主研发的商用对称加密算法，由国家密码管理局于2006年发布，2012年成为国家密码行业标准（GM/T 0002-2012）。该算法采用128位分组长度和128位密钥长度，通过32轮非线性迭代结构实现数据加密，安全强度与AES-128相当。其核心设计包含S盒替换、循环移位等操作，支持ECB、CBC等标准工作模式。作为中国密码体系（SM系列）的核心组件，SM4广泛应用于金融支付、电子政务、物联网等领域，满足国产密码合规要求。算法具备高效软硬件实现特性，并已通过ISO/IEC国际标准认证（18033-3），成为我国信息安全领域的重要基础算法。

## SM4 应用场景

------
金融支付：在银行卡交易、移动支付及网上银行中加密敏感数据（如交易金额、账户信息），确保传输安全并符合中国金融行业密码合规要求；   
电子政务：用于电子身份证、政务系统数据传输加密，结合SM2签名算法实现身份认证与数据完整性保护；   
物联网安全：加密智能设备间的通信数据，防止工业级SSD、智能家居等场景下的数据泄露；   
信创国产化替代：在信息技术应用创新项目中替代AES算法，满足党政机关和关键基础设施的自主可控需求。


## API方法与使用

------

##### generateSymKey  生成对称密钥SymKey

```
let symKey1 = await SM4.generateSymKey();
let symKeyStr1 = CryptoHelper.dataBlobToStr(symKey1.getEncoded(), 'hex');
LogUtil.error(`对称密钥1：${symKeyStr1}`);

let symKey2 = SM4.generateSymKeySync();
let symKeyStr2 = CryptoHelper.dataBlobToStr(symKey2.getEncoded(), 'base64');
LogUtil.error(`对称密钥2：${symKeyStr2}`);
```

##### encryptGCM  加密（GCM模式）

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

##### decryptGCM  解密（GCM模式）

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

##### encryptCBC  加密（CBC模式）

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

##### decryptCBC  解密（CBC模式）

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

##### encryptECB  加密（ECB模式）

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

##### decryptECB  解密（ECB模式）

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

##### encryptGCMSegment  加密（GCM模式）分段

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

##### decryptGCMSegment  解密（GCM模式）分段

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

## 创作不易，请给童长老点赞👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   
