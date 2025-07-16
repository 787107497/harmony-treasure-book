# ObjectUtil of harmony-utils, object tool class

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

## Full Code Example

------

```
import { router } from '@kit.ArkUI';
import { MockSetup } from '@ohos/hamock';
import { DialogHelper } from '@pura/harmony-dialog';
import { ObjectUtil } from '@pura/harmony-utils';
import { TitleBarView } from '../../component/TitleBarView';
import { DescribeBean } from '../../model/DescribeBean';
import { User } from '../../model/User';
import { Utils } from '../../utils/Utils';


/**
 * 对象工具类
 */
@Entry
@Component
struct Index {
  private scroller: Scroller = new Scroller();
  @State describe: DescribeBean = router.getParams() as DescribeBean;
  @State user: User = new User();
  @State obj: String = new String("abcd@1234");
  @State obj1: String = new String();
  readonly userJsonStr = '{"id":"No_1060700","name":"李四","age":23}';

  @MockSetup
  mock() {
    this.describe = new DescribeBean("ObjectUtil", "对象工具类");
  }

  build() {
    Column() {
      TitleBarView({ describe: this.describe })
      Divider()
      Scroll(this.scroller) {
        Column() {
          Button("getHash()")
            .btnStyle()
            .onClick(() => {
              let hash1 = ObjectUtil.getHash(this.user);
              let hash2 = ObjectUtil.getHash(this.describe);
              let str = `hash1: ${hash1}\n\nhash2: ${hash2}`;
              Utils.showSheetText(str);
            })
          Button("getClassName()")
            .btnStyle()
            .onClick(() => {
              let name1 = ObjectUtil.getClassName(this.user);
              let name2 = ObjectUtil.getClassName(this.describe);
              let str = `name1: ${name1}\n\nname2: ${name2}`
              Utils.showSheetText(str);
            })
          Button("getMethodsNames()")
            .btnStyle()
            .onClick(() => {
              let methodsNames1 = ObjectUtil.getMethodsNames(this.user);
              let methodsNames2 = ObjectUtil.getMethodsNames(this.describe);
              let str = `User方法名: \n${methodsNames1}\n\nDescribe方法名: \n${methodsNames2}`
              Utils.showSheetText(str);
            })
          Button("isString()")
            .btnStyle()
            .onClick(() => {
              let bl1 = ObjectUtil.isString(this.user);
              let bl2 = ObjectUtil.isString(this.obj);
              let str = `bls1: ${bl1}\nbls2: ${bl2}`
              Utils.showSheetText(str);
            })
          Button("isNull()")
            .btnStyle()
            .onClick(() => {
              let bl1 = ObjectUtil.isNull(this.user);
              let bl2 = ObjectUtil.isNull(this.obj);
              let bl3 = ObjectUtil.isNull(this.obj1);
              let str = `bl1: ${bl1}\nbl2: ${bl2}\nbl3: ${bl3}`
              Utils.showSheetText(str);
            })
          Button("isEmpty()")
            .btnStyle()
            .onClick(() => {
              let bl1 = ObjectUtil.isEmpty(this.user);
              let bl2 = ObjectUtil.isEmpty(this.obj);
              let bl3 = ObjectUtil.isEmpty(this.obj1);
              let str = `bl1: ${bl1}\nbl2: ${bl2}\nbl3: ${bl3}`
              Utils.showSheetText(str);
            })
          Button("shallowCopy()")
            .btnStyle()
            .onClick(() => {
              let user: User = JSON.parse(this.userJsonStr);
              this.user.user = user;
              let user1 = ObjectUtil.shallowCopy(this.user);
              user.name = "苟富贵"; //浅拷贝，会打印出“苟富贵”
              let str = `user:\n${JSON.stringify(this.user)}\n\nuser1:\n${JSON.stringify(user1)}`
              Utils.showSheetText(str);
            })
          Button("deepCopy()")
            .btnStyle()
            .onClick(() => {
              let user: User = JSON.parse(this.userJsonStr);
              this.user.user = user;
              let user2: User = ObjectUtil.deepCopy(this.user);
              user.name = "李旺财";  //深拷贝，不会打印出“李旺财”
              let str = `user:\n${JSON.stringify(this.user)}\n\nuser2:\n${JSON.stringify(user2)}`
              Utils.showSheetText(str);
            })
          Button("assign()")
            .btnStyle()
            .onClick(() => {
              let user: User = JSON.parse(this.userJsonStr);
              let obj1: Record<string, Object> = { "xx_age": 20, "xx_name": "张呵呵" };
              let obj2: Record<string, Object> = { "my_age": 20, "my_name": "张叁三" };
              let user3 = ObjectUtil.assign(obj1, obj2, user);
              let str = `user:\n${JSON.stringify(user)}\n\nuser3:\n${JSON.stringify(user3)}`
              Utils.showSheetText(str);
            })
          Button("objToClass()")
            .btnStyle()
            .onClick(() => {
              let user: User = JSON.parse(this.userJsonStr);
              let user4 = ObjectUtil.objToClass(User, user);
              let str = `user:\n${JSON.stringify(user)}\n\nuser4:\n${JSON.stringify(user4)}`
              user4.say("烤包子......");
              Utils.showSheetText(str);
            })
          Button("deleteRecord()")
            .btnStyle()
            .onClick(() => {
              let record: Record<string, Object> = { "name": "张若楠", "age": 18, "work": "演员", "addr": "上海市" };
              let recordStr = JSON.stringify(record);
              ObjectUtil.deleteRecord(record,"work");
              let str = `record:\n${recordStr}\n\n删除work后:\n${JSON.stringify(record)}`;
              Utils.showSheetText(str);
            })
          Button("getValue()")
            .btnStyle()
            .onClick(() => {
              let name = ObjectUtil.getValue<string>(this.user, "name");
              DialogHelper.showToast(`对象 name：${name}`);
            })
          Button("setValue()")
            .btnStyle()
            .onClick(() => {
              let userStr = JSON.stringify(this.user);
              ObjectUtil.setValue(this.user, "name", "张若楠");
              ObjectUtil.setValue(this.user, "work", "演员");
              ObjectUtil.setValue(this.user, "job", "表演");
              let str = `user:\n${userStr}\n\n赋值后:\n${JSON.stringify(this.user)}`;
              Utils.showSheetText(str);
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
   

