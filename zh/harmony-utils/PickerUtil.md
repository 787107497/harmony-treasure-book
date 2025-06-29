# harmony-utils之PickerUtil，拍照、文件选择和保存,工具类

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

##### camera  调用系统相机，拍照、录视频

```
PickerUtil.cameraEasy().then((uri) => {
  let uriStr = `调用相机，返回uri：\n${uri}`;
}).catch((err: BusinessError) => {
  let str = `调用相机，异常：\n${JSON.stringify(err)}`;
});
```

##### cameraEasy  调用系统相机，拍照、录视频

```
let options: CameraOptions = {
  mediaTypes: [cameraPicker.PickerMediaType.PHOTO],
  cameraPosition: camera.CameraPosition.CAMERA_POSITION_BACK
}
PickerUtil.camera(options).then((result) => {
  let uriStr = `调用相机，返回uri：\n${result.resultUri}`;
}).catch((err: BusinessError) => {
  let str = `调用相机，异常：\n${JSON.stringify(err)}`;
});
```

##### selectPhoto  通过选择模式拉起photoPicker界面，用户可以选择一个或多个图片/视频

```
PickerUtil.selectPhoto().then((uris) => {
  let uriStr = `调用相册，返回uris：\n${uris.join('\n')}`;
}).catch((err: BusinessError) => {
  let str = `调用相册，异常：\n${JSON.stringify(err)}`;
});
```

##### savePhoto  通过保存模式拉起photoPicker进行保存图片或视频资源的文件名，若无参数，则默认需要用户自行输入

```
let imgName = `大漂亮_${DateUtil.getTodayTime()}.png`;
let imgName1 = `小漂亮_${DateUtil.getTodayTime()}.png`;
PickerUtil.savePhoto([imgName, imgName1]).then(async (uris) => {
  let uri = uris[0];
  let uriStr = `调用保存图片，返回uris：\n${uri}`;
  let file = FileUtil.openSync(uri);
  FileUtil.copyFile(this.filePath, file.fd).then(() => {
    let uriStr = `保存图片，返回uris：\n${uri}`;
    ToastUtil.showToast("图片1保存成功");
  });

  let file1 = FileUtil.openSync(uris[1]);
  let pixelMap1 = await ImageUtil.getPixelMapFromMedia($r("app.media.test_as3"));
  let packOpts: image.PackingOption = { format: 'image/png', quality: 100 };
  ImageUtil.packToFileFromPixelMap(pixelMap1, file1.fd, packOpts).then(() => {
    let uriStr = `保存图片，返回uris：\n${uris[1]}`;
    ToastUtil.showToast("图片2保存成功");
  });
}).catch((err: BusinessError) => {
  let uriStr = `调用保存图片，异常：\n${JSON.stringify(err)}`;
})
```

##### selectDocument  通过选择模式拉起documentPicker界面，用户可以选择一个或多个文件

```
let options: picker.DocumentSelectOptions = {
  maxSelectNumber: 9, //选择媒体文件数量的最大值,默认9。
  selectMode: picker.DocumentSelectMode.FILE, //支持选择的资源类型,默认文件
  // fileSuffixFilters: ['图片(.png, .jpg)|.png,.jpg', '文档|.txt', '视频|.mp4', '.pdf'], //选择文件的后缀类型['后缀类型描述|后缀类型']（可选） 若选择项存在多个后缀名，则每一个后缀名之间用英文逗号进行分隔（可选），后缀类型名不能超过100,选择所有文件：'所有文件(*.*)|.*';
  // defaultFilePathUri: "file://docs/storage/Users/currentUser/Download/com.harmony.utils", //指定选择的文件或者目录路径（可选）
  // authMode: true //选择是否对指定文件或目录授权，true为授权，当为true时，defaultFilePathUri为必选参数。
}
PickerUtil.selectDocument(options).then((uris) => {
  let uriStr = `调用文件管理，返回uris：\n${uris.join('\n')}`
}).catch((err: BusinessError) => {
  let uriStr = `调用文件管理，异常：\n${JSON.stringify(err)}`
});
```

##### saveDocument  通过保存模式拉起documentPicker界面，用户可以保存一个或多个文件

```
let fileName = `test_easy_${DateUtil.getTodayTime()}.txt`;
PickerUtil.saveDocumentEasy([fileName]).then((paths) => {
  let path = paths[0];
  this.cacheUri = FileUtil.getUriFromPath(path);
  PreferencesUtil.put("picker_cache_uri", this.cacheUri);
  let txtStr = `“harmony-utils 一款高效的OpenHarmony/HarmonyOS工具包，封装了常用工具类，提供一系列简单易用的方法。帮助开发者快速构建鸿蒙应用。\n\n`;
  FileUtil.writeEasy(path, txtStr).then(() => {
    let uriStr = `文件保存成功，返回uris：\n${path}`;
    ToastUtil.showToast("文件保存成功！");
  }).catch((err: BusinessError) => {
    let uriStr = `文件保存，异常：\n${JSON.stringify(err)}`;
  })
}).catch((err: BusinessError) => {
  let uriStr = `调用保存文件，异常：\n${JSON.stringify(err)}`;
})
```

##### selectAudio  通过选择模式拉起audioPicker界面，用户可以选择一个或多个音频文件

```
PickerUtil.selectAudio().then((uris) => {
  let uriStr = `调用文件管理，返回uris：\n${uris.join('\n')}`;
}).catch((err: BusinessError) => {
  let uriStr = `调用文件管理，异常：\n${JSON.stringify(err)}`;
});
```

##### saveAudio  通过保存模式拉起audioPicker界面，用户可以保存一个或多个音频文件

```
let fileName = `AudioViewPicker001.mp3`;
PickerUtil.saveAudio([fileName]).then((uris) => {
  let uri = uris[0];
  let uriStr = `音频文件，返回uris：\n${uri}`;
}).catch((err: BusinessError) => {
  let uriStr = `调用保存文件，异常：\n${JSON.stringify(err)}`;
})
```

## 创作不易，请给童长老点赞👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   



