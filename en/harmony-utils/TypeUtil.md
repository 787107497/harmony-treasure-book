# harmony-utils TypeUtil, type checking tool class

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

##### isBoolean Determine whether it is Boolean type

```
let bl1 = TypeUtil.isBoolean(true);
let bl2 = TypeUtil.isBoolean("true");
```

##### isNumber determines whether it is the Number type

```
let num1 = TypeUtil.isNumber(188);
let num2 = TypeUtil.isNumber("188");
```

##### isString determines whether it is String type

```
let str1 = TypeUtil.isString("哈哈");
let str2 = TypeUtil.isString(null);
```

##### isObject determines whether it is Object type

```
let obj1 = TypeUtil.isObject(new User());
let obj2 = TypeUtil.isObject("Object");
```

##### isArray determines whether it is an array type

```
let array: string[] = ["黑龙江省", "哈尔滨市", "道里区", "砂山", "砀山", "高薪区"];
let isArray1 = TypeUtil.isArray(array);
let isArray2 = TypeUtil.isArray([]);
let isArray3 = TypeUtil.isArray("哈哈哈");
```

##### isResource determines whether it is Resource type

```
let bl1 = TypeUtil.isResource($r('app.string.app_name'));
let bl2 = TypeUtil.isResource("哈哈哈");
let bl3 = TypeUtil.isResource(new User());
let bl4 = TypeUtil.isResource(null);
```

##### isResourceStr Determines whether it is ResourceStr type

```
let bl5 = TypeUtil.isResourceStr($r('app.string.app_name'));
let bl6 = TypeUtil.isResourceStr("哈哈哈");
let bl7 = TypeUtil.isResourceStr(undefined);
```

##### isFunction determines whether it is a function type

```
let isFunction = TypeUtil.isFunction(this.aboutToAppear);
```

##### isMap Check whether it is Map type

```
let map = new Map<string, object>();
let isMap = TypeUtil.isMap(map);
```

##### isWeakMap Check whether it is WeakMap type

```
let weakMap: WeakMap<object, number> = new WeakMap();
let isWeakMap = TypeUtil.isWeakMap(weakMap);
```

##### isSet Check whether it is Set type

```
let set: Set<number> = new Set();
let isSet = TypeUtil.isSet(set);
```

##### isWeakSet Check whether it is WeakSet type

```
let weakSet = new WeakSet();
let isWeakSet = TypeUtil.isWeakSet(weakSet);
```

##### isDate Check whether it is Date type

```
let isDate = TypeUtil.isDate(new Date());
```

##### isArrayBuffer Check whether it is ArrayBuffer type

```
let isArrayBuffer = TypeUtil.isArrayBuffer(new ArrayBuffer(0));
```

##### isSharedArrayBuffer Check whether it is SharedArrayBuffer type

```
let isSharedArrayBuffer = TypeUtil.isSharedArrayBuffer(new SharedArrayBuffer(0));
```

##### isAnyArrayBuffer Check whether it is an ArrayBuffer or SharedArrayBuffer type

```
let isAnyArrayBuffer = TypeUtil.isAnyArrayBuffer(new ArrayBuffer(0));
```

##### isUint8Array Check whether it is a Uint8Array array type

```
let isUint8Array = TypeUtil.isUint8Array(new Uint8Array([]));
```

##### isUint16Array Check whether it is a Uint16Array array type

```
let isUint16Array = TypeUtil.isUint16Array(new Uint16Array([]));
```

##### isUint32Array Check whether it is a Uint32Array array type

```
let isUint32Array = TypeUtil.isUint32Array(new Uint32Array([]));
```

##### isInt8Array Check whether it is an Int8Array array type

```
let isInt8Array = TypeUtil.isInt8Array(new Int8Array([]));
```

##### isInt16Array Check whether it is an Int16Array array type

```
let isInt16Array = TypeUtil.isInt16Array(new Int16Array([]));
```

##### isInt32Array Check whether it is an Int32Array array type

```
let isInt32Array = TypeUtil.isInt32Array(new Int32Array([]));
```

##### isTypedArray Check whether it is TypedArray

```
let isTypedArray = TypeUtil.isTypedArray(new Float64Array([]));
```

##### isAsyncFunction Checks whether it is an asynchronous function type

```
let isAsyncFunction = TypeUtil.isAsyncFunction(this.aboutToAppear);
```

##### isPromise Check whether it is a Promise type

```
let isPromise = TypeUtil.isPromise(Promise.resolve(1));
```

##### isProxy Check whether it is Proxy type

```
let user = new User();
const proxy = new Proxy(user, user as ProxyHandler<User>);
let isProxy = TypeUtil.isProxy(proxy);
```

##### isRegExp Check whether it is RegExp type

```
let isRegExp = TypeUtil.isRegExp(new RegExp('abc'));
```

##### isDataView Check whether it is of DataView type

```
let dataView = new DataView(new ArrayBuffer(20));
let isDataView = TypeUtil.isDataView(dataView);
```

##### isExternal Check whether it is native External type

```
let isExternal = TypeUtil.isNativeError("");
```

##### isNativeError Check whether it is Error type

```
let isNativeError1 = TypeUtil.isNativeError(new TypeError());
let isNativeError2 = TypeUtil.isNativeError(new URIError());
let isNativeError3 = TypeUtil.isNativeError("");
```

## Creation is not easy, please give Elder Tong a thumbs up 👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   



