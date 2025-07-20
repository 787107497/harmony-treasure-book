# harmony-utils之RandomUtil，随机工具类

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

## API方法与使用

------

##### getRandomBoolean  生成随机Boolean值

```
let bl = RandomUtil.getRandomBoolean();
```

##### getRandomInt  生成随机整数（可指定范围）

```
let n1 = RandomUtil.getRandomInt();
```

##### getRandomNumber  生成指定范围内的随机数

```
let n3 = RandomUtil.getRandomNumber(10000, 1000000);
```

##### getRandomLimit  生成指定范围内的随机数 [0,limit)

```
let n2 = RandomUtil.getRandomLimit(1000);
```

##### getRandomChineseChar  生成一个随机汉字

```
let str1 = RandomUtil.getRandomChineseChar();
```

##### getRandomChinese  生成随机汉字

```
let str2 = RandomUtil.getRandomChinese(12);
```

##### getRandomStr  根据指定字符串，随机生成 指定长度的字符串

```
let r1 = RandomUtil.getRandomStr(15, "ACCDEFGHIJKMNL");
```

##### getRandomDataBlob  生成随机指定长度的DataBlob

```
let dataBlob = RandomUtil.getRandomDataBlob(8);
```

##### getRandomUint8Array  生成随机指定长度的Uint8Array

```
let unit8Array = RandomUtil.getRandomUint8Array(8);
```

##### getRandomColor  生成随机颜色，十六进制

```
let c3 = RandomUtil.getRandomColor();
```

##### generateUUID36  生成36位UUID，带-

```
let uuid36 = RandomUtil.generateUUID36();
```

##### generateUUID32  生成32位UUID，带-

```
let uuid32 = RandomUtil.generateUUID32();
```

##### generateRandomUUID  使用加密安全随机数生成器生成随机的RFC 4122版本4的string类型UUID

```
let uuid1 = RandomUtil.generateRandomUUID();
```

##### generateRandomBinaryUUID  使用加密安全随机数生成器生成随机的RFC 4122版本4的Uint8Array类型UUID

```
let uuid2 = RandomUtil.generateRandomBinaryUUID();
```


## 示例代码

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


## 创作不易，请给童长老点赞👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   



