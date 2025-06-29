# harmony-utils之PreviewUtil，文件预览工具类

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

##### generatePreviewInfo  根据文件uri构建PreviewInfo

```
 let docPath = FileUtil.getFilesDirPath("download/wps/doc', "测试DOC文件.doc");
 FileUtil.writeEasy(docPath, "harmony-utils 一款高效的OpenHarmony/HarmonyOS工具包。帮助开发者快速构建鸿蒙应用。");
 let uri = FileUtil.getUriFromPath(docPath);
 let info = PreviewUtil.generatePreviewInfo(uri);
 let infoStr = JSON.stringify(info, null, 2);
 LogUtil.error(infoStr);
```

##### openPreview  通过传入文件预览信息，打开预览窗口。1秒内重复调用无效

```
 let docPath = FileUtil.getFilesDirPath("download/wps/doc', "测试DOC文件.doc");
 let uri = FileUtil.getUriFromPath(docPath);
 let info = PreviewUtil.generatePreviewInfo(uri);
 PreviewUtil.openPreview(info).catch((error: BusinessError) => {
  LogUtil.error(`onSharePreview-异常 ~ code: ${error.code} -·- message: ${error.message}`);
 });
```

##### openPreviewEasy  通过传入文件的uri，打开预览窗口。1秒内重复调用无效

```
 let docPath = FileUtil.getFilesDirPath("download/wps/doc', "测试DOC文件.doc");
 let uri = FileUtil.getUriFromPath(docPath);
 PreviewUtil.openPreviewEasy(uri);
```

##### canPreview  根据文件的uri判断文件是否可预览

```
 let docPath = FileUtil.getFilesDirPath("download/wps/doc', "测试DOC文件.doc");
 let uri = FileUtil.getUriFromPath(docPath);
 let canPreview = await PreviewUtil.canPreview(uri);
 ToastUtil.showToast(`canPreview: ${canPreview}`);
```

##### hasDisplayed   判断预览窗口是否已经存在

```
 let hasDisplayed = await PreviewUtil.hasDisplayed();
 ToastUtil.showToast(`hasDisplayed: ${hasDisplayed}`);
```

##### closePreview   关闭预览窗口，仅当预览窗口存在时起效

```
PreviewUtil.closePreview().then(() => {
  ToastUtil.showToast("已关闭预览");
});
```

##### loadData  加载预览文件信息。仅当预览窗口存在时起效

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

##### loadDataEasy  加载预览文件信息。仅当预览窗口存在时起效

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

##### onSharePreview  调用其他应用预览文件

```
let docPath = FileUtil.getFilesDirPath("download/wps/doc', "测试DOC文件.doc");
let uri = FileUtil.getUriFromPath(docPath);
PreviewUtil.onSharePreview(uri).catch((error: BusinessError) => {
  ToastUtil.showToast("打开文件失败，" + error.message);
  LogUtil.error(`onSharePreview-异常 ~ code: ${error.code} -·- message: ${error.message}`);
});
```

##### getTypeDescriptor  根据文件后缀名获取TypeDescriptor（标准化数据类型的描述类）

```
let typeDescriptor = PreviewUtil.getTypeDescriptor("png");
ToastUtil.showToast(`${typeDescriptor.mimeTypes}`);
```

##### getMimeType  根据文件后缀名获取文件mimeType

```
let mimeType = PreviewUtil.getMimeType("png");
let mimeType2 = PreviewUtil.getMimeType("txt");
ToastUtil.showToast(`${mimeType} --- ${mimeType2}`);
```

##### getIconFileStr  根据文件后缀名获取对应文件类型的图标

```
let iconFileStr = PreviewUtil.getIconFileStr("doc");
let iconRes: Resource = $r(iconFileStr);
```

##### canIUsePreview  判断当前设备是否支持文件预览能力

```
 let bl = PreviewUtil.canIUsePreview();
 ToastUtil.showToast(`当前设备是否支持文件预览能力:${bl}`);
```

## 创作不易，请给童长老点赞👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   


