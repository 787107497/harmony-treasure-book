# PasteboardUtil, Clipboard Tools

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

##### requestPermissions request clipboard permissions

```
PasteboardUtil.requestPermissions().then((result) => {
  ToastUtil.showToast(`检测并申请授权，允许应用读取剪贴板：${result}`);
});
```

##### getSystemPasteboard Gets the system clipboard object

```
 let systemPasteboard = PasteboardUtil.getSystemPasteboard();
```

##### hasData determines whether there is any content in the system clipboard

```
let hasData = PasteboardUtil.hasDataSync();
ToastUtil.showToast(`系统剪贴板中是否有内容：${hasData}`);
```

##### setData Writes data to the system clipboard

```
let text = "一款高效的OpenHarmony/HarmonyOS工具包。"
PasteboardUtil.setDataSync(pasteboard.MIMETYPE_TEXT_PLAIN, text);
```

##### getData Reads the contents of the system clipboard

```
let text = PasteboardUtil.getDataSync().getPrimaryText();
ToastUtil.showToast(`剪切板内容为：${text}`);
```

##### setDataText Write plain text data to the system clipboard

```
let text = "harmony-utils 一款高效的OpenHarmony/HarmonyOS工具包，封装了常用工具类，提供一系列简单易用的方法。"
PasteboardUtil.setDataText(text).then(() => {
  ToastUtil.showToast("设置成功！");
})
```

##### getDataText Read plain text content of the system clipboard

```
let str = await PasteboardUtil.getDataText();
ToastUtil.showToast(`剪切板内容为：${str}`);
```

##### setDataHtml Write HTML data to the system clipboard

```
let html = "<!DOCTYPE html>\n" + "<html>\n" + "<head>\n" + "<meta charset=\"utf-8\">\n" +
  "<title>HTML-PASTEBOARD_HTML</title>\n" + "</head>\n" + "<body>\n" + "<h1>HEAD</h1>\n" +
  "<p>一个富文本</p>\n" + "</body>\n" + "</html>";
PasteboardUtil.setDataHtml(html).then(() => {
  ToastUtil.showToast("设置成功");
})
```

##### getDataHtml Read the HTML content of the system clipboard

```
 let html = await PasteboardUtil.getDataHtml();
 ToastUtil.showToast(`剪切板内容为：${html}`);
```

##### setDataUri Write URI data to the system clipboard

```
let dataUri = 'dataability:///com.example.myapplication1/user.txt';
PasteboardUtil.setDataUri(dataUri).then(() => {
  ToastUtil.showToast("设置成功");
})
```

##### getDataUri Reads the URI content of the system clipboard URI

```
let uri = PasteboardUtil.getDataUriSync();
ToastUtil.showToast(`剪切板内容为：${uri}`);
```

##### setDataWant Write Want data to the system clipboard

```
let want: Want = {
  deviceId: 'device_666666',
  bundleName: 'com.example.myapplication',
  abilityName: 'FuncAbility',
  moduleName: 'entry'
};
PasteboardUtil.setDataWantSync(want);
```

##### getDataWant Reads the Want content of the system clipboard

```
let want = PasteboardUtil.getDataWantSync();
if (want) {
  let jsonStr = JSON.stringify(want, null, 2);
  Utils.showSheetText(jsonStr);
}else {
  ToastUtil.showToast("剪切板内容为空，请先设置内容");
}
```

##### setDataPixelMap Write PixelMap data to the system clipboard

```
let pixelMap = await ImageUtil.getPixelMapFromMedia($r("app.media.test_as4"))
PasteboardUtil.setDataPixelMap(pixelMap).then(() => {
  ToastUtil.showToast("设置成功");
});
```

##### getDataPixelMap Read the content of the system clipboard PixelMap

```
let pixelMap = PasteboardUtil.getDataPixelMapSync();
if (pixelMap) {
  Utils.showSheetImg(pixelMap);
} else {
  ToastUtil.showToast("剪切板内容为空，请先设置内容");
}
```

##### getDataStr Read strings in the system clipboard

```
let str = PasteboardUtil.getDataStrSync();
ToastUtil.showToast(`剪切板内容为：${str}`);
```

##### getDataEasy Read content in the system clipboard (plain text content, HTML content, URI content, Want content, PixelMap content)

```
let data = PasteboardUtil.getDataEasy();
if (data && typeof data === 'string') {
  Utils.showSheetText(data);
} else if (data && typeof data === 'object') {
  if (typeof (data as PixelMap).getImageInfo === 'function') {
    Utils.showSheetImg(data as PixelMap);
  } else {
    Utils.showSheetText(JSON.stringify(data, null, 2));
  }
} else {
  ToastUtil.showToast("剪切板内容为空，请先设置内容");
}
```

##### clearData Clear system clipboard content

```
PasteboardUtil.clearDataSync();
ToastUtil.showToast(`清空成功！`);
```

## Creation is not easy, please give Elder Tong a thumbs up 👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   

