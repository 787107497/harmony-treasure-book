# PickerUtil, taking photos, selecting and saving files, tool classes

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

##### camera calls the system camera, take photos and record videos

```
PickerUtil.cameraEasy().then((uri) => {
  let uriStr = `调用相机，返回uri：\n${uri}`;
}).catch((err: BusinessError) => {
  let str = `调用相机，异常：\n${JSON.stringify(err)}`;
});
```

##### cameraEasy Call the system camera, take photos and record videos

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

##### selectPhoto Pull up the photoPicker interface by selecting mode, users can select one or more pictures/videos

```
PickerUtil.selectPhoto().then((uris) => {
  let uriStr = `调用相册，返回uris：\n${uris.join('\n')}`;
}).catch((err: BusinessError) => {
  let str = `调用相册，异常：\n${JSON.stringify(err)}`;
});
```

##### savePhoto pull up photoPicker to save the file name of the picture or video resource through the save mode. If there are no parameters, the user needs to enter it by default.

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

##### selectDocument Pull up the documentPicker interface by selecting mode, users can select one or more files

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

##### saveDocument Pull up the documentPicker interface through the save mode, and the user can save one or more files.

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

##### selectAudio Pull up the audioPicker interface by selecting mode, users can select one or more audio files

```
PickerUtil.selectAudio().then((uris) => {
  let uriStr = `调用文件管理，返回uris：\n${uris.join('\n')}`;
}).catch((err: BusinessError) => {
  let uriStr = `调用文件管理，异常：\n${JSON.stringify(err)}`;
});
```

##### saveAudio Pull up the audioPicker interface through save mode, and users can save one or more audio files.

```
let fileName = `AudioViewPicker001.mp3`;
PickerUtil.saveAudio([fileName]).then((uris) => {
  let uri = uris[0];
  let uriStr = `音频文件，返回uris：\n${uri}`;
}).catch((err: BusinessError) => {
  let uriStr = `调用保存文件，异常：\n${JSON.stringify(err)}`;
})
```

## Creation is not easy, please give Elder Tong a thumbs up 👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   



