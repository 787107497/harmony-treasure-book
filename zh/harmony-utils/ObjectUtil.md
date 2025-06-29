# harmony-utils之ObjectUtil，对象工具类

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

##### getHash  获取对象的Hash值

```
let user: User = new User();
let hash1 = ObjectUtil.getHash(user);
```

##### getClassName  获取对象的Class名称

```
let user: User = new User();
let name1 = ObjectUtil.getClassName(user);
```

##### getMethodsNames  获取对象的所有方法名

```
let user: User = new User();
let methodsNames1 = ObjectUtil.getMethodsNames(this.user);
```

##### isString  判断是否是String

```
let user: User = new User();
let obj: String = new String("abcd@1234");
let bl1 = ObjectUtil.isString(user);
let bl2 = ObjectUtil.isString(obj);
```

##### isNull  判断对象是否为空

```
let user: User = new User();
let bl1 = ObjectUtil.isString(user)
```

##### isEmpty  判断属性内容是否为空

```
let user: User = new User();
let obj: String = new String();
let bl1 = ObjectUtil.isEmpty(user);
let bl2 = ObjectUtil.isEmpty(obj);
```

##### shallowCopy  浅拷贝

```
let user: User = new User();
let user1 = ObjectUtil.shallowCopy(user);
```

##### deepCopy  深度拷贝对象

```
let user: User = new User();
let user2: User = ObjectUtil.deepCopy(user);
```

##### assign  合并两个或多个对象

```
let user: User = new User();
let obj1: Record<string, Object> = { "xx_age": 20, "xx_name": "张呵呵" };
let obj2: Record<string, Object> = { "my_age": 20, "my_name": "张叁三" };
let user3 = ObjectUtil.assign(obj1, obj2, user);
```

##### objToClass  obj转class，解决obj as class后丢失方法的问题

```
let user: User = new User();
let user4 = ObjectUtil.objToClass(User, user);
```

##### deleteRecord  删除Record中的元素

```
let record: Record<string, Object> = { "name": "张若楠", "age": 18, "work": "演员", "addr": "上海市" };
let recordStr = JSON.stringify(record);
ObjectUtil.deleteRecord(record,"work");
```

##### getValue  通过key获取对象值

```
let user: User = new User();
let name = ObjectUtil.getValue<string>(user, "name");
```

##### setValue  给对象obj动态添加或者修改属性

```
let user: User = new User();
ObjectUtil.setValue(user, "name", "张若喃");
ObjectUtil.setValue(user, "work", "女演员啊");
ObjectUtil.setValue(user, "job", "女演员");
```

## 创作不易，请给童长老点赞👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   

