# harmony-utils之SHA，SHA工具类

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


## SHA 算法简介

------
SHA（Secure Hash Algorithm）是由美国国家标准技术研究院（NIST）发布的密码散列函数家族，用于生成数据的唯一性摘要。   
其核心版本包括：   
SHA-1：160位摘要，曾广泛用于SSL/TLS和文件校验，但因碰撞漏洞（2017年实际攻击案例）已被淘汰。   
SHA-2：（含SHA-256/384/512）：采用分块压缩结构，抗碰撞性强，现为区块链（如比特币）和数字证书的主流选择。   
SHA-3：基于海绵结构的新一代算法，设计上区别于SHA-2，具备抗量子计算潜力。   

## SHA 应用场景

------
数据完整性校验：验证文件传输是否被篡改；
数字签名：与公钥加密结合实现身份认证（SHA-256替代SHA-1成为主流）；
密码存储：系统存储用户密码的哈希值而非明文（需结合盐值增强安全）。


## API方法与使用

------

##### digest  SHA摘要

```
let str1 = "鸿蒙技术交流QQ群：1029219059";

let digest1 = await SHA.digest(str1);
LogUtil.error(`摘要，异步: ${digest1}`);

let digest2 = SHA.digestSync(str1);
LogUtil.error(`摘要，同步: ${digest2}`);

let digest3 = SHA.digestSync(str1, 'SHA512');
LogUtil.error(`摘要:\t ${digest3}`);

let digest4 = SHA.digestSync(str1, 'SHA512', 'base64');
LogUtil.error(`摘要:\t ${digest4}`);
```

##### digestSegment  SHA摘要，分段

```
let str3 = "harmony-utils，一款高效的HarmonyOS工具包，封装了常用工具类，提供一系列简单易用的方法。帮助开发者快速构建鸿蒙应用。gitee地址：https://gitee.com/tongyuyan/harmony-utils。github主页地址：https://github.com/787107497。";

let digest1 = await SHA.digestSegment(str3);
LogUtil.error(`分段摘要，异步: ${digest1}`);

let digest2 = SHA.digestSegmentSync(str3);
LogUtil.error(`分段摘要，同步: ${digest2}`);

let digest3 = SHA.digestSegmentSync(str3, 'SHA256', 'base64', 256);
LogUtil.error(`分段摘要:\t ${digest3}`);
```

##### hmac  消息认证码计算

```
let symKey = CryptoUtil.generateSymKeySync("HMAC|SHA256");

let str1 = "鸿蒙技术交流QQ群：1029219059";

let digest1 = await SHA.hmac(str1);
LogUtil.error(`消息认证码计算，异步: ${digest1}`);

let digest2 = SHA.hmacSync(str1);
LogUtil.error(`消息认证码计算，同步: ${digest2}`);

let digest3 = SHA.hmacSync(str1, 'SHA256', symKey);
LogUtil.error(`消息认证码计算:\t ${digest3}`);
```

##### hmacSegment  消息认证码计算，分段

```
let symKey = CryptoUtil.generateSymKeySync("HMAC|SHA256");

let str3 = "harmony-utils，一款高效的HarmonyOS工具包，封装了常用工具类，提供一系列简单易用的方法。帮助开发者快速构建鸿蒙应用。gitee地址：https://gitee.com/tongyuyan/harmony-utils。github主页地址：https://github.com/787107497。";

let digest1 = await SHA.hmacSegment(str3);
LogUtil.error(`分段消息认证码计算，异步: ${digest1}`);

let digest2 = SHA.hmacSegmentSync(str3);
LogUtil.error(`分段消息认证码计算，同步: ${digest2}`);

let digest3 = SHA.hmacSegmentSync(str3, 'SHA256', symKey, 'hex', 256);
LogUtil.error(`分段消息认证码计算:\t ${digest3}`);
```

## 创作不易，请给童长老点赞👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   

