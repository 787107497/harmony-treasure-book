# harmony-utils之AssetUtil，关键资产存储服务工具类

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

##### canIUse  当前设备是否支持该模块

```
let canIUse = AssetUtil.canIUse();
ToastUtil.showToast(`当前设备是否支持该模块：${canIUse}`);
```

##### add  新增一条关键资产

```
AssetUtil.add("key_harmony", "我是异步知产X!").then(() => {
  ToastUtil.showToast(`新增资产成功！`);
});

AssetUtil.addSync("key_harmony_sync", "我是同步知产X!");
ToastUtil.showToast(`新增资产成功！`);
```

##### get  查询关键资产

```
let rStr = await AssetUtil.get("key_harmony");
ToastUtil.showToast(`取值: ${rStr}`);

let sStr = AssetUtil.getSync("key_harmony_sync");
ToastUtil.showToast(`同步：${sStr}`);
```

##### remove  删除关键资产

```
AssetUtil.remove("key_harmony").then(() => {
  ToastUtil.showToast("移除成功！");
});

AssetUtil.removeSync("key_harmony_sync");
ToastUtil.showToast("移除成功!");
```


## 示例代码

------

```
import { router } from '@kit.ArkUI';
import { DescribeBean } from '../../model/DescribeBean';
import { MockSetup } from '@ohos/hamock';
import { AssetUtil, LogUtil, ToastUtil } from '@pura/harmony-utils';
import { TitleBarView } from '../../component/TitleBarView';

/**
 * 关键资产存储服务工具类
 */
@Entry
@Component
struct Index {
  private scroller: Scroller = new Scroller();
  @State describe: DescribeBean = router.getParams() as DescribeBean;
  @State readonly rkey: string = "key_harmony"
  @State readonly skey: string = "key_harmony_sync"

  @MockSetup
  mock() {
    this.describe = new DescribeBean("AssetUtil", "关键资产存储服务工具类");
  }

  build() {
    Column() {
      TitleBarView({ describe: this.describe })
      Divider()
      Scroll(this.scroller) {
        Column() {
          Button("canIUse")
            .btnStyle()
            .onClick(() => {
              let canIUse = AssetUtil.canIUse();
              ToastUtil.showToast(`当前设备是否支持该模块：${canIUse}`);
            })
          Button("add")
            .btnStyle()
            .onClick(() => {
              AssetUtil.add(this.rkey, "我是异步知产X!").then(() => {
                ToastUtil.showToast(`新增资产成功！`);
              });
            })
          Button("get")
            .btnStyle()
            .onClick(async () => {
              let rStr = await AssetUtil.get(this.rkey);
              ToastUtil.showToast(`取值: ${rStr}`);
              LogUtil.error(`取值: ${rStr}`);
            })
          Button("addSync")
            .btnStyle()
            .onClick(() => {
              AssetUtil.addSync(this.skey, "我是同步知产X!");
              ToastUtil.showToast(`新增资产成功！`);
            })
          Button("getSync")
            .btnStyle()
            .onClick(() => {
              let sStr = AssetUtil.getSync(this.skey);
              ToastUtil.showToast(`同步：${sStr}`);
            })
          Button("remove")
            .btnStyle()
            .onClick(() => {
              AssetUtil.remove(this.rkey).then(() => {
                ToastUtil.showToast("移除成功！");
              });
            })
          Button("removeSync")
            .btnStyle()
            .onClick(() => {
              AssetUtil.removeSync(this.skey);
              ToastUtil.showToast("移除成功!");
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
   

