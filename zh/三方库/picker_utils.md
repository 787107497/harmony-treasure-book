# picker_utils (API12+)

## 🏆简介与推荐

[picker_utils](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fpicker_utils)
是[harmony-utils](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)
拆分出来的一个子库，包含PickerUtil、PhotoHelper、ScanUtil。   
主要解决：当使用 harmony-utils 三方库且未使用picker能力时，隐私政策中无需声明相机权限与储存权限。

## 🌞下载安装

`ohpm i @pura/picker_utils`

OpenHarmony ohpm
环境配置等更多内容，请参考[如何安装 OpenHarmony ohpm 包](https://ohpm.openharmony.cn/#/cn/help/downloadandinstall)
<br>

## 📚API详解 [使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/plug/MimeTypesPage.ets)

## 📂模块介绍

| 模块          | 介绍                       |
|:------------|:-------------------------|
| PickerUtil  | 拍照、文件(文件、图片、视频)选择和保存,工具类 |
| PhotoHelper | 相册相关工具类                  |
| ScanUtil    | 码工具类（扫码、码图生成、图片识码）       |

## PickerUtil（拍照、文件选择和保存,工具类）[使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/utils/PickerUtilPage.ets)

| 方法                               | 介绍                                                  |
|:---------------------------------|:----------------------------------------------------|
| camera<br>cameraEasy             | 调用系统相机，拍照、录视频                                       |
| selectPhoto                      | 通过选择模式拉起photoPicker界面，用户可以选择一个或多个图片/视频              |
| savePhoto                        | 通过保存模式拉起photoPicker进行保存图片或视频资源的文件名，若无参数，则默认需要用户自行输入 |
| selectDocument                   | 通过选择模式拉起documentPicker界面，用户可以选择一个或多个文件              |
| saveDocument<br>saveDocumentEasy | 通过保存模式拉起documentPicker界面，用户可以保存一个或多个文件              |
| selectAudio                      | 通过选择模式拉起audioPicker界面，用户可以选择一个或多个音频文件               |
| saveAudio                        | 通过保存模式拉起audioPicker界面，用户可以保存一个或多个音频文件               |

## PhotoHelper（相册相关,工具类）[使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/utils/PhotoHelperPage.ets)

| 方法                           | 介绍                                     |
|:-----------------------------|:---------------------------------------|
| select<br>selectEasy         | 通过选择模式拉起photoPicker界面，用户可以选择一个或多个图片/视频 |
| save                         | 申请权限保存，保存图片或视频到相册。                     |
| showAssetsCreationDialog     | 弹窗授权保存，调用接口拉起保存确认弹窗。                   |
| showAssetsCreationDialogEasy | 弹窗授权保存，调用接口拉起保存确认弹窗，并保存。               |
| applyChanges                 | 安全控件保存，提交媒体变更请求，插入图片/视频。               |
| getPhotoAsset                | 获取对应uri的PhotoAsset对象,用于读取文件信息          |

## ScanUtil（码工具类(扫码、码图生成、图片识码)）[使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/utils/ScanUtilPage.ets)

| 方法                    | 介绍                             |
|:----------------------|:-------------------------------|
| startScanForResult    | 调用默认界面扫码，使用Promise方式异步返回解码结果   |
| generateBarcode       | 码图生成，使用Promise异步返回生成的码图        |
| decode                | 调用图片识码，使用Promise方式异步返回识码结果     |
| decodeImage           | 调用图像数据识码能力，使用Promise异步回调返回识码结果 |
| onPickerScanForResult | 通过picker拉起图库并选择图片,并调用图片识码      |
| canIUseScan           | 判断当前设备是否支持码能力                  |




## 示例代码

------

```
import { router } from '@kit.ArkUI';
import { DateUtil, FileUtil, ImageUtil, LogUtil, PreferencesUtil, StrUtil, ToastUtil } from '@pura/harmony-utils';
import { DescribeBean } from '../../model/DescribeBean';
import { BusinessError } from '@kit.BasicServicesKit';
import { image } from '@kit.ImageKit';
import { MockSetup } from '@ohos/hamock';
import { TitleBarView } from '../../component/TitleBarView';
import { camera, cameraPicker } from '@kit.CameraKit';
import { picker } from '@kit.CoreFileKit';
import { CameraOptions, PickerUtil } from '@pura/picker_utils';


/**
 * 拍照、文件(文件、图片、视频、音频)选择和保存,工具类
 */
@Entry
@Component
struct Index {
  private scroller: Scroller = new Scroller();
  @State describe: DescribeBean = router.getParams() as DescribeBean;
  @State uriStr: string = ''
  @State filePath: string = ''; //本地图片path
  @State cacheUri: string = ''; //缓存本地Uri，上次保存的Uri。


  @MockSetup
  mock() {
    this.describe = new DescribeBean("PickerUtil", "拍照、文件(文件、图片、视频、音频)选择和保存,工具类");
  }


  async aboutToAppear(): Promise<void> {
    this.cacheUri = PreferencesUtil.getStringSync("picker_cache_uri");
    let pixelMap = await ImageUtil.getPixelMapFromMedia($r("app.media.test_as4"))
    this.filePath = await ImageUtil.savePixelMap(pixelMap, FileUtil.getFilesDirPath(""), "漂亮小姐姐.png")
    LogUtil.error("filePath: " + this.filePath);
  }

  build() {
    Column() {
      TitleBarView({ describe: this.describe })
      Divider()
      Scroll(this.scroller) {
        Column() {
          Button("cameraEasy()")
            .btnStyle()
            .onClick(async () => {
              PickerUtil.cameraEasy().then((uri) => {
                this.uriStr = `调用相机，返回uri：\n${uri}`;
              }).catch((err: BusinessError) => {
                this.uriStr = `调用相机，异常：\n${JSON.stringify(err)}`;
              });
            })
          Button("camera()")
            .btnStyle()
            .onClick(async () => {
              let options: CameraOptions = {
                mediaTypes: [cameraPicker.PickerMediaType.PHOTO],
                cameraPosition: camera.CameraPosition.CAMERA_POSITION_BACK
              }
              PickerUtil.camera(options).then((result) => {
                this.uriStr = `调用相机，返回uri：\n${result.resultUri}`;
              }).catch((err: BusinessError) => {
                this.uriStr = `调用相机，异常：\n${JSON.stringify(err)}`;
              });
            })
          Button("selectPhoto()")
            .btnStyle()
            .onClick(() => {
              PickerUtil.selectPhoto().then((uris) => {
                this.uriStr = `调用相册，返回uris：\n${uris.join('\n')}`;
              }).catch((err: BusinessError) => {
                this.uriStr = `调用相册，异常：\n${JSON.stringify(err)}`;
              });
            })
          Button("savePhoto()")
            .btnStyle()
            .onClick(() => {
              let imgName = `大漂亮_${DateUtil.getTodayTime()}.png`;
              let imgName1 = `小漂亮_${DateUtil.getTodayTime()}.png`;
              PickerUtil.savePhoto([imgName, imgName1]).then(async (uris) => {
                let uri = uris[0];
                this.uriStr = `调用保存图片，返回uris：\n${uri}`
                let file = FileUtil.openSync(uri);
                FileUtil.copyFile(this.filePath, file.fd).then(() => {
                  this.uriStr = `保存图片，返回uris：\n${uri}`
                  ToastUtil.showToast("图片1保存成功");
                })

                let file1 = FileUtil.openSync(uris[1]);
                let pixelMap1 = await ImageUtil.getPixelMapFromMedia($r("app.media.test_as3"))
                let packOpts: image.PackingOption = { format: 'image/png', quality: 100 }
                ImageUtil.packToFileFromPixelMap(pixelMap1, file1.fd, packOpts).then(() => {
                  this.uriStr = `保存图片，返回uris：\n${uris[1]}`
                  ToastUtil.showToast("图片2保存成功");
                })
              }).catch((err: BusinessError) => {
                this.uriStr = `调用保存图片，异常：\n${JSON.stringify(err)}`
              })
            })
          Button("selectDocument()")
            .btnStyle()
            .onClick(() => {
              let options: picker.DocumentSelectOptions = {
                maxSelectNumber: 9, //选择媒体文件数量的最大值,默认9。
                selectMode: picker.DocumentSelectMode.FILE, //支持选择的资源类型,默认文件
                // fileSuffixFilters: ['图片(.png, .jpg)|.png,.jpg', '文档|.txt', '视频|.mp4', '.pdf'], //选择文件的后缀类型['后缀类型描述|后缀类型']（可选） 若选择项存在多个后缀名，则每一个后缀名之间用英文逗号进行分隔（可选），后缀类型名不能超过100,选择所有文件：'所有文件(*.*)|.*';
                // defaultFilePathUri: "file://docs/storage/Users/currentUser/Download/com.harmony.utils", //指定选择的文件或者目录路径（可选）
                // authMode: true //选择是否对指定文件或目录授权，true为授权，当为true时，defaultFilePathUri为必选参数。
              }
              PickerUtil.selectDocument(options).then((uris) => {
                this.uriStr = `调用文件管理，返回uris：\n${uris.join('\n')}`
              }).catch((err: BusinessError) => {
                this.uriStr = `调用文件管理，异常：\n${JSON.stringify(err)}`
              });
            })
          Button("saveDocumentEasy()")
            .btnStyle()
            .onClick(() => {
              let fileName = `test_easy_${DateUtil.getTodayTime()}.txt`;
              PickerUtil.saveDocumentEasy([fileName]).then((paths) => {
                let path = paths[0];
                this.cacheUri = FileUtil.getUriFromPath(path);
                PreferencesUtil.put("picker_cache_uri", this.cacheUri);
                let txtStr = `“harmony-utils 一款高效的OpenHarmony/HarmonyOS工具包，封装了常用工具类，提供一系列简单易用的方法。帮助开发者快速构建鸿蒙应用。\n\n`;
                FileUtil.writeEasy(path, txtStr).then(() => {
                  this.uriStr = `文件保存成功，返回uris：\n${path}`;
                  ToastUtil.showToast("文件保存成功！");
                }).catch((err: BusinessError) => {
                  this.uriStr = `文件保存，异常：\n${JSON.stringify(err)}`;
                })
              }).catch((err: BusinessError) => {
                this.uriStr = `调用保存文件，异常：\n${JSON.stringify(err)}`;
              })
            })
          Button("saveDocument()")
            .btnStyle()
            .onClick(() => {
              let fileName = `test_${DateUtil.getTodayTime()}.txt`;
              PickerUtil.saveDocument({newFileNames:[fileName]}).then((uris) => {
                let uri = uris[0];
                this.cacheUri = uri
                PreferencesUtil.put("picker_cache_uri", this.cacheUri);
                let txtStr = `“harmony-utils 一款高效的OpenHarmony/HarmonyOS工具包，封装了常用工具类，提供一系列简单易用的方法。帮助开发者快速构建鸿蒙应用。\n\n`;
                FileUtil.writeEasy(uri, txtStr).then(() => {
                  this.uriStr = `文件保存成功，返回uris：\n${uri}`;
                  ToastUtil.showToast("文件保存成功！");
                }).catch((err: BusinessError) => {
                  this.uriStr = `文件保存，异常：\n${JSON.stringify(err)}`;
                })
              }).catch((err: BusinessError) => {
                this.uriStr = `调用保存文件，异常：\n${JSON.stringify(err)}`;
              })
            })
          Button("selectAudio()")
            .btnStyle()
            .onClick(() => {
              PickerUtil.selectAudio().then((uris) => {
                this.uriStr = `调用文件管理，返回uris：\n${uris.join('\n')}`;
              }).catch((err: BusinessError) => {
                this.uriStr = `调用文件管理，异常：\n${JSON.stringify(err)}`;
              });
            })
          Button("saveAudio()")
            .btnStyle()
            .onClick(() => {
              let fileName = `AudioViewPicker001.mp3`;
              PickerUtil.saveAudio([fileName]).then((uris) => {
                let uri = uris[0];
                this.uriStr = `音频文件，返回uris：\n${uri}`;
              }).catch((err: BusinessError) => {
                this.uriStr = `调用保存文件，异常：\n${JSON.stringify(err)}`;
              })
            })

          Text(this.uriStr)
            .visibility(StrUtil.isNotEmpty(this.uriStr) ? Visibility.Visible : Visibility.None)
            .textStyle()
            .margin(12)

          Blank().layoutWeight(1)
        }
        .margin({ top: 5, bottom: 5 })
      }
      .layoutWeight(1)
    }
    .width('100%')
    .height('100%')
    .justifyContent(FlexAlign.Start)
    .backgroundColor($r('app.color.main_background'))
  }
}


@Styles
function btnStyle() {
  .width('90%')
  .margin({ top: 10, bottom: 5 })
}

@Styles
function textStyle() {
  .width('95%')
  .padding(10)
  .shadow(ShadowStyle.OUTER_DEFAULT_XS)
  .margin({ top: 5, bottom: 10 })
  .border({ width: 1, color: Color.Grey, radius: 10, style: BorderStyle.Dashed })
}
```




## 🍎沟通与交流🙏

使用过程中发现任何问题都可以提 [Issue](https://gitee.com/tongyuyan/harmony-utils/issues) 给我们；   
当然，我们也非常欢迎你给我们发 [PR](https://gitee.com/tongyuyan/harmony-utils/pulls) 。


## 🌏开源协议

本项目基于 [Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0.html) ，在拷贝和借鉴代码时，请大家务必注明出处。
