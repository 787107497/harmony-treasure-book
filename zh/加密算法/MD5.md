# harmony-utils之MD5，MD5工具类

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


## MD5 算法简介

------
MD5（Message-Digest Algorithm 5）是由Ronald Rivest于1991年设计的密码散列函数，可将任意长度数据生成128位（16字节）的固定长度哈希值。其核心通过‌填充-分块-循环压缩‌流程实现：先对输入补位至512位倍数，再分块进行4轮非线性运算（每轮16次操作），最终输出唯一性摘要。
该算法曾广泛用于文件完整性校验（如软件包校验）、密码存储及数字证书签名。但因存在碰撞漏洞（可人为构造相同哈希的不同数据），自2004年被证实不抗碰撞攻击后，逐步被SHA-256等更安全算法替代。目前仍见于非敏感场景如缓存标识或数据去重。因MD5存在碰撞攻击风险（王小云团队2004年破解），金融、政务等关键领域已禁用，推荐改用SM3/SHA-256。


## API方法与使用

------

##### digest  MD5摘要

```
let str1 = "鸿蒙技术交流QQ群：1029219059";

let digest1 = await MD5.digest(str1);
LogUtil.error(`摘要，异步: ${digest1}`);

let digest2 = MD5.digestSync(str1);
LogUtil.error(`摘要，同步1: ${digest2}`);

let digest3 = MD5.digestSync(str1, 'base64');
LogUtil.error(`摘要，同步2: ${digest3}`);
```

##### digestSegment  MD5摘要，分段

```
let str3 = "harmony-utils，一款高效的HarmonyOS工具包，封装了常用工具类，提供一系列简单易用的方法。帮助开发者快速构建鸿蒙应用。gitee地址：https://gitee.com/tongyuyan/harmony-utils。github主页地址：https://github.com/787107497。";

let digest1 = await MD5.digestSegment(str3);
LogUtil.error(`分段摘要，异步: ${digest1}`);

let digest2 = MD5.digestSegmentSync(str3);
LogUtil.error(`分段摘要，同步1: ${digest2}`);

let digest3 = MD5.digestSegmentSync(str3, 'base64', 256);
LogUtil.error(`分段摘要，同步2: ${digest3}`);
```

##### hmac  消息认证码计算

```
let symKey = CryptoUtil.generateSymKeySync("AES256");
let str1 = "鸿蒙技术交流QQ群：1029219059";

let digest1 = await MD5.hmac(str1, symKey);
LogUtil.error(`消息认证码计算，异步: ${digest1}`);

let digest2 = MD5.hmacSync(str1, symKey);
LogUtil.error(`消息认证码计算，同步1: ${digest2}`);

let digest3 = MD5.hmacSync(str1, symKey, 'base64');
LogUtil.error(`消息认证码计算，同步2: ${digest3}`);
```

##### hmacSegment   消息认证码计算，分段

```
let symKey = CryptoUtil.generateSymKeySync("AES256");
let str3 = "harmony-utils，一款高效的HarmonyOS工具包，封装了常用工具类，提供一系列简单易用的方法。帮助开发者快速构建鸿蒙应用。gitee地址：https://gitee.com/tongyuyan/harmony-utils。github主页地址：https://github.com/787107497。";

let digest1 = await MD5.hmacSegment(str3, symKey);
LogUtil.error(`分段消息认证码计算，异步: ${digest1}`);

let digest2 = MD5.hmacSegmentSync(str3, symKey);
LogUtil.error(`分段消息认证码计算，同步1: ${digest2}`);

let digest3 = MD5.hmacSegmentSync(str3, symKey, 'hex', 256);
LogUtil.error(`分段消息认证码计算，同步2: ${digest3}`);
```

## 创作不易，请给童长老点赞👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   

