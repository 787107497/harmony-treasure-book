# EmitterUtil, Emitter tool class

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

##### post send event

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

##### onSubscribe Subscription Events

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

##### onceSubscribe Specified Events for Single Subscription

```
EmitterUtil.onceSubscribe<string>(10001, (data) => {
  this.txtStr = `单次事件(string)：\n${JSON.stringify(data, null, 2)}`;
  LogUtil.error(this.txtStr);
});
```

##### unSubscribe Unsubscribe

```
 EmitterUtil.unSubscribe("S123456"); //取消事件订阅
 EmitterUtil.unSubscribe("N123456"); //取消事件订阅
 EmitterUtil.unSubscribe("O123456"); //取消事件订阅
```

##### getListenerCount Gets the number of subscriptions for the specified event

```
let count = EmitterUtil.getListenerCount("O123456");
LogUtil.error(`获取指定事件的订阅数：${count}`);
```

##### on Subscribe to events, support Callback

```
private callback: Callback<emitter.GenericEventData<string>> = (eventData) => {
  let txtStr = eventData.data as string;
  LogUtil.error(txtStr);
};
EmitterUtil.on<string>(100, callback);
```

##### once a single subscription to the specified event, support Callback

```
private callback: Callback<emitter.GenericEventData<string>> = (eventData) => {
  let txtStr = eventData.data as string;
  LogUtil.error(txtStr);
};
EmitterUtil.once<string>(100, callback);
```

##### off Unsubscribe from event, support Callback

```
 EmitterUtil.off(100, callback);
```

## Full Code Example

------

```
import { router } from '@kit.ArkUI';
import { DescribeBean } from '../../model/DescribeBean';
import { MockSetup } from '@ohos/hamock';
import { EmitterUtil, LogUtil, StrUtil } from '@pura/harmony-utils';
import { emitter } from '@kit.BasicServicesKit';
import { TitleBarView } from '../../component/TitleBarView';


/**
 * Emitter工具类（进行线程间通信）
 */
@Entry
@Component
struct Index {
  private scroller: Scroller = new Scroller();
  @State describe: DescribeBean = router.getParams() as DescribeBean;
  @State txtStr: string = '';
  @State eventDataStr: string = '';
  private callback: Callback<emitter.GenericEventData<string>> = (eventData) => {
    if (StrUtil.isNotEmpty(this.eventDataStr)) {
      this.eventDataStr = this.eventDataStr + `\n事件1：\t${eventData.data}`;
      this.txtStr = this.eventDataStr
      LogUtil.error(this.txtStr);
    } else {
      this.eventDataStr = `事件1：\t${eventData.data}`;
      this.txtStr = this.eventDataStr;
    }
    LogUtil.error(`事件1X：\t${eventData.data}`)
  };


  @MockSetup
  mock() {
    this.describe = new DescribeBean("EmitterUtil", "Emitter工具类（进行线程间通信）");
  }

  aboutToAppear(): void {
    EmitterUtil.onSubscribe<string>("S123456", (data) => {
      this.txtStr = `事件(string)：\t${data}`;
      LogUtil.error(this.txtStr);
    });
    EmitterUtil.onSubscribe<number>("N123456", (data) => {
      this.txtStr = `事件(number)：\t${data}`;
      LogUtil.error(this.txtStr);
    });
    EmitterUtil.onSubscribe<boolean>("B123456", (data) => {
      this.txtStr = `事件(boolean)：\t${data}`;
      LogUtil.error(this.txtStr);
    });
    EmitterUtil.onSubscribe<Student>("O123456", (data) => {
      this.txtStr = `事件(对象)：\n${JSON.stringify(data, null, 2)}`;
      LogUtil.error(this.txtStr);
    });
    EmitterUtil.onceSubscribe<string>(10001, (data) => {
      this.txtStr = `单次事件(string)：\n${JSON.stringify(data, null, 2)}`;
      LogUtil.error(this.txtStr);
    });
  }


  aboutToDisappear(): void {
    EmitterUtil.unSubscribe("S123456"); //取消事件订阅
    EmitterUtil.unSubscribe("N123456"); //取消事件订阅
    EmitterUtil.unSubscribe("O123456"); //取消事件订阅
  }


  build() {
    Column() {
      TitleBarView({ describe: this.describe })
      Divider()
      Scroll(this.scroller) {
        Column() {
          Button("发送事件（string）")
            .btnStyle()
            .onClick(() => {
              EmitterUtil.post<string>("S123456", "哈哈哈哈哈哈哈哈哈哈", emitter.EventPriority.LOW);
            })
          Button("发送事件（number）")
            .btnStyle()
            .onClick(() => {
              EmitterUtil.post<number>("N123456", 90123456789);
            })
          Button("发送事件（boolean）")
            .btnStyle()
            .onClick(() => {
              EmitterUtil.post<boolean>("B123456", false);
            })
          Button("发送事件（对象）")
            .btnStyle()
            .onClick(() => {
              let student: Student = {
                id: "NO_1234567809",
                name: "小宝子",
                age: 18,
                sex: "男"
              }
              EmitterUtil.post<Student>("O123456", student);
            })
          Button("发送事件（单次订阅指定事件）")
            .btnStyle()
            .onClick(() => {
              EmitterUtil.post<string>(10001, "单次订阅指定事件-消息");
            })
          Button("获取指定事件的订阅数")
            .btnStyle()
            .onClick(() => {
              let count = EmitterUtil.getListenerCount("O123456");
              LogUtil.error(`获取指定事件的订阅数：${count}`);
            })

          Divider().margin(12)

          Button("订阅事件-1")
            .btnStyle()
            .onClick(() => {
              EmitterUtil.on<string>(100, this.callback);
            })
          Button("订阅事件-2")
            .btnStyle()
            .onClick(() => {
              EmitterUtil.on<string>(100, (eventData) => {
                if (StrUtil.isNotEmpty(this.eventDataStr)) {
                  this.eventDataStr = this.eventDataStr + `\n事件2：\t${eventData.data}`;
                  this.txtStr = this.eventDataStr
                  LogUtil.error(this.txtStr);
                } else {
                  this.eventDataStr = `事件2：\t${eventData.data}`;
                  this.txtStr = this.eventDataStr;
                }
                LogUtil.error(`事件2X：\t${eventData.data}`)
              });
            })
          Button("发送事件")
            .btnStyle()
            .onClick(() => {
              this.eventDataStr = ""
              EmitterUtil.post<string>(100, "一款功能丰富且极易上手的HarmonyOS工具库");
            })
          Button("取消事件订阅(指定callback)")
            .btnStyle()
            .onClick(() => {
              EmitterUtil.off(100,this.callback);
            })
          Button("取消事件订阅（所有）")
            .btnStyle()
            .onClick(() => {
              EmitterUtil.unSubscribe(100);
            })

          Blank().layoutWeight(1)

          Text(this.txtStr)
            .visibility(StrUtil.isNotEmpty(this.txtStr) ? Visibility.Visible : Visibility.None)
            .textStyle()
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

@Styles
function textStyle() {
  .width('95%')
  .padding(10)
  .shadow(ShadowStyle.OUTER_DEFAULT_XS)
  .margin({ top: 5, bottom: 10 })
  .border({
    width: 1,
    color: Color.Grey,
    radius: 10,
    style: BorderStyle.Dashed
  })
}


/**
 * 学生对象 */
interface Student {
  id: string;
  name: string;
  age: number;
  sex: string;
}
```


## Creation is not easy, please give Elder Tong a thumbs up 👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   




