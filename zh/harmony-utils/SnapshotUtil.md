# harmony-utils之SnapshotUtil，截图相关工具类

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

##### get  获取已加载的组件的截图，传入组件的组件id，找到对应组件进行截图

```
let pixelMap1 = await SnapshotUtil.get('snapshot_id1');
let pixelMap2 = SnapshotUtil.getSync('snapshot_id2');
```

##### createFromBuilder  在应用后台渲染CustomBuilder自定义组件，并输出其截图

```
SnapshotUtil.createFromBuilder(() => {
  this.RandomBuilder()
}).then((pixelMap) => {
  Utils.showSheetImg(pixelMap);
}).catch((err: BusinessError) => {
  ToastUtil.showToast("组件生成图片异常！");
});

@Builder
RandomBuilder() {
  Column() {
    Text("Builder截图")
      .fontSize(20)
      .fontWeight(FontWeight.Bold)
      .fontStyle(FontStyle.Italic)
      .margin({ top: 20 })
    Image($r("app.media.test_as4"))
      .margin({ top: 30, bottom: 10 })
      .padding(10)
      .width('95%')
      .backgroundColor(Color.Pink)
  }
  .backgroundColor(Color.Blue)
  .padding(10)
  .width('100%')
  .aspectRatio(1)
  .margin({ top: 50 })
  .id("rBuilder")
}
```

##### snapshot  获取窗口截图，使用Promise异步回调

```
let pixelMap3 = await SnapshotUtil.snapshot();
```

##### onSnapshotListener  开启系统截屏事件的监听

```
SnapshotUtil.onSnapshotListener(() => {
  ToastUtil.showToast("系统截图了！");
  LogUtil.error("系统截图了！");
});
```

##### removeSnapshotListener  关闭系统截屏事件的监听

```
 SnapshotUtil.removeSnapshotListener();
 SnapshotUtil.removeSnapshotListener(snapshotCallBack);
```

## 创作不易，请给童长老点赞👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   

