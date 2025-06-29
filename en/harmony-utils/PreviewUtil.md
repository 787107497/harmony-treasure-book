# PreviewUtil, file preview tool class

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

##### generatePreviewInfo build PreviewInfo based on file uri

```
 let docPath = FileUtil.getFilesDirPath("download/wps/doc', "测试DOC文件.doc");
 FileUtil.writeEasy(docPath, "harmony-utils 一款高效的OpenHarmony/HarmonyOS工具包。帮助开发者快速构建鸿蒙应用。");
 let uri = FileUtil.getUriFromPath(docPath);
 let info = PreviewUtil.generatePreviewInfo(uri);
 let infoStr = JSON.stringify(info, null, 2);
 LogUtil.error(infoStr);
```

##### openPreview opens the preview window by passing in file preview information. Repeated calls within 1 second are invalid

```
 let docPath = FileUtil.getFilesDirPath("download/wps/doc', "测试DOC文件.doc");
 let uri = FileUtil.getUriFromPath(docPath);
 let info = PreviewUtil.generatePreviewInfo(uri);
 PreviewUtil.openPreview(info).catch((error: BusinessError) => {
  LogUtil.error(`onSharePreview-异常 ~ code: ${error.code} -·- message: ${error.message}`);
 });
```

##### openPreviewEasy opens the preview window through the uri of the file. Repeated calls within 1 second are invalid

```
 let docPath = FileUtil.getFilesDirPath("download/wps/doc', "测试DOC文件.doc");
 let uri = FileUtil.getUriFromPath(docPath);
 PreviewUtil.openPreviewEasy(uri);
```

##### canPreview determines whether the file can be previewed based on the uri of the file

```
 let docPath = FileUtil.getFilesDirPath("download/wps/doc', "测试DOC文件.doc");
 let uri = FileUtil.getUriFromPath(docPath);
 let canPreview = await PreviewUtil.canPreview(uri);
 ToastUtil.showToast(`canPreview: ${canPreview}`);
```

##### hasDisplayed determines whether the preview window already exists

```
 let hasDisplayed = await PreviewUtil.hasDisplayed();
 ToastUtil.showToast(`hasDisplayed: ${hasDisplayed}`);
```

##### closePreview Closes the preview window, only effective if the preview window exists

```
PreviewUtil.closePreview().then(() => {
  ToastUtil.showToast("已关闭预览");
});
```

##### loadData Loads preview file information. Only effective if the preview window exists

```
let docPath = FileUtil.getFilesDirPath("download/wps/doc', "测试DOC文件.doc");
let uri = FileUtil.getUriFromPath(docPath);
let info = PreviewUtil.generatePreviewInfo(uri);
let hasDisplayed = await PreviewUtil.hasDisplayed();
if (hasDisplayed) {
  PreviewUtil.loadData(info);
} else {
  PreviewUtil.openPreview(info);
}
```

##### loadDataEasy Loads preview file information. Only effective if the preview window exists

```
let docPath = FileUtil.getFilesDirPath("download/wps/doc', "测试DOC文件.doc");
let uri = FileUtil.getUriFromPath(docPath);
let hasDisplayed = await PreviewUtil.hasDisplayed();
if (hasDisplayed) {
  PreviewUtil.loadDataEasy(uri);
} else {
  PreviewUtil.openPreviewEasy(uri);
}
```

##### onSharePreview Calls other application preview files

```
let docPath = FileUtil.getFilesDirPath("download/wps/doc', "测试DOC文件.doc");
let uri = FileUtil.getUriFromPath(docPath);
PreviewUtil.onSharePreview(uri).catch((error: BusinessError) => {
  ToastUtil.showToast("打开文件失败，" + error.message);
  LogUtil.error(`onSharePreview-异常 ~ code: ${error.code} -·- message: ${error.message}`);
});
```

##### getTypeDescriptor Get TypeDescriptor (a description class for standardized data type)

```
let typeDescriptor = PreviewUtil.getTypeDescriptor("png");
ToastUtil.showToast(`${typeDescriptor.mimeTypes}`);
```

##### getMimeType Get file mimeType according to file suffix name

```
let mimeType = PreviewUtil.getMimeType("png");
let mimeType2 = PreviewUtil.getMimeType("txt");
ToastUtil.showToast(`${mimeType} --- ${mimeType2}`);
```

##### getIconFileStr Get the icon of the corresponding file type according to the file suffix name

```
let iconFileStr = PreviewUtil.getIconFileStr("doc");
let iconRes: Resource = $r(iconFileStr);
```

##### canIUsePreview determines whether the current device supports file preview capabilities

```
 let bl = PreviewUtil.canIUsePreview();
 ToastUtil.showToast(`当前设备是否支持文件预览能力:${bl}`);
```

## Creation is not easy, please give Elder Tong a thumbs up 👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   


