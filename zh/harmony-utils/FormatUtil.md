# harmony-utils之FormatUtil，格式化工具类

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

##### isPhone  判断传入的电话号码格式是否正确

```
let phone: string = "19869062586";
let bl = FormatUtil.isPhone(phone);
```

##### getPhoneFormat  对电话号码进行格式化

```
let phone: string = "19869062586";
let format = FormatUtil.getPhoneFormat(phone);
```

##### getPhoneLocationName  获取电话号码归属地

```
let phone: string = "19869062586";
let locationName = FormatUtil.getPhoneLocationName(phone);
```

##### transliterator  将输入字符串从源格式转换为目标格式（中文汉字转为拼音）

```
let str = FormatUtil.transliterator("中国");
```

##### getFormatPercentage  格式化百分比，将数字转化从百分比字符串

```
let percentage = FormatUtil.getFormatPercentage(0.491);
LogUtil.error(`percentage: ${percentage}`);
```

##### getFormatPhone  格式化手机号码，隐藏中间四位

```
let phone: string = "18969062528";
let str = FormatUtil.getFormatPhone(phone);
```

##### getFormatCardNo  格式化身份证号码，隐藏中间部分数字

```
let str = FormatUtil.getFormatCardNo("110101199001011234");
LogUtil.error(`格式化后的身份证号: ${str}`);
```

##### getFormatFileSize  格式化文件大小

```
let str = FormatUtil.getFormatFileSize(1024102400);
LogUtil.error(`文件大小: ${str}`);
```

##### getTruncateText  缩短长文本，超出部分用省略号表示

```
let str = FormatUtil.getTruncateText("女人什么年龄是最好？任何年龄都可以。因为每个年龄段都有不一样的美。看XX的穿搭你就会发现成熟女性的魅力，反而会更加的吸引人。", 20);
LogUtil.error(`缩短长文本: ${str}`);
```

##### getIconFont  解析iconFont字符

```
let str = FormatUtil.getIconFont("e631");
LogUtil.error(`getIconFont: ${str}`);
```

##### getQueryValue  获取url里的参数，Key对应的Value

```
let url = "https://blog.csdn.net/article?spm=blog1024&name=李斯";
let value1 = FormatUtil.getQueryValue(url, 'spm');
let value2 = FormatUtil.getQueryValue(url, 'name');
let value3 = FormatUtil.getQueryValue(url, 'mona');
```

##### getParamsUrl  将参数拼接在url上，返回新的url

```
let map = new Map<string, Any>();
map.set("id", 100011);
map.set("name", '王五');
map.set("sex", undefined);
let url1 = FormatUtil.getParamsUrl("https://blog.csdn.net?id=100012", map);

let obj: Record<string, Object> = {};
obj['key'] = 'show';
obj['user'] = '王五';
obj['pd'] = 0;
obj['type'] = 'csaitab';
let url2 = FormatUtil.getParamsUrl("https://blog.csdn.net?id=100012", obj);
```

## 创作不易，请给童长老点赞👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   

