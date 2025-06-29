# RegexUtils, RegexUtil, Regular Tools Class

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

## Creation is not easy, please give Elder Tong a thumbs up 👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   

