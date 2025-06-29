# harmony-utils之ECDSA，ECDSA工具类

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


## ECDSA 算法简介

------
ECDSA（椭圆曲线数字签名算法）是基于椭圆曲线密码学的数字签名方案，核心通过椭圆曲线离散对数问题的难解性保障安全。其原理为：选定椭圆曲线参数后，生成私钥 (d) 与公钥 (Q = d times G)（(G) 为曲线基点）；签名时结合消息哈希值与随机数计算签名对 ((r, s))，验证时通过公钥与签名还原点坐标并比对。

## ECDSA 应用场景

------
ECDSA（椭圆曲线数字签名算法）基于椭圆曲线离散对数难题，凭借短密钥、高安全性和低计算开销，在多场景中发挥关键作用。区块链领域，它用于比特币、以太坊的交易签名与地址生成，保障交易不可篡改；网络安全方面，支持TLS/SSL证书签名，降低握手计算开销，也适用于VPN和物联网设备的身份认证。在合规与资源受限场景，它符合国际标准，用于电子证照等，且适配智能卡、手机银行等低算力设备。与RSA相比，256位ECDSA安全性等效于3072位RSA，签名数据量小、效率高，更适合区块链、边缘计算等场景。虽面临量子计算威胁，但其仍是后量子密码过渡前的主流签名方案，在数字签名领域占据重要地位。


## API方法与使用

------

##### sign  对数据进行签名

```
let keyPair = await CryptoUtil.generateKeyPair('ECC256'); //生成密钥

let str1 = "鸿蒙技术交流QQ群：1029219059";
let dataBlob = CryptoHelper.strToDataBlob(str1, 'utf-8');

let signDataBlob = await ECDSA.sign(dataBlob, keyPair.priKey);
let signStr = CryptoHelper.dataBlobToStr(signDataBlob, 'hex');
LogUtil.error(`签名，异步: ${signStr}`);
```

##### verify  对数据进行验签

```
let keyPair = await CryptoUtil.generateKeyPair('ECC256'); //生成密钥

let str1 = "鸿蒙技术交流QQ群：1029219059";
let dataBlob = CryptoHelper.strToDataBlob(str1, 'utf-8');

let signDataBlob = await ECDSA.sign(dataBlob, keyPair.priKey);;
let verify = await ECDSA.verify(dataBlob, signDataBlob, keyPair.pubKey);
LogUtil.error(`验签，异步: ${verify}`);
```

##### signSegment  对数据进行分段签名

```
let keyPair = await CryptoUtil.generateKeyPair('ECC256'); //生成密钥

let str3 = "harmony-utils，一款高效的HarmonyOS工具包，封装了常用工具类，提供一系列简单易用的方法。帮助开发者快速构建鸿蒙应用。gitee地址：https://gitee.com/tongyuyan/harmony-utils。github主页地址：https://github.com/787107497。";
let data = CryptoHelper.strToUint8Array(str3, 'utf-8');

let signDataBlob = await ECDSA.signSegment(data, keyPair.priKey);
let signStr = CryptoHelper.dataBlobToStr(signDataBlob, 'base64');
LogUtil.error(`分段签名，异步: ${signStr}`);

```

##### verifySegment  对数据进行分段验签

```
let keyPair = await CryptoUtil.generateKeyPair('ECC256'); //生成密钥

let str3 = "harmony-utils，一款高效的HarmonyOS工具包，封装了常用工具类，提供一系列简单易用的方法。帮助开发者快速构建鸿蒙应用。gitee地址：https://gitee.com/tongyuyan/harmony-utils。github主页地址：https://github.com/787107497。";
let data = CryptoHelper.strToUint8Array(str3, 'utf-8');

let signDataBlob = await ECDSA.signSegment(data, keyPair.priKey);
let verify = await ECDSA.verifySegment(data, signDataBlob, keyPair.pubKey);
LogUtil.error(`分段验签，异步: ${verify}`);
```

## 创作不易，请给童长老点赞👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   

