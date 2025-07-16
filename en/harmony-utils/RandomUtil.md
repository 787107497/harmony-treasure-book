# harmony-utils RandomUtil, random tool class

## Introduction and description of harmony-utils

------
[harmony-utils](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils) A HarmonyOS tool library with rich features and extremely easy to use, with the help of many practical tools, is committed to helping developers quickly build Hongmeng applications. Its encapsulated tools cover APP, device, screen, authorization, notification, inter-thread communication, pop-up frames, toast, biometric authentication, user preferences, taking photos, albums, scanning codes, files, logs, exception capture, characters, strings, numbers, collections, dates, random, base64, encryption, decryption, JSON and other functions, which can meet various development needs.     
[picker_utils](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fpicker_utils) It is a sub-store split by harmony-utils, including PickerUtil, PhotoHelper, and ScanUtil.

Download and install
`ohpm i @pura/harmony-utils`  
`ohpm i @pura/picker_utils`

 ```
  //全局初始化方法，在UIAbility的onCreate方法中初始化 AppUtil.init()
  onCreate(want: Want, launchParam: AbilityConstant.LaunchParam): void {
    AppUtil.init(this.context);
  }
 ```

## API methods and usage

------

##### getRandomBoolean generates random Boolean values

```
let bl = RandomUtil.getRandomBoolean();
```

##### getRandomInt generates random integers (the range can be specified)

```
let n1 = RandomUtil.getRandomInt();
```

##### getRandomNumber Generates a random number within a specified range

```
let n3 = RandomUtil.getRandomNumber(10000, 1000000);
```

##### getRandomLimit generates a random number within the specified range [0,limit)

```
let n2 = RandomUtil.getRandomLimit(1000);
```

##### getRandomChineseChar generates a random Chinese character

```
let str1 = RandomUtil.getRandomChineseChar();
```

##### getRandomChinese generates random Chinese characters

```
let str2 = RandomUtil.getRandomChinese(12);
```

##### getRandomStr randomly generates strings of specified length according to the specified string.

```
let r1 = RandomUtil.getRandomStr(15, "ACCDEFGHIJKMNL");
```

##### getRandomDataBlob Generates DataBlob of randomly specified length

```
let dataBlob = RandomUtil.getRandomDataBlob(8);
```

##### getRandomUint8Array generates a Uint8Array of randomly specified length

```
let unit8Array = RandomUtil.getRandomUint8Array(8);
```

##### getRandomColor generates random colors in hexadecimal

```
let c3 = RandomUtil.getRandomColor();
```

##### generateUUID36 generates 36-bit UUID with -

```
let uuid36 = RandomUtil.generateUUID36();
```

##### generateUUID32 generates 32-bit UUID with -

```
let uuid32 = RandomUtil.generateUUID32();
```

##### generateRandomUUID generates a random RFC 4122 version 4 string type UUID using the Encrypted Secure Random Number Generator

```
let uuid1 = RandomUtil.generateRandomUUID();
```

##### generateRandomBinaryUUID generates random RFC 4122 version 4 Uint8Array type UUID using Encrypted Secure Random Number Generator

```
let uuid2 = RandomUtil.generateRandomBinaryUUID();
```


## Full Code Example

------

```
import { router } from '@kit.ArkUI';
import { MockSetup } from '@ohos/hamock';
import { LogUtil, RandomUtil, StrUtil } from '@pura/harmony-utils';
import { TitleBarView } from '../../component/TitleBarView';
import { DescribeBean } from '../../model/DescribeBean';
import { Utils } from '../../utils/Utils';

/**
 * 随机工具类
 */
@Entry
@Component
struct Index {
  private scroller: Scroller = new Scroller();
  @State describe: DescribeBean = router.getParams() as DescribeBean;

  @MockSetup
  mock() {
    this.describe = new DescribeBean("RandomUtil", "随机工具类");
  }

  build() {
    Column() {
      TitleBarView({ describe: this.describe })
      Divider()
      Scroll(this.scroller) {
        Column() {
          Button("getRandomInt()\ngetRandomLimit()\ngetRandomNumber()")
            .labelStyle({ maxLines: 3 })
            .type(ButtonType.Normal)
            .borderRadius(10)
            .padding({ top: 10, bottom: 10 })
            .btnStyle()
            .onClick(() => {
              let n1 = RandomUtil.getRandomInt();
              let n2 = RandomUtil.getRandomLimit(1000);
              let n3 = RandomUtil.getRandomNumber(10000, 1000000);
              let txtStr = `随机数1：${n1}\n随机数2：${n2}\n随机数3：${n3}`;
              LogUtil.error(txtStr);
              Utils.showSheetText(txtStr);
            })
          Button("getRandomChineseChar()\ngetRandomChinese()")
            .labelStyle({ maxLines: 3 })
            .type(ButtonType.Normal)
            .borderRadius(10)
            .padding({ top: 10, bottom: 10 })
            .btnStyle()
            .onClick(() => {
              let str1 = RandomUtil.getRandomChineseChar();
              let str2 = RandomUtil.getRandomChinese(12);
              let txtStr = `随机汉字：${str1}\n随机汉字：${str2}`;
              LogUtil.error(txtStr);
              Utils.showSheetText(txtStr);
            })
          Button("getRandomBoolean()\ngetRandomColor()")
            .labelStyle({ maxLines: 3 })
            .type(ButtonType.Normal)
            .borderRadius(10)
            .padding({ top: 10, bottom: 10 })
            .btnStyle()
            .onClick(() => {
              let b1 = RandomUtil.getRandomBoolean();
              let b2 = RandomUtil.getRandomBoolean();
              let c3 = RandomUtil.getRandomColor();
              let txtStr = `随机Boolean值1：${b1}\n随机Boolean值2：${b2}\n随机颜色：${c3}`;
              LogUtil.error(txtStr);
              Utils.showSheetText(txtStr);
            })
          Button("getRandomStr()")
            .btnStyle()
            .onClick(() => {
              let r1 = RandomUtil.getRandomStr(15, "ACCDEFGHIJKMNL");
              let r2 = RandomUtil.getRandomStr(12, "accdefghijkmnl");
              let r3 = RandomUtil.getRandomStr(16, "1234567890");
              let r4 = RandomUtil.getRandomStr(10, "哈呵嘿哼噢哦呸嗷");
              let txtStr = `随机1：${r1}\n随机2：${r2}\n随机3：${r3}\n随机4：${r4}`;
              LogUtil.error(txtStr);
              Utils.showSheetText(txtStr);
            })
          Button("getRandomDataBlob()\ngetRandomUint8Array()")
            .labelStyle({ maxLines: 3 })
            .type(ButtonType.Normal)
            .borderRadius(10)
            .padding({ top: 10, bottom: 10 })
            .btnStyle()
            .onClick(() => {
              let dataBlob = RandomUtil.getRandomDataBlob(8);
              let unit8Array = RandomUtil.getRandomUint8Array(8);
              let txtStr = `dataBlob：\n${dataBlob.data}\n\n3unit8Array：\n${unit8Array}`;
              LogUtil.error(txtStr);
              Utils.showSheetText(txtStr);
            })

          Button("generateUUID36()\ngenerateUUID32()")
            .labelStyle({ maxLines: 3 })
            .type(ButtonType.Normal)
            .borderRadius(10)
            .padding({ top: 10, bottom: 10 })
            .btnStyle()
            .onClick(() => {
              let uuid36 = RandomUtil.generateUUID36();
              let uuid32 = RandomUtil.generateUUID32();
              let txtStr = `36位UUID：\n${uuid36}\n\n32位UUID：\n${uuid32}`;
              LogUtil.error(txtStr);
              Utils.showSheetText(txtStr);
            })
          Button("generateRandomUUID()\ngenerateRandomBinaryUUID")
            .labelStyle({ maxLines: 3 })
            .type(ButtonType.Normal)
            .borderRadius(10)
            .padding({ top: 10, bottom: 10 })
            .btnStyle()
            .onClick(() => {
              let uuid1 = RandomUtil.generateRandomUUID();
              let uuid2 = RandomUtil.generateRandomBinaryUUID();
              let txtStr = `使用加密安全随机数生成器生成随机的string类型UUID：\n${uuid1}\n\n使用加密安全随机数生成器生成随机的Uint8Array类型UUID：\n${uuid2}`;
              LogUtil.error(txtStr);
              Utils.showSheetText(txtStr);
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
   



