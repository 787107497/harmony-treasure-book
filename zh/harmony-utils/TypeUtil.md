# harmony-utils之TypeUtil，类型检查工具类

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

##### isBoolean  判断是否是Boolean类型

```
let bl1 = TypeUtil.isBoolean(true);
let bl2 = TypeUtil.isBoolean("true");
```

##### isNumber  判断是否是Number类型

```
let num1 = TypeUtil.isNumber(188);
let num2 = TypeUtil.isNumber("188");
```

##### isString  判断是否是String类型

```
let str1 = TypeUtil.isString("哈哈");
let str2 = TypeUtil.isString(null);
```

##### isObject  判断是否是Object类型

```
let obj1 = TypeUtil.isObject(new User());
let obj2 = TypeUtil.isObject("Object");
```

##### isArray  判断是否是数组类型

```
let array: string[] = ["黑龙江省", "哈尔滨市", "道里区", "砂山", "砀山", "高薪区"];
let isArray1 = TypeUtil.isArray(array);
let isArray2 = TypeUtil.isArray([]);
let isArray3 = TypeUtil.isArray("哈哈哈");
```

##### isResource  判断是否是Resource类型

```
let bl1 = TypeUtil.isResource($r('app.string.app_name'));
let bl2 = TypeUtil.isResource("哈哈哈");
let bl3 = TypeUtil.isResource(new User());
let bl4 = TypeUtil.isResource(null);
```

##### isResourceStr  判断是否是ResourceStr类型

```
let bl5 = TypeUtil.isResourceStr($r('app.string.app_name'));
let bl6 = TypeUtil.isResourceStr("哈哈哈");
let bl7 = TypeUtil.isResourceStr(undefined);
```

##### isFunction  判断是否是函数类型

```
let isFunction = TypeUtil.isFunction(this.aboutToAppear);
```

##### isMap  检查是否为Map类型

```
let map = new Map<string, object>();
let isMap = TypeUtil.isMap(map);
```

##### isWeakMap  检查是否为WeakMap类型

```
let weakMap: WeakMap<object, number> = new WeakMap();
let isWeakMap = TypeUtil.isWeakMap(weakMap);
```

##### isSet  检查是否为Set类型

```
let set: Set<number> = new Set();
let isSet = TypeUtil.isSet(set);
```

##### isWeakSet  检查是否为WeakSet类型

```
let weakSet = new WeakSet();
let isWeakSet = TypeUtil.isWeakSet(weakSet);
```

##### isDate  检查是否为Date类型

```
let isDate = TypeUtil.isDate(new Date());
```

##### isArrayBuffer  检查是否为ArrayBuffer类型

```
let isArrayBuffer = TypeUtil.isArrayBuffer(new ArrayBuffer(0));
```

##### isSharedArrayBuffer  检查是否为SharedArrayBuffer类型

```
let isSharedArrayBuffer = TypeUtil.isSharedArrayBuffer(new SharedArrayBuffer(0));
```

##### isAnyArrayBuffer  检查是否为ArrayBuffer或SharedArrayBuffer类型

```
let isAnyArrayBuffer = TypeUtil.isAnyArrayBuffer(new ArrayBuffer(0));
```

##### isUint8Array  检查是否为Uint8Array数组类型

```
let isUint8Array = TypeUtil.isUint8Array(new Uint8Array([]));
```

##### isUint16Array  检查是否为Uint16Array数组类型

```
let isUint16Array = TypeUtil.isUint16Array(new Uint16Array([]));
```

##### isUint32Array  检查是否为Uint32Array数组类型

```
let isUint32Array = TypeUtil.isUint32Array(new Uint32Array([]));
```

##### isInt8Array  检查是否为Int8Array数组类型

```
let isInt8Array = TypeUtil.isInt8Array(new Int8Array([]));
```

##### isInt16Array  检查是否为Int16Array数组类型

```
let isInt16Array = TypeUtil.isInt16Array(new Int16Array([]));
```

##### isInt32Array  检查是否为Int32Array数组类型

```
let isInt32Array = TypeUtil.isInt32Array(new Int32Array([]));
```

##### isTypedArray  检查是否为TypedArray类型

```
let isTypedArray = TypeUtil.isTypedArray(new Float64Array([]));
```

##### isAsyncFunction  检查是否为异步函数类型

```
let isAsyncFunction = TypeUtil.isAsyncFunction(this.aboutToAppear);
```

##### isPromise  检查是否为Promise类型

```
let isPromise = TypeUtil.isPromise(Promise.resolve(1));
```

##### isProxy  检查是否为Proxy类型

```
let user = new User();
const proxy = new Proxy(user, user as ProxyHandler<User>);
let isProxy = TypeUtil.isProxy(proxy);
```

##### isRegExp  检查是否为RegExp类型

```
let isRegExp = TypeUtil.isRegExp(new RegExp('abc'));
```

##### isDataView  检查是否为DataView类型

```
let dataView = new DataView(new ArrayBuffer(20));
let isDataView = TypeUtil.isDataView(dataView);
```

##### isExternal  检查是否为native External类型

```
let isExternal = TypeUtil.isNativeError("");
```

##### isNativeError  检查是否为Error类型

```
let isNativeError1 = TypeUtil.isNativeError(new TypeError());
let isNativeError2 = TypeUtil.isNativeError(new URIError());
let isNativeError3 = TypeUtil.isNativeError("");
```

## 创作不易，请给童长老点赞👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   



