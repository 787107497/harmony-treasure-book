# harmony-utils之SM3，SM3工具类

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


## SM3 算法简介

------
SM3是中国国家密码管理局2010年发布的商用密码杂凑算法标准（GM/T 0004-2012），输出256位固定长度哈希值，安全强度与SHA-256相当。该算法采用Merkle-Damgard结构设计，通过消息填充、分组扩展及32轮迭代压缩实现数据混淆，具备抗碰撞攻击和原像攻击能力。作为国产密码体系核心组件，SM3广泛应用于数字签名、电子认证、金融支付及物联网安全等领域，并已纳入ISO/IEC 10118-3国际标准。其高效性适配普通计算机与嵌入式设备，支撑了30余项国内密码行业标准的制定。

## SM3 应用场景

------
数字签名：与SM2非对称算法配合使用，对电子合同、政务文件等生成哈希摘要并签名，确保数据完整性和不可抵赖性；   
金融安全：用于网上银行交易验证、支付报文完整性保护，国内超80%金融机构在关键系统中部署该算法；   
物联网认证：为智能设备通信数据生成消息认证码（HMAC-SM3），防止工业级SSD、智能电网等场景的数据篡改；   
密码协议基础：支撑SSL/TLS、VPN等安全协议的密钥派生与校验，满足国产化替代需求。   


## API方法与使用

------

##### digest  SM3摘要

```
let str1 = "鸿蒙技术交流QQ群：1029219059";

let digest1 = await SM3.digest(str1);
LogUtil.error(`摘要，异步: ${digest1}`);

let digest2 = SM3.digestSync(str1,'hex');
LogUtil.error(`摘要，同步1: ${digest2}`);

let digest3 = SM3.digestSync(str1, 'base64');
LogUtil.error(`摘要，同步2:  ${digest3}`);
```

##### digestSegment  SM3分段摘要

```
let str3 = "harmony-utils，一款高效的HarmonyOS工具包，封装了常用工具类，提供一系列简单易用的方法。帮助开发者快速构建鸿蒙应用。";

let digest1 = await SM3.digestSegment(str3);
LogUtil.error(`分段摘要，异步: ${digest1}`);

let digest2 = SM3.digestSegmentSync(str3);
LogUtil.error(`分段摘要，同步1: ${digest2}`);

let digest3 = SM3.digestSegmentSync(str3, 'base64', 256);
LogUtil.error(`分段摘要，同步2: ${digest3}`);
```

##### hmac  SM3消息认证码计算

```
let str1 = "鸿蒙技术交流QQ群：1029219059";
let symKey = CryptoUtil.generateSymKeySync("HMAC|SM3");

let digest1 = await SM3.hmac(str1, symKey);
LogUtil.error(`消息认证码计算，异步: ${digest1}`);

let digest2 = SM3.hmacSync(str1, symKey);
LogUtil.error(`消息认证码计算，同步1: ${digest2}`);

let digest3 = SM3.hmacSync(str1, symKey, 'base64');
LogUtil.error(`消息认证码计算，同步2: ${digest3}`);
```

##### hmacSegment  SM3消息认证码计算，分段

```
let str2 = "harmony-utils，一款高效的HarmonyOS工具包，封装了常用工具类，提供一系列简单易用的方法。帮助开发者快速构建鸿蒙应用。";
let symKey = CryptoUtil.generateSymKeySync("HMAC|SM3");

let digest1 = await SM3.hmacSegment(str2, symKey);
LogUtil.error(`分段消息认证码计算，异步: ${digest1}`);

let digest2 = SM3.hmacSegmentSync(str2, symKey);
LogUtil.error(`分段消息认证码计算，同步1: ${digest2}`);

let digest3 = SM3.hmacSegmentSync(str2, symKey, 'hex', 256);
LogUtil.error(`分段消息认证码计算，同步2: ${digest3}`);
```

## 创作不易，请给童长老点赞👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   
