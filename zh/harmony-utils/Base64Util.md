# harmony-utils之Base64Util，Base64工具类

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

## Base64 简介

------
Base64是一种基于64个可打印字符（A-Z、a-z、0-9、+、/，部分场景以-、_
替代）的二进制编码方案，核心功能是将非文本数据转化为文本形式传输，有效规避字符集差异导致的传输错误。   
作为非加密技术，Base64凭借文本化传输的天然优势，成为数据处理与跨系统交互的基础工具，在“二进制转文本”场景中具有不可替代性。其核心价值在于构建数据转换的桥梁——尽管编码后数据体积会增加约33%，却能完美兼容跨系统、跨协议的传输需求。从邮件附件编码到API接口设计，从前端图片内嵌优化到加密数据的文本化封装，Base64始终是解决“非文本数据文本化”问题的标准方案，尤其在兼顾可读性与传输稳定性的场景中不可或缺。

## API方法与使用

------

##### encode  编码，通过输入参数编码后输出Uint8Array对象

```
let unit8Array = StrUtil.strToUint8Array("我是甜啦啦");
let unit8Array1 = Base64Util.encodeSync(unit8Array);
```

##### encodeToStr  编码，通过输入参数编码后输出对应文本

```
let unit8Array = StrUtil.strToUint8Array("我是甜啦啦");
let str = Base64Util.encodeToStrSync(unit8Array);
```

##### decode  解码，通过输入参数解码后输出对应Uint8Array对象

```
let unit8Array = StrUtil.strToUint8Array("我是甜啦啦");
let str = Base64Util.encodeToStrSync(unit8Array);
let unit8Array2 = Base64Util.decodeSync(str);
let str2 = StrUtil.unit8ArrayToStr(unit8Array2);
```

##### 字符串 与 Base64字符串 的 转换

```
let str1 = "我是笑面虎";
let base64Str = StrUtil.strToBase64(str1);
let str = StrUtil.base64ToStr(base64Str);
```

## 创作不易，请给童长老点赞👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   
