# Harmony-utils ArrayUtil, collection tool class

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

##### isNotEmpty determines whether the set is a non-empty set

```
let array0: string[] = []
let array1: string[] = [" 张三 ", "马哒哒 ", "李四", " 阿尼玛", "", "王五", "李四", "王五五", ""]
let b1 = ArrayUtil.isNotEmpty(array0);
let b3 = ArrayUtil.isNotEmpty(array1);
```

##### isEmpty determines whether the set is an empty set

```
let array0: string[] = []
let array1: string[] = [" 张三 ", "马哒哒 ", "李四", " 阿尼玛", "", "王五", "李四", "王五五", ""]
let b2 = ArrayUtil.isEmpty(array0);
let b4 = ArrayUtil.isEmpty(array1);
```

##### removeEmpty Removes null values ​​in string array

```
let array: string[] = [" 张三 ", "null", "希大大 ", "李四", "undefined", " 阿超", '', "王五 ", ""];
let arr1 = ArrayUtil.removeEmpty(array); //去空
```

##### trim Removes the spaces before and after each value of the string array

```
let array: string[] = [" 张三 ", "null", "希大大 ", "李四", "undefined", " 阿超", '', "王五 ", ""];
let arr2 = ArrayUtil.trim(array); //去空格
```

##### distinct deduplication of the array, and after deduplication, generate a new array, the original array remains unchanged

```
let array2: string[] = ["张三 ", "马哒哒 ", "李四", " 阿尼玛", "李四", "王五", "李四", "王五"];
let array = ArrayUtil.distinct(array2); //去重
```

##### reverse reverse the array, which will modify the original array

```
let array4: number[] = [1, 100, 10, 0, 22, 68, 11];
let array = ArrayUtil.reverse(array4);
```

##### filter array filtering, filtering and returning required elements through filter function implementation

```
let array4: number[] = [1, 100, 10, 0, 22, 68, 11];
let array1 = ArrayUtil.filter(array4, (item) => item > 10);
```

##### append splicing data, using extension operators, does not affect the original array

```
let array2: string[] = ["张三 ", "马哒哒 ", "李四", " 阿尼玛", "李四", "王五", "李四", "王五"];
let array3: string[] = ["黑龙江省", "哈尔滨市", "道里区", "砂山", "砀山", "高薪区"];
let array = ArrayUtil.append(array2, array3);
```

##### min Gets the minimum value of the array (value, string, date)

```
let array4: number[] = [1, 100, 10, 0, 22, 68, 11];
let min = ArrayUtil.min(array4);
```

##### max Gets the maximum value of the array (value, string, date)

```
let array4: number[] = [1, 100, 10, 0, 22, 68, 11];
let max = ArrayUtil.max(array4);
```

##### flatten tiled two-dimensional array

```
let array1: string[] = [" 张三 ", "马哒哒 ", "李四", " 阿尼玛", "", "王五", "李四", "王五五", ""]
let array2: string[] = ["张三 ", "马哒哒 ", "李四", " 阿尼玛", "李四", "王五", "李四", "王五"]
let array3: string[] = ["黑龙江省", "哈尔滨市", "道里区", "砂山", "砀山", "高薪区"]
let array5: string[][] = [array1, array2, array3];
let array = ArrayUtil.flatten(array5);
```

##### union tiles two-dimensional arrays and deduplication

```
let array1: string[] = [" 张三 ", "马哒哒 ", "李四", " 阿尼玛", "", "王五", "李四", "王五五", ""]
let array2: string[] = ["张三 ", "马哒哒 ", "李四", " 阿尼玛", "李四", "王五", "李四", "王五"];
let array3: string[] = ["黑龙江省", "哈尔滨市", "道里区", "砂山", "砀山", "高薪区"]
let array5: string[][] = [array1, array2, array3];
let array = ArrayUtil.union(array5);
```

##### chunk array chunking

```
let array2: string[] = ["张三 ", "马哒哒 ", "李四", " 阿尼玛", "李四", "王五", "李四", "王五"];
let array = ArrayUtil.chunk(array2, 2);
```

##### contains determines whether the set contains a certain value

```
let array1: string[] = [" 张三 ", "马哒哒 ", "李四", " 阿尼玛", "", "王五", "李四", "王五五"];
let array = ArrayUtil.contain(array1, "王五");
```

##### remove Remove a value from the collection

```
let array1: string[] = [" 张三 ", "马哒哒 ", "李四", " 阿尼玛", "", "王五", "李四", "王五五"];
ArrayUtil.remove(array1, "王五");
```

## Creation is not easy, please give Elder Tong a thumbs up 👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   

