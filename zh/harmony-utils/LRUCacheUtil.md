# harmony-utils之LRUCacheUtil，LRUCache缓存工具类

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

##### getInstance  获取LRUCacheUtil的单例

```
 private lruCache: LRUCacheUtil = LRUCacheUtil.getInstance();
```

##### has  判断是否包含key对应的缓存

```
let pwd = this.lruCache.has("pwd");
ToastUtil.showToast(`缓存是否存在：${pwd}`);
```

##### put  添加缓存到lruCache中

```
 this.lruCache.put("pwd", "abcd@12345");
 ToastUtil.showToast("缓存密码成功");
```

##### get  获取key对应的缓存

```
let pwd = this.lruCache.get<string>("pwd");
ToastUtil.showToast(`取值：${pwd}`);
```

##### remove  删除key对应的缓存

```
this.lruCache.remove("pwd");
ToastUtil.showToast(`删除成功！`);
```

##### isEmpty  判断lruCache缓存是否为空

```
let blEmpty = this.lruCache.isEmpty();
ToastUtil.showToast(`缓存是否为空：${blEmpty}`);
```

##### getCapacity  获取当前缓冲区的容量

```
 let count = this.lruCache.getCapacity();
 ToastUtil.showToast(`当前缓冲区的容量：${count}`);
```

##### updateCapacity   重新设置lruCache的容量

```
this.lruCache.updateCapacity(128);
ToastUtil.showToast(`重新设置lruCache的容量成功`);
```

##### clear  清除缓存数据，并重置lruCache的大小

```
this.lruCache.clear();
ToastUtil.showToast(`清除缓存数据成功`);
```


## 示例代码

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


## 创作不易，请给童长老点赞👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   

