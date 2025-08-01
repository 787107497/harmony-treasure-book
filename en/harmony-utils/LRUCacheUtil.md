# Harmony-utils LRUCacheUtil, LRUCache cache tool class

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

##### getInstance Gets a single case of LRUCacheUtil

```
 private lruCache: LRUCacheUtil = LRUCacheUtil.getInstance();
```

##### has to determine whether the cache corresponding to the key is included

```
let pwd = this.lruCache.has("pwd");
ToastUtil.showToast(`缓存是否存在：${pwd}`);
```

##### put add cache to lruCache

```
 this.lruCache.put("pwd", "abcd@12345");
 ToastUtil.showToast("缓存密码成功");
```

##### get get the cache corresponding to the key

```
let pwd = this.lruCache.get<string>("pwd");
ToastUtil.showToast(`取值：${pwd}`);
```

##### remove delete the cache corresponding to the key

```
this.lruCache.remove("pwd");
ToastUtil.showToast(`删除成功！`);
```

##### isEmpty determines whether the lruCache cache is empty

```
let blEmpty = this.lruCache.isEmpty();
ToastUtil.showToast(`缓存是否为空：${blEmpty}`);
```

##### getCapacity Gets the capacity of the current buffer

```
 let count = this.lruCache.getCapacity();
 ToastUtil.showToast(`当前缓冲区的容量：${count}`);
```

##### updateCapacity Reset the capacity of lruCache

```
this.lruCache.updateCapacity(128);
ToastUtil.showToast(`重新设置lruCache的容量成功`);
```

##### clear clear cache data and reset lruCache size

```
this.lruCache.clear();
ToastUtil.showToast(`清除缓存数据成功`);
```

## Full Code Example

------

```
import { router } from '@kit.ArkUI';
import { MockSetup } from '@ohos/hamock';
import { LRUCacheUtil, ToastUtil } from '@pura/harmony-utils';
import { TitleBarView } from '../../component/TitleBarView';
import { DescribeBean } from '../../model/DescribeBean';

/**
 * "LRUCache缓存工具类
 */
@Entry
@Component
struct Index {
  private scroller: Scroller = new Scroller();
  @State describe: DescribeBean = router.getParams() as DescribeBean;
  private lruCache: LRUCacheUtil = LRUCacheUtil.getInstance();

  @MockSetup
  mock() {
    this.describe = new DescribeBean("LRUCacheUtil", "LRUCache缓存工具类");
  }


  build() {
    Column() {
      TitleBarView({ describe: this.describe })
      Divider()
      Scroll(this.scroller) {
        Column() {
          Button("put()")
            .btnStyle()
            .onClick(() => {
              this.lruCache.put("pwd", "abcd@12345");
              ToastUtil.showToast("缓存密码成功");
            })
          Button("get()")
            .btnStyle()
            .onClick(() => {
              let pwd = this.lruCache.get<string>("pwd");
              ToastUtil.showToast(`取值：${pwd}`);
            })
          Button("has()")
            .btnStyle()
            .onClick(() => {
              let pwd = this.lruCache.has("pwd");
              ToastUtil.showToast(`缓存是否存在：${pwd}`);
            })
          Button("remove()")
            .btnStyle()
            .onClick(() => {
              this.lruCache.remove("pwd");
              ToastUtil.showToast(`删除成功！`);
            })
          Button("isEmpty()")
            .btnStyle()
            .onClick(() => {
              let blEmpty = this.lruCache.isEmpty();
              ToastUtil.showToast(`缓存是否为空：${blEmpty}`);
            })
          Button("getCapacity()")
            .btnStyle()
            .onClick(() => {
              let count = this.lruCache.getCapacity();
              ToastUtil.showToast(`当前缓冲区的容量：${count}`);
            })
          Button("updateCapacity()")
            .btnStyle()
            .onClick(() => {
              this.lruCache.updateCapacity(128);
              ToastUtil.showToast(`重新设置lruCache的容量成功`);
            })
          Button("clear()")
            .btnStyle()
            .onClick(() => {
              this.lruCache.clear();
              ToastUtil.showToast(`清除缓存数据成功`);
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
   

