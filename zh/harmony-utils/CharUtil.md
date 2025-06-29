# harmony-utils之CharUtil，字符工具类

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

##### isDigit  判断字符串char是否是数字

```
let b1 = CharUtil.isDigit('6');
let b2 = CharUtil.isDigit('A');
let b3 = CharUtil.isDigit('瑶');
let b4 = CharUtil.isDigit('6a');
```

##### isLetter  判断字符串char是否是字母

```
let bl1 = CharUtil.isLetter('A');
let bl2 = CharUtil.isLetter('6');
let bl3 = CharUtil.isLetter('瑶');
let bl4 = CharUtil.isLetter('a6');
```

##### isLowerCase  判断字符串char是否是小写字母

```
let b1 = CharUtil.isLowerCase('a');
let b2 = CharUtil.isLowerCase('ad');
let b3 = CharUtil.isLowerCase('瑶');
let b4 = CharUtil.isLowerCase('6abc');
let b5 = CharUtil.isLowerCase('Abc');
let b6 = CharUtil.isLowerCase('aBC');
```

##### isUpperCase  判断字符串char是否是大写字母

```
let bl1 = CharUtil.isUpperCase('A');
let bl2 = CharUtil.isUpperCase('AB');
let bl3 = CharUtil.isUpperCase('瑶');
let bl4 = CharUtil.isUpperCase('6cba');
let bl5 = CharUtil.isUpperCase('cBA');
let bl6 = CharUtil.isUpperCase('Cba');
```

##### isSpaceChar  判断字符串char是否是空格符

```
let b1 = CharUtil.isSpaceChar(' ');
let b2 = CharUtil.isSpaceChar('a d');
let b3 = CharUtil.isSpaceChar('a ');
let b4 = CharUtil.isSpaceChar(' ');
```

##### isWhitespace  判断字符串char是否是空白符

```
let bl1 = CharUtil.isWhitespace('  ');
let bl2 = CharUtil.isWhitespace('A  B');
let bl3 = CharUtil.isWhitespace('a  ');
let bl4 = CharUtil.isWhitespace(' ');
```

##### isRTL  判断字符串char是否是从右到左语言的字符

```
let b1 = CharUtil.isRTL('我尼玛');
let b2 = CharUtil.isRTL('ad');
let b3 = CharUtil.isRTL('瑶');
let b4 = CharUtil.isRTL('6abc');
let b5 = CharUtil.isRTL('Abc');
let b6 = CharUtil.isRTL('aBC');
```

##### isIdeograph  判断字符串char是否是表意文字

```
let bl1 = CharUtil.isIdeograph('我尼玛');
let bl2 = CharUtil.isIdeograph('AB');
let bl3 = CharUtil.isIdeograph('ABC瑶');
let bl4 = CharUtil.isIdeograph('我尼玛6cba');
let bl5 = CharUtil.isIdeograph('cBA');
let bl6 = CharUtil.isIdeograph('Cba');
```

##### isBlankChar  判断是否空白符 空白符包括空格、制表符、全角空格和不间断空格

```
let b1 = CharUtil.isBlankChar(6);
let b2 = CharUtil.isBlankChar(126);
let b3 = CharUtil.isBlankChar(666);
let b4 = CharUtil.isBlankChar(66666);
```

##### isAscii  判断字符是否位于ASCII范围内（0~127）

```
let bl1 = CharUtil.isAscii('A');
let bl2 = CharUtil.isAscii('B');
let bl3 = CharUtil.isAscii('瑶');
let bl4 = CharUtil.isAscii('6cba');
```

## 创作不易，请给童长老点赞👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545) 
   

