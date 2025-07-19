# harmony-web (API12)

## 🏆Introduction and Recommendations

[harmony-web](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-web)It is a WebView based on Hongmeng
The powerful and extremely easy-to-use library is not only lightweight, flexible and flexible, but also provides a series of problem solutions for Hongmeng WebView, helping developers to easily deal with various development challenges.

[harmony-utils](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)
A HarmonyOS tool library with rich features and extremely easy to use, with the help of many practical tools, is committed to helping developers quickly build Hongmeng applications.

[harmony-dialog](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-dialog)
An extremely simple and easy-to-use zero-invasion pop-up window, which can be easily implemented with just one line of code, and can be easily popped up no matter where you are.

## 🌞Download and install

`ohpm i @pura/harmony-web`

OpenHarmony ohpm
For more information, please refer to[如何安装 OpenHarmony ohpm 包](https://ohpm.openharmony.cn/#/cn/help/downloadandinstall)
<br>


## 📚 ***ArkWeb*** Component, Parameter Description

| Name | Type | Description | Required |
|:------------|:----------------------------|:-------------|:-----|
| controller | webview.WebviewController | Controller | Y |
| src | ResourceStr | Web Resource Address | Y |
| options | ArkWebOptions | ArkWeb property parameters | N |
| webClient | ArkWebClient | ArkWeb Lifecycle Events | N |
| arkJsObject | ArkJsObject or ArkJsObject[] | Interface object that needs to be registered | N |

## 📚 ArkWebHelper, method description

| Method name | Introduction |
|:-------------------|:----------------------|
| init | Initialization |
| prepareForPageLoad | Pre-connect url, call this API before loading the url |

## 📚Sample code

```
@Entry
@ComponentV2
struct Index {
  private controller: webview.WebviewController = new webview.WebviewController();
  @Local webUrl: string = "";
  @Local options: ArkWebOptions = new ArkWebOptions();
  @Local webClient: MyWebClient = new MyWebClient();
  @Local jsObject: MyJsObject = new MyJsObject();

  onBackPress(): boolean {
    if (this.controller?.accessBackward()) {
      this.controller?.backward();
      return true;
    }
    return false;
  }

  aboutToAppear(): void {
    let params: Params = router.getParams() as Params;
    this.webUrl = params.webUrl;
  }

  build() {
    Column() {
      ArkWeb({
        controller: this.controller,
        src: this.webUrl,
        options: this.options,
        webClient: this.webClient,
        arkJsObject: this.jsObject
      })
    }
    .height('100%')
    .width('100%')
  }

}



import { router } from '@kit.ArkUI';
import { ArkJsObject } from '@pura/harmony-web';
import { JSONUtil, LogUtil } from '@pura/harmony-utils';
import { User } from '../model/User';


/**
 * JS交互 */
export class MyJsObject extends ArkJsObject {

  //关闭页面
  closePage(str?: string) {
    LogUtil.error(`closePage: ${str}`);
    router.back();
  }

  async onDemo() {
    let user: User = new User();
    let str: string = JSONUtil.beanToJsonStr(user);

    this.runJavaScriptFun("onH5Demo", str ).then((data)=>{
      LogUtil.error(`网页回传值：${data}`);
    });
  }

}



import { ImageUtil, LogUtil } from '@pura/harmony-utils';
import { ArkWebClient } from '@pura/harmony-web';
import { webview } from '@kit.ArkWeb';
import { Utils } from './Utils';
import { DialogHelper } from '@pura/harmony-dialog';
import { cameraPicker } from '@kit.CameraKit';
import { BusinessError } from '@kit.BasicServicesKit';
import { CameraOptions, PickerUtil } from '@pura/picker_utils';

/**
 * Web事件 */
export class MyWebClient implements ArkWebClient {
  controller?: webview.WebviewController;

  private onPageBeginCallback?: Callback<OnPageBeginEvent>;

  setOnPageBegin(onPageBeginCallback: Callback<OnPageBeginEvent>) {
    this.onPageBeginCallback = onPageBeginCallback;
  }


  setWebviewController(controller: webview.WebviewController): void {
    this.controller = controller;
  }

  onControllerAttached(): void {
    //重新定义UserAgent，在原来的UserAgent的上拼接“Linux”，这样就能调用原来Android的JS方法
    this.controller?.setCustomUserAgent(`${this.controller?.getUserAgent()},Linux`)
  }

  onPageBegin(event: OnPageBeginEvent): void {
    this.onPageBeginCallback?.(event);
    LogUtil.info(`onPageBegin => ` + event.url);
  }


  //文件选择
  onShowFileSelector(event: OnShowFileSelectorEvent): boolean {
    const isCapture = event.fileSelector.isCapture(); //是否拍照/拍视频
    if (isCapture) { //拍照/拍视频
      PickerUtil.cameraEasy().then((result) => {
        event.result.handleFileList([result]);
      });
    } else {
      const types = event.fileSelector.getAcceptType() ?? [];
      const mode = event.fileSelector.getMode();
      const isPhoto = Utils.isPhoto(types);
      const isVideo = Utils.isVideo(types);
      if (isPhoto || isVideo) { //图片、视频
        let sheets = isPhoto ? ["拍照", "选择照片"] : ["拍视频", "选择视频"];
        DialogHelper.showActionSheetDialog({
          title: "请选择",
          sheets: sheets,
          onAction: (action) => {
            if (action === 0) {
              let options = new CameraOptions();
              options.mediaTypes = isPhoto ? [cameraPicker.PickerMediaType.PHOTO] : [cameraPicker.PickerMediaType.VIDEO];
              PickerUtil.cameraEasy(options).then((result) => {
                if (isPhoto) { //对拍照的图片进行压缩，压缩到3M以内
                  ImageUtil.compressPhoto(result, 1024 * 3).then((path) => {
                    event.result.handleFileList([path]);
                  }).catch((err: BusinessError) => {
                    event.result.handleFileList([result]); //图片压缩异常时，使用原图。
                    LogUtil.error(`拍照图片压缩异常：${err.code} - ${err.message}`);
                  });
                } else {
                  event.result.handleFileList([result]);
                }
              });
            } else {
              PickerUtil.selectDocument({
                maxSelectNumber: mode === FileSelectorMode.FileOpenMode ? 1 : 9,
                fileSuffixFilters: types
              }).then((result) => {
                event.result.handleFileList(result);
              })
            }
          }
        })
      } else { //文档
        PickerUtil.selectDocument({
          maxSelectNumber: mode === FileSelectorMode.FileOpenMode ? 1 : 9,
          fileSuffixFilters: types
        }).then((result) => {
          event.result.handleFileList(result);
        })
      }
    }
    return true;
  }

}





```


## 🍎Communication and communication 🙏

Any problems found during use can be asked[Issue](https://gitee.com/tongyuyan/harmony-utils/issues)Give us;
Of course, we also welcome you to send us a message[PR](https://gitee.com/tongyuyan/harmony-utils/pulls) 。

[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[https://github.com/787107497](https://github.com/787107497)


## 🌏Open Source Protocol

This project is based on[Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0.html), when copying and borrowing codes, please be sure to indicate the source.
