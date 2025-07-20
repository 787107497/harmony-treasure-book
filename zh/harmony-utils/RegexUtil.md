# harmony-utils之RegexUtil，正则工具类

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

##### isMatch  给定内容是否匹配正则（配合RegexUtil里的正则常量一起使用）

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

##### isPhone  判断传入的电话号码格式是否正确

```
let phone: string = "18969062528";
let bl = RegexUtil.isPhone(phone);
```

##### isDigits  检查字符串是否只包含数字字符

```
let str: string = "18969062528001";
let bl = RegexUtil.isDigits(str);
```

##### isEmail  判断传入的邮箱格式是否正确

```
let email: string = "787107497@qq.com";
let bl2 = RegexUtil.isEmail(email);
```

##### isEmoji  判断字符串是否包含表情

```
let str = "hdc shell aa start -a EntryAbility -b com.harmony.utils in 253 ms";
let isEmoji = RegexUtil.isEmoji(str);
```

##### isValidCard  验证身份证号码的有效性

```
let bl1 = RegexUtil.isValidCard('11010519491231002X'); //true
let bl2 = RegexUtil.isValidCard('110101199001011235'); //false (校验码错误)
let bl3 = RegexUtil.isValidCard("110101900101123"); //true (15位格式正确)
let bl4 = RegexUtil.isValidCard("123456789012345"); //false (格式错误)
```


## 示例代码

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


## 创作不易，请给童长老点赞👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   

