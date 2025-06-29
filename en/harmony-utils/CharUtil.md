**# harmony-utils: CharUtil, character tool class

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

##### isDigit determines whether the string char is a number

```
let b1 = CharUtil.isDigit('6');
let b2 = CharUtil.isDigit('A');
let b3 = CharUtil.isDigit('瑶');
let b4 = CharUtil.isDigit('6a');
```

##### isLetter determines whether the string char is a letter

```
let bl1 = CharUtil.isLetter('A');
let bl2 = CharUtil.isLetter('6');
let bl3 = CharUtil.isLetter('瑶');
let bl4 = CharUtil.isLetter('a6');
```

##### isLowerCase determines whether the string char is a lowercase letter

```
let b1 = CharUtil.isLowerCase('a');
let b2 = CharUtil.isLowerCase('ad');
let b3 = CharUtil.isLowerCase('瑶');
let b4 = CharUtil.isLowerCase('6abc');
let b5 = CharUtil.isLowerCase('Abc');
let b6 = CharUtil.isLowerCase('aBC');
```

##### isUpperCase determines whether the string char is capital letter

```
let bl1 = CharUtil.isUpperCase('A');
let bl2 = CharUtil.isUpperCase('AB');
let bl3 = CharUtil.isUpperCase('瑶');
let bl4 = CharUtil.isUpperCase('6cba');
let bl5 = CharUtil.isUpperCase('cBA');
let bl6 = CharUtil.isUpperCase('Cba');
```

##### isSpaceChar determines whether the string char is a space character

```
let b1 = CharUtil.isSpaceChar(' ');
let b2 = CharUtil.isSpaceChar('a d');
let b3 = CharUtil.isSpaceChar('a ');
let b4 = CharUtil.isSpaceChar(' ');
```

##### isWhitespace determines whether the string char is a whitespace character

```
let bl1 = CharUtil.isWhitespace('  ');
let bl2 = CharUtil.isWhitespace('A  B');
let bl3 = CharUtil.isWhitespace('a  ');
let bl4 = CharUtil.isWhitespace(' ');
```

##### isRTL determines whether the string char is a character from right to left language

```
let b1 = CharUtil.isRTL('我尼玛');
let b2 = CharUtil.isRTL('ad');
let b3 = CharUtil.isRTL('瑶');
let b4 = CharUtil.isRTL('6abc');
let b5 = CharUtil.isRTL('Abc');
let b6 = CharUtil.isRTL('aBC');
```

##### isIdeograph determines whether the string char is an ideographic text

```
let bl1 = CharUtil.isIdeograph('我尼玛');
let bl2 = CharUtil.isIdeograph('AB');
let bl3 = CharUtil.isIdeograph('ABC瑶');
let bl4 = CharUtil.isIdeograph('我尼玛6cba');
let bl5 = CharUtil.isIdeograph('cBA');
let bl6 = CharUtil.isIdeograph('Cba');
```

##### isBlankChar determines whether a blank symbol is white space. White space includes spaces, tab characters, full-width spaces and uninterrupted spaces.

```
let b1 = CharUtil.isBlankChar(6);
let b2 = CharUtil.isBlankChar(126);
let b3 = CharUtil.isBlankChar(666);
let b4 = CharUtil.isBlankChar(66666);
```

##### isAscii determines whether the character is within the ASCII range (0~127)

```
let bl1 = CharUtil.isAscii('A');
let bl2 = CharUtil.isAscii('B');
let bl3 = CharUtil.isAscii('瑶');
let bl4 = CharUtil.isAscii('6cba');
```

## Creation is not easy, please give Elder Tong a thumbs up 👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545) 
   

