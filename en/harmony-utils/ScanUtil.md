# ScanUtils, code tool class (scan code, code image generation, picture identification)

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

##### startScanForResult calls the default interface to scan the code, and use the Promise method to asynchronously return the decoded result.

```
ScanUtil.startScanForResult().then((scanResult) => {
  let scanStr1 = JSON.stringify(scanResult, null, 2);
});
```

##### generateBarcode code diagram generation, use Promise to asynchronously return the generated code diagram

```
let txtStr = "harmony-utils 一款高效的OpenHarmony/HarmonyOS工具包，封装了常用工具类，提供一系列简单易用的方法";
let pixelMap = await ScanUtil.generateBarcode(txtStr);
ImageUtil.savePixelMap(pixelMap, FileUtil.getFilesDirPath(""), "qr_code.png");
```

##### decode calls picture identification and uses Promise to return the identification result asynchronously

```
let filePath = FileUtil.getFilesDirPath("","qr_code.png");
if (FileUtil.accessSync(this.filePath)) {
  ScanUtil.decode(this.filePath).then((scanResult) => {
    let scanStr3 = JSON.stringify(scanResult, null, 2);
  })
} else {
  ToastUtil.showToast("请先点击generateBarcode生成二维码图片");
}
```

##### decodeImage calls image data identification capability and uses Promise asynchronous callback to return code identification results

```
//优先获取图像的YuvByteBuffer, YuvHeight, YuvWidth数据，比如获取宽高是1920*1080时
let byteImg: detectBarcode.ByteImage = {
  byteBuffer: YuvByteBuffer,
  width: 1920,
  height: 1080,
  format: detectBarcode.ImageFormat.NV21
};
ScanUtil.decodeImage(byteImg).then((scanResult) => {
  let scanStr3 = JSON.stringify(scanResult, null, 2);
});
```

##### onPickerScanForResult Pull up the gallery through picker and select the picture, and call the picture identification code

```
ScanUtil.onPickerScanForResult().then((scanResult) => {
  let scanStr2 = JSON.stringify(scanResult, null, 2);
  Utils.showSheetText(scanStr2);
}).catch((err: BusinessError) => {
  ToastUtil.showToast("扫码异常！");
});
```

##### canIUseScan judgement

```
let canIUseScan = ScanUtil.canIUseScan();
ToastUtil.showToast(`当前设备是否支持码能力：${canIUseScan}`);
```

## Creation is not easy, please give Elder Tong a thumbs up 👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   



