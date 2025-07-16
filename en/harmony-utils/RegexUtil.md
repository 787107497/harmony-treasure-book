# RegexUtils, RegexUtil, Regular Tools Class

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

##### isMatch Whether the given content matches the regular (used with regular constants in RegexUtil)

```
let url = "https://ohpm.openharmony.cn/#/cn/publisher/663b99a5788eb334c83d9cd5";
let blUrl = RegexUtil.isMatch(url, RegexUtil.REG_URL);

let num = "123479";
let blNum = RegexUtil.isMatch(num, RegexUtil.REG_NUMBERS);

let cardNo = "340322199601100668";
let blCardNo = RegexUtil.isMatch(cardNo, RegexUtil.REG_CITIZEN_ID);

let date = "2024-10-15 21:18";
let blDate = RegexUtil.isMatch(date, RegexUtil.REG_TIME);
```

##### isPhone determines whether the incoming phone number format is correct

```
let phone: string = "18969062528";
let bl = RegexUtil.isPhone(phone);
```

##### isDigits Check whether the string contains only numeric characters

```
let str: string = "18969062528001";
let bl = RegexUtil.isDigits(str);
```

##### isEmail determines whether the format of the incoming mailbox is correct

```
let email: string = "787107497@qq.com";
let bl2 = RegexUtil.isEmail(email);
```

##### isEmoji determines whether the string contains emoticons

```
let str = "hdc shell aa start -a EntryAbility -b com.harmony.utils in 253 ms";
let isEmoji = RegexUtil.isEmoji(str);
```

##### isValidCard Verify the validity of the ID number

```
let bl1 = RegexUtil.isValidCard('11010519491231002X'); //true
let bl2 = RegexUtil.isValidCard('110101199001011235'); //false (校验码错误)
let bl3 = RegexUtil.isValidCard("110101900101123"); //true (15位格式正确)
let bl4 = RegexUtil.isValidCard("123456789012345"); //false (格式错误)
```


## Full Code Example

------

```
import { router } from '@kit.ArkUI';
import { MockSetup } from '@ohos/hamock';
import { LogUtil, RegexUtil, ToastUtil } from '@pura/harmony-utils';
import { TitleBarView } from '../../component/TitleBarView';
import { DescribeBean } from '../../model/DescribeBean';

/**
 * 正则工具类
 */
@Entry
@Component
struct Index {
  private scroller: Scroller = new Scroller();
  @State describe: DescribeBean = router.getParams() as DescribeBean;

  @MockSetup
  mock() {
    this.describe = new DescribeBean("RegexUtil", "正则工具类");
  }

  build() {
    Column() {
      TitleBarView({ describe: this.describe })
      Divider()
      Scroll(this.scroller) {
        Column() {
          Button("isMatch()")
            .btnStyle()
            .onClick(() => {
              let url = "https://ohpm.openharmony.cn/#/cn/publisher/663b99a5788eb334c83d9cd5";
              let blUrl = RegexUtil.isMatch(url, RegexUtil.REG_URL);
              let num = "123479";
              let blNum = RegexUtil.isMatch(num, RegexUtil.REG_NUMBERS);
              let cardNo = "340322199601100668";
              let blCardNo = RegexUtil.isMatch(cardNo, RegexUtil.REG_CITIZEN_ID);
              let date = "2024-10-15 21:18";
              let blDate = RegexUtil.isMatch(date, RegexUtil.REG_TIME);
              LogUtil.error(`是否是URL: ${blUrl}`);
              LogUtil.error(`是否是数字: ${blNum}`);
              LogUtil.error(`是否是身份证号: ${blCardNo}`);
              LogUtil.error(`是否是时间: ${blDate}`);
              ToastUtil.showToast("请查看Log日志");
            })
          Button("isDigits()")
            .btnStyle()
            .onClick(() => {
              let str: string = "18969062528001";
              let bl = RegexUtil.isDigits(str);
              LogUtil.error(`isDigits: ${bl}`);
              ToastUtil.showToast("请查看Log日志");
            })
          Button("isPhone()")
            .btnStyle()
            .onClick(() => {
              let phone: string = "18969062528";
              let bl = RegexUtil.isPhone(phone);
              LogUtil.error(`isPhone: ${bl}`);
              ToastUtil.showToast("请查看Log日志");
            })
          Button("isEmoji()\nisEmail()")
            .labelStyle({ maxLines: 2 })
            .type(ButtonType.Normal)
            .borderRadius(10)
            .padding({ top: 10, bottom: 10 })
            .btnStyle()
            .onClick(() => {
              let email: string = "787107497@qq.com";
              let bl2 = RegexUtil.isEmail(email);
              LogUtil.error(`是否是邮件: ${bl2}`);
              let str = "hdc shell aa start -a EntryAbility -b com.harmony.utils in 253 ms";
              let isEmoji = RegexUtil.isEmoji(str);
              LogUtil.error(`判断字符串是否包含表情: ${isEmoji}`);
              ToastUtil.showToast("请查看Log日志");
            })
          Button("isValidCard()")
            .btnStyle()
            .onClick(() => {
              let bl1 = RegexUtil.isValidCard('11010519491231002X'); //true
              let bl2 = RegexUtil.isValidCard('110101199001011235'); //false (校验码错误)
              let bl3 = RegexUtil.isValidCard("110101900101123"); //true (15位格式正确)
              let bl4 = RegexUtil.isValidCard("123456789012345"); //false (格式错误)
              LogUtil.error(`bl1: ${bl1}\n\nbl2: ${bl2}\n\nbl3: ${bl3}\n\nbl4: ${bl4}`);
              ToastUtil.showToast(`bl1: ${bl1}\n\nbl2: ${bl2}\n\nbl3: ${bl3}\n\nbl4: ${bl4}`);
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
   

