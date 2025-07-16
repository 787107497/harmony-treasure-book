# Base64Utils, Base64 tool class

## Introduction and description of harmony-utils

------
[harmony-utils](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)A HarmonyOS tool library with rich features and extremely easy to use, with the help of many practical tools, is committed to helping developers quickly build Hongmeng applications. Its encapsulated tools cover APP, device, screen, authorization, notification, inter-thread communication, pop-up frames, toast, biometric authentication, user preferences, taking photos, albums, scanning codes, files, logs, exception capture, characters, strings, numbers, collections, dates, random, base64, encryption, decryption, JSON and other functions, which can meet various development needs.
[picker_utils](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fpicker_utils)It is a sub-store split by harmony-utils, including PickerUtil, PhotoHelper, and ScanUtil.

Download and install
`ohpm i @pura/harmony-utils`  
`ohpm i @pura/picker_utils`

 ```
  //全局初始化方法，在UIAbility的onCreate方法中初始化 AppUtil.init()
  onCreate(want: Want, launchParam: AbilityConstant.LaunchParam): void {
    AppUtil.init(this.context);
  }
 ```

## Base64 Introduction

------
Base64 is a type of 64 printable characters (A-Z, a-z, 0-9, +, /, some scenes are -, _
The core function of the binary encoding scheme is to convert non-text data into text transmission, effectively avoiding transmission errors caused by character set differences.
As a non-encryption technology, Base64 has become a basic tool for data processing and cross-system interaction with its natural advantages of textual transmission, and is irreplaceable in the "binary to text" scenario. Its core value lies in building a bridge for data conversion - although the data volume will increase by about 33% after encoding, it can be perfectly compatible with the transmission requirements of cross-system and cross-protocols. From email attachment encoding to API interface design, from front-end picture embedding optimization to textual encapsulation of encrypted data, Base64 has always been a standard solution to the problem of "non-text data textualization", especially in scenarios that take into account readability and transmission stability.

## API methods and usage

------

##### encode encoding, output Uint8Array object after inputting parameters

```
let unit8Array = StrUtil.strToUint8Array("我是甜啦啦");
let unit8Array1 = Base64Util.encodeSync(unit8Array);
```

##### encodeToStr encoding, output the corresponding text after inputting parameters

```
let unit8Array = StrUtil.strToUint8Array("我是甜啦啦");
let str = Base64Util.encodeToStrSync(unit8Array);
```

##### decode decode, decode the corresponding Uint8Array object after decoding by input parameters

```
let unit8Array = StrUtil.strToUint8Array("我是甜啦啦");
let str = Base64Util.encodeToStrSync(unit8Array);
let unit8Array2 = Base64Util.decodeSync(str);
let str2 = StrUtil.unit8ArrayToStr(unit8Array2);
```

##### Conversion of string and Base64 string

```
let str1 = "我是笑面虎";
let base64Str = StrUtil.strToBase64(str1);
let str = StrUtil.base64ToStr(base64Str);
```

## Full Code Example

```
import { router } from '@kit.ArkUI';
import { MockSetup } from '@ohos/hamock';
import { Base64Util, LogUtil, StrUtil, ToastUtil } from '@pura/harmony-utils';
import { TitleBarView } from '../../component/TitleBarView';
import { DescribeBean } from '../../model/DescribeBean';
import { Utils } from '../../utils/Utils';

/**
 * Base64工具类
 */
@Entry
@Component
struct Index {
  private scroller: Scroller = new Scroller();
  @State describe: DescribeBean = router.getParams() as DescribeBean;

  @MockSetup
  mock() {
    this.describe = new DescribeBean("Base64Util", "Base64工具类");
  }

  build() {
    Column() {
      TitleBarView({ describe: this.describe })
      Divider()
      Scroll(this.scroller) {
        Column() {
          Button("encodeSync()\nencodeToStrSync()\ndecodeSync()")
            .labelStyle({ maxLines: 3 })
            .type(ButtonType.Normal)
            .borderRadius(10)
            .padding({ top: 10, bottom: 10 })
            .btnStyle()
            .onClick(() => {
              let unit8Array = StrUtil.strToUint8Array("我是甜啦啦");
              let unit8Array1 = Base64Util.encodeSync(unit8Array);
              LogUtil.error(`unit8Array1: ${unit8Array1}`);
              let str = Base64Util.encodeToStrSync(unit8Array);
              LogUtil.error(`str: ${str}`);
              let unit8Array2 = Base64Util.decodeSync(str);
              LogUtil.error(`unit8Array2: ${unit8Array2}`);
              Utils.showSheetText(`unit8Array1: ${unit8Array1}\n\nstr: ${str}\n\nunit8Array2: ${unit8Array2}`);
            })
          Button("encode()\nencodeToStr()\ndecode()")
            .labelStyle({ maxLines: 3 })
            .type(ButtonType.Normal)
            .borderRadius(10)
            .padding({ top: 10, bottom: 10 })
            .btnStyle()
            .onClick(async () => {
              let unit8Array = StrUtil.strToUint8Array("我是甜啦啦!");
              let unit8Array1 = await Base64Util.encode(unit8Array);
              LogUtil.error(`unit8Array1: ${unit8Array1}`);
              let str = await Base64Util.encodeToStr(unit8Array);
              LogUtil.error(`str: ${str}`);
              let unit8Array2 = await Base64Util.decode(unit8Array1);
              LogUtil.error(`unit8Array2: ${unit8Array2}`);
              let str2 = StrUtil.unit8ArrayToStr(unit8Array2);
              Utils.showSheetText(`unit8Array1: ${unit8Array1}\n\nstr: ${str}\n\nunit8Array2: ${unit8Array2}\n\nstr2: ${str2}`);
            })

          Blank().layoutWeight(1)
        }
        .margin({ top: 5, bottom: 5 })
      }
      .layoutWeight(1)
    }
    .width('100%')
    .height('100%')
    .justifyContent(FlexAlign.Start)
    .backgroundColor($r('app.color.main_background'))
  }
}


@Styles
function btnStyle() {
  .width('90%')
  .margin({ top: 10, bottom: 5 })
}

```

## Creation is not easy, please give Elder Tong a thumbs up 👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   
