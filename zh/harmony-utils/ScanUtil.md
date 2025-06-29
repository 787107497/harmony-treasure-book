# harmony-utils之ScanUtil，码工具类(扫码、码图生成、图片识码)

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

##### startScanForResult  调用默认界面扫码，使用Promise方式异步返回解码结果

```
ScanUtil.startScanForResult().then((scanResult) => {
  let scanStr1 = JSON.stringify(scanResult, null, 2);
});
```

##### generateBarcode  码图生成，使用Promise异步返回生成的码图

```
let txtStr = "harmony-utils 一款高效的OpenHarmony/HarmonyOS工具包，封装了常用工具类，提供一系列简单易用的方法";
let pixelMap = await ScanUtil.generateBarcode(txtStr);
ImageUtil.savePixelMap(pixelMap, FileUtil.getFilesDirPath(""), "qr_code.png");
```

##### decode  调用图片识码，使用Promise方式异步返回识码结果

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

##### decodeImage  调用图像数据识码能力，使用Promise异步回调返回识码结果

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

##### onPickerScanForResult  通过picker拉起图库并选择图片,并调用图片识码

```
ScanUtil.onPickerScanForResult().then((scanResult) => {
  let scanStr2 = JSON.stringify(scanResult, null, 2);
  Utils.showSheetText(scanStr2);
}).catch((err: BusinessError) => {
  ToastUtil.showToast("扫码异常！");
});
```

##### canIUseScan  判断

```
let canIUseScan = ScanUtil.canIUseScan();
ToastUtil.showToast(`当前设备是否支持码能力：${canIUseScan}`);
```

## 创作不易，请给童长老点赞👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   



