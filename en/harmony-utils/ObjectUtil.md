# ObjectUtil of harmony-utils, object tool class

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

##### getHash Get the Hash value of the object

```
let user: User = new User();
let hash1 = ObjectUtil.getHash(user);
```

##### getClassName Gets the Class name of the object

```
let user: User = new User();
let name1 = ObjectUtil.getClassName(user);
```

##### getMethodsNames Get all method names of the object

```
let user: User = new User();
let methodsNames1 = ObjectUtil.getMethodsNames(this.user);
```

##### isString determines whether it is a String

```
let user: User = new User();
let obj: String = new String("abcd@1234");
let bl1 = ObjectUtil.isString(user);
let bl2 = ObjectUtil.isString(obj);
```

##### isNull determines whether the object is empty

```
let user: User = new User();
let bl1 = ObjectUtil.isString(user)
```

##### isEmpty determines whether the attribute content is empty

```
let user: User = new User();
let obj: String = new String();
let bl1 = ObjectUtil.isEmpty(user);
let bl2 = ObjectUtil.isEmpty(obj);
```

##### shallowCopy

```
let user: User = new User();
let user1 = ObjectUtil.shallowCopy(user);
```

##### deepCopy deep copy object

```
let user: User = new User();
let user2: User = ObjectUtil.deepCopy(user);
```

##### assign Merge two or more objects

```
let user: User = new User();
let obj1: Record<string, Object> = { "xx_age": 20, "xx_name": "张呵呵" };
let obj2: Record<string, Object> = { "my_age": 20, "my_name": "张叁三" };
let user3 = ObjectUtil.assign(obj1, obj2, user);
```

##### objToClass obj to class, solve the problem of missing method after obj as class

```
let user: User = new User();
let user4 = ObjectUtil.objToClass(User, user);
```

##### deleteRecord Delete elements in Record

```
let record: Record<string, Object> = { "name": "张若楠", "age": 18, "work": "演员", "addr": "上海市" };
let recordStr = JSON.stringify(record);
ObjectUtil.deleteRecord(record,"work");
```

##### getValue get object value through key

```
let user: User = new User();
let name = ObjectUtil.getValue<string>(user, "name");
```

##### setValue dynamically adds or modifys attributes to object obj

```
let user: User = new User();
ObjectUtil.setValue(user, "name", "张若喃");
ObjectUtil.setValue(user, "work", "女演员啊");
ObjectUtil.setValue(user, "job", "女演员");
```

## Creation is not easy, please give Elder Tong a thumbs up 👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   

