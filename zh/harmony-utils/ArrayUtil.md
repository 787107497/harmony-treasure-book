# harmony-utils之ArrayUtil，集合工具类

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

##### isNotEmpty  判断集合是否为非空集合

```
let array0: string[] = []
let array1: string[] = [" 张三 ", "马哒哒 ", "李四", " 阿尼玛", "", "王五", "李四", "王五五", ""]
let b1 = ArrayUtil.isNotEmpty(array0);
let b3 = ArrayUtil.isNotEmpty(array1);
```

##### isEmpty  判断集合是否为空集合

```
let array0: string[] = []
let array1: string[] = [" 张三 ", "马哒哒 ", "李四", " 阿尼玛", "", "王五", "李四", "王五五", ""]
let b2 = ArrayUtil.isEmpty(array0);
let b4 = ArrayUtil.isEmpty(array1);
```

##### removeEmpty  去除字符串数组中的空值

```
let array: string[] = [" 张三 ", "null", "希大大 ", "李四", "undefined", " 阿超", '', "王五 ", ""];
let arr1 = ArrayUtil.removeEmpty(array); //去空
```

##### trim  去除字符串数组的每个值的前后空格

```
let array: string[] = [" 张三 ", "null", "希大大 ", "李四", "undefined", " 阿超", '', "王五 ", ""];
let arr2 = ArrayUtil.trim(array); //去空格
```

##### distinct  将数组去重，去重后生成新的数组，原数组不变

```
let array2: string[] = ["张三 ", "马哒哒 ", "李四", " 阿尼玛", "李四", "王五", "李四", "王五"];
let array = ArrayUtil.distinct(array2); //去重
```

##### reverse  将数组反转，会修改原始数组

```
let array4: number[] = [1, 100, 10, 0, 22, 68, 11];
let array = ArrayUtil.reverse(array4);
```

##### filter  数组过滤，通过filter函数实现来过滤返回需要的元素

```
let array4: number[] = [1, 100, 10, 0, 22, 68, 11];
let array1 = ArrayUtil.filter(array4, (item) => item > 10);
```

##### append  拼接数据，使用扩展运算符，不影响原数组

```
let array2: string[] = ["张三 ", "马哒哒 ", "李四", " 阿尼玛", "李四", "王五", "李四", "王五"];
let array3: string[] = ["黑龙江省", "哈尔滨市", "道里区", "砂山", "砀山", "高薪区"];
let array = ArrayUtil.append(array2, array3);
```

##### min  获取数组最小值（数值、字符串、日期）

```
let array4: number[] = [1, 100, 10, 0, 22, 68, 11];
let min = ArrayUtil.min(array4);
```

##### max  获取数组最大值（数值、字符串、日期）

```
let array4: number[] = [1, 100, 10, 0, 22, 68, 11];
let max = ArrayUtil.max(array4);
```

##### flatten  平铺二维数组

```
let array1: string[] = [" 张三 ", "马哒哒 ", "李四", " 阿尼玛", "", "王五", "李四", "王五五", ""]
let array2: string[] = ["张三 ", "马哒哒 ", "李四", " 阿尼玛", "李四", "王五", "李四", "王五"]
let array3: string[] = ["黑龙江省", "哈尔滨市", "道里区", "砂山", "砀山", "高薪区"]
let array5: string[][] = [array1, array2, array3];
let array = ArrayUtil.flatten(array5);
```

##### union  平铺二维数组，并去重

```
let array1: string[] = [" 张三 ", "马哒哒 ", "李四", " 阿尼玛", "", "王五", "李四", "王五五", ""]
let array2: string[] = ["张三 ", "马哒哒 ", "李四", " 阿尼玛", "李四", "王五", "李四", "王五"];
let array3: string[] = ["黑龙江省", "哈尔滨市", "道里区", "砂山", "砀山", "高薪区"]
let array5: string[][] = [array1, array2, array3];
let array = ArrayUtil.union(array5);
```

##### chunk  数组分块

```
let array2: string[] = ["张三 ", "马哒哒 ", "李四", " 阿尼玛", "李四", "王五", "李四", "王五"];
let array = ArrayUtil.chunk(array2, 2);
```

##### contain  判断集合是否包含某个值

```
let array1: string[] = [" 张三 ", "马哒哒 ", "李四", " 阿尼玛", "", "王五", "李四", "王五五"];
let array = ArrayUtil.contain(array1, "王五");
```

##### remove  移除集合的某个值

```
let array1: string[] = [" 张三 ", "马哒哒 ", "李四", " 阿尼玛", "", "王五", "李四", "王五五"];
ArrayUtil.remove(array1, "王五");
```

## 创作不易，请给童长老点赞👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   

