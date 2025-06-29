# harmony-utils之EmitterUtil，Emitter工具类

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

##### post  发送事件

```
EmitterUtil.post<string>("S123456", "哈哈哈哈哈哈哈哈哈哈", emitter.EventPriority.LOW);
EmitterUtil.post<number>("N123456", 90123456789);
EmitterUtil.post<boolean>("B123456", false);

let student: Student = {
  id: "NO_1234567809",
  name: "小宝子",
  age: 18,
  sex: "男"
}
EmitterUtil.post<Student>("O123456", student);
```

##### onSubscribe  订阅事件

```
EmitterUtil.onSubscribe<string>("S123456", (data) => {
  this.txtStr = `事件(string)：\t${data}`;
  LogUtil.error(this.txtStr);
});
EmitterUtil.onSubscribe<number>("N123456", (data) => {
  this.txtStr = `事件(number)：\t${data}`;
  LogUtil.error(this.txtStr);
});
EmitterUtil.onSubscribe<boolean>("B123456", (data) => {
  let txtStr = `事件(boolean)：\t${data}`;
  LogUtil.error(txtStr);
});
```

##### onceSubscribe  单次订阅指定事件

```
EmitterUtil.onceSubscribe<string>(10001, (data) => {
  this.txtStr = `单次事件(string)：\n${JSON.stringify(data, null, 2)}`;
  LogUtil.error(this.txtStr);
});
```

##### unSubscribe  取消事件订阅

```
 EmitterUtil.unSubscribe("S123456"); //取消事件订阅
 EmitterUtil.unSubscribe("N123456"); //取消事件订阅
 EmitterUtil.unSubscribe("O123456"); //取消事件订阅
```

##### getListenerCount  获取指定事件的订阅数

```
let count = EmitterUtil.getListenerCount("O123456");
LogUtil.error(`获取指定事件的订阅数：${count}`);
```

##### on  订阅事件，支持Callback

```
private callback: Callback<emitter.GenericEventData<string>> = (eventData) => {
  let txtStr = eventData.data as string;
  LogUtil.error(txtStr);
};
EmitterUtil.on<string>(100, callback);
```

##### once  单次订阅指定事件，支持Callback

```
private callback: Callback<emitter.GenericEventData<string>> = (eventData) => {
  let txtStr = eventData.data as string;
  LogUtil.error(txtStr);
};
EmitterUtil.once<string>(100, callback);
```

##### off  取消事件订阅，支持Callback

```
 EmitterUtil.off(100, callback);
```

## 创作不易，请给童长老点赞👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   




