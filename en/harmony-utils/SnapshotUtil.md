# Harmony-utils: SnapshotUtil, screenshot related tool class

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

##### get get a screenshot of the loaded component, pass in the component id of the component, find the corresponding component to take a screenshot

```
let pixelMap1 = await SnapshotUtil.get('snapshot_id1');
let pixelMap2 = SnapshotUtil.getSync('snapshot_id2');
```

##### createFromBuilder renders CustomBuilder custom components in the application background and outputs screenshots

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

##### snapshot to get window screenshot and use Promise asynchronous callback

```
let pixelMap3 = await SnapshotUtil.snapshot();
```

##### onSnapshotListener enables monitoring of system screenshot events

```
SnapshotUtil.onSnapshotListener(() => {
  ToastUtil.showToast("系统截图了！");
  LogUtil.error("系统截图了！");
});
```

##### removeSnapshotListener Close listening of system screenshot events

```
 SnapshotUtil.removeSnapshotListener();
 SnapshotUtil.removeSnapshotListener(snapshotCallBack);
```

## Creation is not easy, please give Elder Tong a thumbs up 👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   

