# harmony-utils之PhotoHelper，相册相关工具类

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

##### select 通过选择模式拉起photoPicker界面，用户可以选择一个或多个图片/视频

```
//相册选择图片
PhotoHelper.select().then((result) => {
  let uris = result.photoUris;
  let uriStr = `调用相册，返回uris：\n${uris.join('\n')}`;
}).catch((err: BusinessError) => {
  let str = `调用相册，异常：\n${JSON.stringify(err)}`;
});
```

##### selectEasy  通过选择模式拉起photoPicker界面，用户可以选择一个或多个图片/视频

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

##### save  申请权限保存，保存图片或视频到相册

```
//图片保存进相册（已申请权限使用该方法）
let ps: Permissions[] = ['ohos.permission.WRITE_IMAGEVIDEO'];
PermissionUtil.requestPermissions(ps).then((result) => {
  if (result) {
    let imgName = `测试图片_${DateUtil.getTodayTime()}`;
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

##### showAssetsCreationDialog  弹窗授权保存，调用接口拉起保存确认弹窗

```
let pixelMap = await ImageUtil.getPixelMapFromMedia($r("app.media.test_as4"));
let filePath = await ImageUtil.savePixelMap(pixelMap, FileUtil.getFilesDirPath(""), "测试图片.png");
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

##### showAssetsCreationDialogEasy  弹窗授权保存，调用接口拉起保存确认弹窗，并保存

```
let pixelMap = await ImageUtil.getPixelMapFromMedia($r("app.media.test_as4"));
let filePath = await ImageUtil.savePixelMap(pixelMap, FileUtil.getFilesDirPath(""), "测试图片.png");
let uri = FileUtil.getUriFromPath(this.filePath);

PhotoHelper.showAssetsCreationDialogEasy([uri, uri2]).then((result) => {
  let uriStr = `图片保存成功，返回uris：\n${JSON.stringify(result, null, 2)}`;
  DialogHelper.showToast("图片保存成功！");
}).catch((error: BusinessError) => {
  DialogHelper.showToast("图片保存失败！");
});
```

##### applyChanges  安全控件保存，提交媒体变更请求，插入图片/视频

```
//安全控件保存，图片保存进相册。
let pixelMap = await ImageUtil.getPixelMapFromMedia($r("app.media.test_as4"));
let filePath = await ImageUtil.savePixelMap(pixelMap, FileUtil.getFilesDirPath(""), "测试图片.png");

let uri = FileUtil.getUriFromPath(this.filePath);
PhotoHelper.applyChanges(uri).then((result) => {
  let uriStr = `保存图片成功：${result.uri}`;
}).catch((err: BusinessError) => {
  let str = `保存图片失败：${JSON.stringify(err)}`;
});
```

##### getPhotoAsset  获取对应uri的PhotoAsset对象,用于读取文件信息

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

## 创作不易，请给童长老点赞👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   

