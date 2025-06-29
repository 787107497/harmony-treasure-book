# harmony-utils PhotoHelper, photo album related tool category

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

##### select by selecting the photoPicker interface, the user can select one or more pictures/videos

```
//相册选择图片
PhotoHelper.select().then((result) => {
  let uris = result.photoUris;
  let uriStr = `调用相册，返回uris：\n${uris.join('\n')}`;
}).catch((err: BusinessError) => {
  let str = `调用相册，异常：\n${JSON.stringify(err)}`;
});
```

##### selectEasy pulls up the photoPicker interface by selecting mode, and users can select one or more pictures/videos

```
//相册选择图片/视频（多选）
let options: photoAccessHelper.PhotoSelectOptions = {
  MIMEType: photoAccessHelper.PhotoViewMIMETypes.IMAGE_VIDEO_TYPE,
  maxSelectNumber: 12,
  isPhotoTakingSupported: false,
  isSearchSupported: false,
  isEditSupported: false,
  isOriginalSupported: true
}
PhotoHelper.selectEasy(options).then((uris) => {
  let uriStr = `调用相册，返回uris：\n${uris.join('\n')}`;
}).catch((err: BusinessError) => {
  let str = `调用相册，异常：\n${JSON.stringify(err)}`;
});
 
//相册选择图片（单选）
let options: photoAccessHelper.PhotoSelectOptions = {
  MIMEType: photoAccessHelper.PhotoViewMIMETypes.IMAGE_TYPE,
  maxSelectNumber: 1,
  isOriginalSupported: true,
  isPreviewForSingleSelectionSupported: true //单选模式下是否需要进大图预览
}
PhotoHelper.selectEasy(options).then((uris) => {
  let uriStr = `调用相册，返回uris：\n${uris.join('\n')}`;
}).catch((err: BusinessError) => {
  let str = `调用相册，异常：\n${JSON.stringify(err)}`;
});
```

##### save Apply for permission to save, save pictures or videos to albums

```
//图片保存进相册（已申请权限使用该方法）
let ps: Permissions[] = ['ohos.permission.WRITE_IMAGEVIDEO'];
PermissionUtil.requestPermissions(ps).then((result) => {
  if (result) {
    let imgName = `漂亮小姐姐_${DateUtil.getTodayTime()}`;
    PhotoHelper.save(photoAccessHelper.PhotoType.IMAGE, 'jpg', { title: imgName }).then(async (uri) => {
      if (uri) {
        let uriStr = `保存图片成功，返回uris：\n${uri}`;
        let file = FileUtil.openSync(uri);
        FileUtil.copyFile(this.filePath, file.fd).then(() => {
          FileUtil.close(file.fd);
          ToastUtil.showToast("图片保存成功");
        })
      }
    }).catch((err: BusinessError) => {
      let str = `调用保存图片，异常：\n${JSON.stringify(err)}`;
    })
  } else {
    ToastUtil.showLong("请在设置中打开权限");
    WantUtil.toAppSetting();
  }
});
```

##### showAssetsCreationDialog pop-up window authorization save, call the interface to pull up the save confirmation pop-up window

```
let pixelMap = await ImageUtil.getPixelMapFromMedia($r("app.media.test_as4"));
let filePath = await ImageUtil.savePixelMap(pixelMap, FileUtil.getFilesDirPath(""), "漂亮小姐姐.png");
let uri = FileUtil.getUriFromPath(this.filePath);
let srcFileUris: Array<string>=[uri];

let desFileUris: Array<string> = await PhotoHelper.showAssetsCreationDialog(srcFileUris);
for (let index = 0; index < desFileUris.length; index++) {
  //将来源于应用沙箱的照片内容写入媒体库的目标uri
  let srcFile: fs.File = await Utils.open(srcFileUris[index], fs.OpenMode.READ_ONLY);
  let desFile: fs.File = await Utils.open(desFileUris[index], fs.OpenMode.WRITE_ONLY);
  await Utils.copyFile(srcFile.fd, desFile.fd);
  await Utils.close(srcFile);
  await Utils.close(desFile);
}
```

##### showAssetsCreationDialogEasy pop-up window authorization save, call the interface to pull up the save confirmation pop-up window, and save it

```
let pixelMap = await ImageUtil.getPixelMapFromMedia($r("app.media.test_as4"));
let filePath = await ImageUtil.savePixelMap(pixelMap, FileUtil.getFilesDirPath(""), "漂亮小姐姐.png");
let uri = FileUtil.getUriFromPath(this.filePath);

PhotoHelper.showAssetsCreationDialogEasy([uri, uri2]).then((result) => {
  let uriStr = `图片保存成功，返回uris：\n${JSON.stringify(result, null, 2)}`;
  DialogHelper.showToast("图片保存成功！");
}).catch((error: BusinessError) => {
  DialogHelper.showToast("图片保存失败！");
});
```

##### applyChanges security controls save, submit media change requests, insert pictures/videos

```
//安全控件保存，图片保存进相册。
let pixelMap = await ImageUtil.getPixelMapFromMedia($r("app.media.test_as4"));
let filePath = await ImageUtil.savePixelMap(pixelMap, FileUtil.getFilesDirPath(""), "漂亮小姐姐.png");

let uri = FileUtil.getUriFromPath(this.filePath);
PhotoHelper.applyChanges(uri).then((result) => {
  let uriStr = `保存图片成功：${result.uri}`;
}).catch((err: BusinessError) => {
  let str = `保存图片失败：${JSON.stringify(err)}`;
});
```

##### getPhotoAsset Gets the PhotoAsset object of the corresponding uri, used to read file information

```
PickerUtil.selectPhoto().then(async (uris) => {
  if (uris && uris.length > 0) {
    PhotoHelper.getPhotoAsset(uris[0]).then((photoAsset) => {
      try {
        let name = photoAsset?.get(photoAccessHelper.PhotoKeys.DISPLAY_NAME);
        let type = photoAsset?.get(photoAccessHelper.PhotoKeys.PHOTO_TYPE);
        let title = photoAsset?.get(photoAccessHelper.PhotoKeys.TITLE.toString());
        let size = photoAsset?.get(photoAccessHelper.PhotoKeys.SIZE.toString());
        let with1 = photoAsset?.get(photoAccessHelper.PhotoKeys.WIDTH.toString());
        let height = photoAsset?.get(photoAccessHelper.PhotoKeys.HEIGHT.toString());
        let date = photoAsset?.get(photoAccessHelper.PhotoKeys.DATE_TAKEN.toString());
        let orientation = photoAsset?.get(photoAccessHelper.PhotoKeys.ORIENTATION.toString());
        let uriStr = `图片信息：\n文件名：${name}\n文件类型：${type}\n文件大小：${size}\n图片宽度：${with1}\n图片高度：${height}\n拍摄日期：${date}\n文件标题：${title}\n图片文件的方向：${orientation}`
      } catch (err) {
        LogUtil.error("读取图片信息失败：" + JSON.stringify(err));
      }
      photoAsset?.getThumbnail((err, pixelMap) => {
        if (err) {
          LogUtil.error("缩略图-异常：" + JSON.stringify(err));
          return;
        }
        // this.pixelMap = pixelMap;
      })
    }).catch((err: BusinessError) => {
      let str = `读取图片异常：\n${JSON.stringify(err)}`;
    });
  } else {
    ToastUtil.showToast("请选择图片");
  }
}).catch((err: BusinessError) => {
  let str = `异常：\n${JSON.stringify(err)}`;
});
```

## Creation is not easy, please give Elder Tong a thumbs up 👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   

