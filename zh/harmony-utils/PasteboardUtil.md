# harmony-utils之PasteboardUtil，剪贴板工具类

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

##### requestPermissions  申请剪贴板权限

```
PasteboardUtil.requestPermissions().then((result) => {
  ToastUtil.showToast(`检测并申请授权，允许应用读取剪贴板：${result}`);
});
```

##### getSystemPasteboard  获取系统剪贴板对象

```
 let systemPasteboard = PasteboardUtil.getSystemPasteboard();
```

##### hasData  判断系统剪贴板中是否有内容

```
let hasData = PasteboardUtil.hasDataSync();
ToastUtil.showToast(`系统剪贴板中是否有内容：${hasData}`);
```

##### setData  将数据写入系统剪贴板

```
let text = "一款高效的OpenHarmony/HarmonyOS工具包。"
PasteboardUtil.setDataSync(pasteboard.MIMETYPE_TEXT_PLAIN, text);
```

##### getData  读取系统剪贴板内容

```
let text = PasteboardUtil.getDataSync().getPrimaryText();
ToastUtil.showToast(`剪切板内容为：${text}`);
```

##### setDataText  将纯文本数据写入系统剪贴板

```
let text = "harmony-utils 一款高效的OpenHarmony/HarmonyOS工具包，封装了常用工具类，提供一系列简单易用的方法。"
PasteboardUtil.setDataText(text).then(() => {
  ToastUtil.showToast("设置成功！");
})
```

##### getDataText  读取系统剪贴板纯文本内容

```
let str = await PasteboardUtil.getDataText();
ToastUtil.showToast(`剪切板内容为：${str}`);
```

##### setDataHtml  将HTML数据写入系统剪贴板

```
let html = "<!DOCTYPE html>\n" + "<html>\n" + "<head>\n" + "<meta charset=\"utf-8\">\n" +
  "<title>HTML-PASTEBOARD_HTML</title>\n" + "</head>\n" + "<body>\n" + "<h1>HEAD</h1>\n" +
  "<p>一个富文本</p>\n" + "</body>\n" + "</html>";
PasteboardUtil.setDataHtml(html).then(() => {
  ToastUtil.showToast("设置成功");
})
```

##### getDataHtml  读取系统剪贴板HTML内容

```
 let html = await PasteboardUtil.getDataHtml();
 ToastUtil.showToast(`剪切板内容为：${html}`);
```

##### setDataUri  将URI数据写入系统剪贴板

```
let dataUri = 'dataability:///com.example.myapplication1/user.txt';
PasteboardUtil.setDataUri(dataUri).then(() => {
  ToastUtil.showToast("设置成功");
})
```

##### getDataUri  读取系统剪贴板URI内容

```
let uri = PasteboardUtil.getDataUriSync();
ToastUtil.showToast(`剪切板内容为：${uri}`);
```

##### setDataWant  将Want数据写入系统剪贴板

```
let want: Want = {
  deviceId: 'device_666666',
  bundleName: 'com.example.myapplication',
  abilityName: 'FuncAbility',
  moduleName: 'entry'
};
PasteboardUtil.setDataWantSync(want);
```

##### getDataWant  读取系统剪贴板Want内容

```
let want = PasteboardUtil.getDataWantSync();
if (want) {
  let jsonStr = JSON.stringify(want, null, 2);
  Utils.showSheetText(jsonStr);
}else {
  ToastUtil.showToast("剪切板内容为空，请先设置内容");
}
```

##### setDataPixelMap  将PixelMap数据写入系统剪贴板

```
let pixelMap = await ImageUtil.getPixelMapFromMedia($r("app.media.test_as4"))
PasteboardUtil.setDataPixelMap(pixelMap).then(() => {
  ToastUtil.showToast("设置成功");
});
```

##### getDataPixelMap  读取系统剪贴板PixelMap内容

```
let pixelMap = PasteboardUtil.getDataPixelMapSync();
if (pixelMap) {
  Utils.showSheetImg(pixelMap);
} else {
  ToastUtil.showToast("剪切板内容为空，请先设置内容");
}
```

##### getDataStr  读取系统剪贴板里的字符串

```
let str = PasteboardUtil.getDataStrSync();
ToastUtil.showToast(`剪切板内容为：${str}`);
```

##### getDataEasy  读取系统剪贴板里的内容（纯文本内容、HTML内容、URI内容、Want内容、PixelMap内容）

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

##### clearData  清空系统剪贴板内容

```
PasteboardUtil.clearDataSync();
ToastUtil.showToast(`清空成功！`);
```

## 创作不易，请给童长老点赞👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   

