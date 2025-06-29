# harmony-utils之ImageUtil，图片相关工具类

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

##### base64ToPixelMap  图片base64字符串转PixelMap

```
 let base64str = "data:image/png;base64,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";
 let pixelMap = await ImageUtil.base64ToPixelMap(base64str);
```

##### pixelMapToBase64Str  PixelMap转图片base64字符串

```
  let pixelMap = await ImageUtil.getPixelMapFromMedia($r("app.media.test_as3"));
  let base64Str = await ImageUtil.pixelMapToBase64Str(pixelMap);
```

##### savePixelMap   保存pixelMap到本地

```
let pixelMap = await ImageUtil.getPixelMapFromMedia($r("app.media.test_as4"));
let filePath = await ImageUtil.savePixelMap(pixelMap, FileUtil.getFilesDirPath(""), "测试图片.png");
```

##### saveImageSource   保存ImageSource到本地

```
let filePath = "这里是图片地址"
let imageSource = await ImageUtil.createImageSource(filePath);
ImageUtil.saveImageSource(imageSource, FileUtil.getFilesDirPath(""), `MZ_${DateUtil.getTodayStr()}.png`)
  .then(() => {
    ToastUtil.showToast("保存成功");
  });
```

##### createImageSource  创建图片源实例

```
let filePath = "这里是图片地址"
let imageSource = await ImageUtil.createImageSource(filePath);
let pixelMap = await imageSource.createPixelMap();
```

##### packingFromPixelMap  图片压缩或重新打包

```
let filePath = "这里是图片地址"
let pixelMap = await ImageUtil.createImageSource(filePath).createPixelMap()
let packOpts: image.PackingOption = { format: "image/png", quality: 98 }
ImageUtil.packingFromPixelMap(pixelMap, packOpts).then((buff) => {
  LogUtil.error("buff: " + buff.byteLength);
  ToastUtil.showToast("打包成功了");
});
```

##### packingFromImageSource   图片压缩或重新打包

```
let filePath = "这里是图片地址"
let imageSource = await ImageUtil.createImageSource(filePath);
let packOpts: image.PackingOption = { format: "image/png", quality: 98 }
ImageUtil.packingFromImageSource(imageSource, packOpts).then((buff) => {
  LogUtil.error("buff: " + buff.byteLength);
  ToastUtil.showToast("打包成功了");
});
```

##### packToFileFromPixelMap   将PixelMap图片源编码后直接打包进文件

```
let filePath = "这里是图片地址"
let pixelMap = await ImageUtil.createImageSource(this.filePath).createPixelMap();
let filePath = FileUtil.getFilesDirPath("", `MeiZi_${DateUtil.getTodayTime()}.png`);
let file = FileUtil.openSync(filePath);
let packOpts: image.PackingOption = { format: "image/png", quality: 100 }
ImageUtil.packToFileFromPixelMap(pixelMap, file.fd, packOpts).then(() => {
  FileUtil.closeSync(file.fd); //关闭文件
  ToastUtil.showToast("图片保存成功");
});
```

##### packToFileFromImageSource  将ImageSource图片源编码后直接打包进文件

```
let filePath = "这里是图片地址"
let imageSource = await ImageUtil.createImageSource(filePath);
let filePath = FileUtil.getFilesDirPath("", `MeiZi_${DateUtil.getTodayTime()}.png`);
let file = FileUtil.openSync(filePath);
let packOpts: image.PackingOption = { format: "image/png", quality: 100 }
ImageUtil.packToFileFromImageSource(imageSource, file.fd, packOpts).then(() => {
  FileUtil.closeSync(file.fd); //关闭文件
  ToastUtil.showToast("图片保存成功");
});
```

##### getPixelMapFromMedia   用户获取resource目录下的media中的图片PixelMap

```
let pixelMap = await ImageUtil.getPixelMapFromMedia($r("app.media.test_as4"));
```

##### compressedImage  图片压缩

```
let pixelMap = await ImageUtil.getPixelMapFromMedia($r("app.media.test_as5")); //原大小3.78M
let arrayBuffer = await ImageUtil.compressedImage(pixelMap, 150);
LogUtil.error("压缩后的大小：" + arrayBuffer.byteLength);
PickerUtil.savePhoto(['压缩后的图片.jpeg']).then(async (uris)=>{
  let uri = uris[0];
  await FileUtil.writeEasy(uri,arrayBuffer,false);
  ToastUtil.showToast("压缩文件保存成功");
});
```

##### compressPhoto  图片压缩，返回压缩后的图片文件路径

```
PhotoHelper.select({ maxSelectNumber: 1 }).then(async (uris) => {
  if (uris?.length > 0) {
    let uri = uris[0];
    let filePath = await ImageUtil.compressPhoto(uri, 100).catch((err: BusinessError) => {
      LogUtil.error("图片压缩异常：" + err.message);
      return "";
    }); //压缩返回路径
    let oldSize = FileUtil.statSync(FileUtil.openSync(uri, fs.OpenMode.READ_ONLY).fd).size; //压缩前大小
    let compressSize = FileUtil.statSync(filePath).size; //压缩后大小
    this.resultStr = `压缩路径: ${filePath}\n\n压缩前大小: ${FileUtil.getFormatFileSize(oldSize)}\n压缩后大小: ${FileUtil.getFormatFileSize(compressSize)}`;
    LogUtil.error(this.resultStr);
  }
}).catch((err: BusinessError) => {
  LogUtil.error("异常信息：" + err.message);
});
```

## 创作不易，请给童长老点赞👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   





