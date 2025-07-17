# ScanUtils, code tool class (scan code, code image generation, picture identification)

## Introduction and description of harmony-utils

------
[harmony-utils](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils) A HarmonyOS tool library with rich features and extremely easy to use, with the help of many practical tools, is committed to helping developers quickly build Hongmeng applications. Its encapsulated tools cover APP, device, screen, authorization, notification, inter-thread communication, pop-up frames, toast, biometric authentication, user preferences, taking photos, albums, scanning codes, files, logs, exception capture, characters, strings, numbers, collections, dates, random, base64, encryption, decryption, JSON and other functions, which can meet various development needs.     
[picker_utils](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fpicker_utils) It is a sub-store split by harmony-utils, including PickerUtil, PhotoHelper, and ScanUtil.

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

##### startScanForResult calls the default interface to scan the code, and use the Promise method to asynchronously return the decoded result.

```
ScanUtil.startScanForResult().then((scanResult) => {
  let scanStr1 = JSON.stringify(scanResult, null, 2);
});
```

##### generateBarcode code diagram generation, use Promise to asynchronously return the generated code diagram

```
let txtStr = "harmony-utils 一款高效的OpenHarmony/HarmonyOS工具包，封装了常用工具类，提供一系列简单易用的方法";
let pixelMap = await ScanUtil.generateBarcode(txtStr);
ImageUtil.savePixelMap(pixelMap, FileUtil.getFilesDirPath(""), "qr_code.png");
```

##### decode calls picture identification and uses Promise to return the identification result asynchronously

```
let filePath = FileUtil.getFilesDirPath("","qr_code.png");
if (FileUtil.accessSync(this.filePath)) {
  ScanUtil.decode(this.filePath).then((scanResult) => {
    let scanStr3 = JSON.stringify(scanResult, null, 2);
  })
} else {
  ToastUtil.showToast("请先点击generateBarcode生成二维码图片");
}
```

##### decodeImage calls image data identification capability and uses Promise asynchronous callback to return code identification results

```
//优先获取图像的YuvByteBuffer, YuvHeight, YuvWidth数据，比如获取宽高是1920*1080时
let byteImg: detectBarcode.ByteImage = {
  byteBuffer: YuvByteBuffer,
  width: 1920,
  height: 1080,
  format: detectBarcode.ImageFormat.NV21
};
ScanUtil.decodeImage(byteImg).then((scanResult) => {
  let scanStr3 = JSON.stringify(scanResult, null, 2);
});
```

##### onPickerScanForResult Pull up the gallery through picker and select the picture, and call the picture identification code

```
ScanUtil.onPickerScanForResult().then((scanResult) => {
  let scanStr2 = JSON.stringify(scanResult, null, 2);
  Utils.showSheetText(scanStr2);
}).catch((err: BusinessError) => {
  ToastUtil.showToast("扫码异常！");
});
```

##### canIUseScan judgement

```
let canIUseScan = ScanUtil.canIUseScan();
ToastUtil.showToast(`当前设备是否支持码能力：${canIUseScan}`);
```

## Full Code Example

------

```
import { router } from '@kit.ArkUI';
import { DescribeBean } from '../../model/DescribeBean';
import { FileUtil, ImageUtil, LogUtil, ToastUtil } from '@pura/harmony-utils';
import { MockSetup } from '@ohos/hamock';
import { TitleBarView } from '../../component/TitleBarView';
import { BusinessError } from '@kit.BasicServicesKit';
import { ScanUtil } from '@pura/picker_utils';
import { Utils } from '../../utils/Utils';
import { detectBarcode } from '@kit.ScanKit';

/**
 * 码工具类（扫码、码图生成、图片识码）
 */
@Entry
@Component
struct Index {
  private scroller: Scroller = new Scroller();
  @State describe: DescribeBean = router.getParams() as DescribeBean;
  private txtStr: string = "harmony-utils 一款高效的OpenHarmony/HarmonyOS工具包，封装了常用工具类，提供一系列简单易用的方法";
  private readonly fileName: string = "qr_code.png";
  @State filePath: string = '';


  @MockSetup
  mock() {
    this.describe = new DescribeBean("ScanUtil", "码工具类（扫码、码图生成、图片识码）");
  }


  aboutToAppear(): void {
    this.filePath = FileUtil.getFilesDirPath("",this.fileName)
  }

  onBackPress(): boolean {
    return false;
  }

  build() {
    Column() {
      TitleBarView({ describe: this.describe })
      Divider()
      Scroll(this.scroller) {
        Column() {
          Button("startScanForResult()")
            .btnStyle()
            .onClick(() => {
              if (ScanUtil.canIUseScan()) {
                ScanUtil.startScanForResult().then((scanResult) => {
                  let scanStr1 = JSON.stringify(scanResult, null, 2);
                  Utils.showSheetText(scanStr1);
                });
              } else {
                ToastUtil.showToast("当前设备不支持码能力！")
              }
            })
          Button("generateBarcode()")
            .btnStyle()
            .onClick(async () => {
              if (ScanUtil.canIUseScan()) {
                let pixelMap = await ScanUtil.generateBarcode(this.txtStr);
                ImageUtil.savePixelMap(pixelMap, FileUtil.getFilesDirPath(""), this.fileName);
                Utils.showSheetImg(pixelMap);
              } else {
                ToastUtil.showToast("当前设备不支持码能力！");
              }
            })
          Button("decode()")
            .btnStyle()
            .onClick(() => {
              if (ScanUtil.canIUseScan()) {
                if (FileUtil.accessSync(this.filePath)) {
                  ScanUtil.decode(this.filePath).then((scanResult) => {
                    let scanStr3 = JSON.stringify(scanResult, null, 2);
                    Utils.showSheetText(scanStr3);
                  })
                } else {
                  ToastUtil.showToast("请先点击generateBarcode生成二维码图片");
                }
              } else {
                ToastUtil.showToast("当前设备不支持码能力！");
              }
            })
          Button("decodeImage()")
            .btnStyle()
            .onClick(async () => {
                let pixelMap = await ScanUtil.generateBarcode(this.txtStr);
                let arrayBuffer = await ImageUtil.packingFromPixelMap(pixelMap, { format: 'image/png', quality: 100 });
                let byteImg: detectBarcode.ByteImage = {
                  byteBuffer: arrayBuffer,
                  width: pixelMap.getImageInfoSync().size.width,
                  height: pixelMap.getImageInfoSync().size.height,
                  format: detectBarcode.ImageFormat.NV21
                };
                ScanUtil.decodeImage(byteImg).then((scanResult) => {
                  let scanStr3 = JSON.stringify(scanResult, null, 2);
                  Utils.showSheetText(scanStr3);
                });

            })
          Button("onPickerScanForResult()")
            .btnStyle()
            .onClick(() => {
              if (ScanUtil.canIUseScan()) {
                ScanUtil.onPickerScanForResult().then((scanResult) => {
                  let scanStr2 = JSON.stringify(scanResult, null, 2);
                  Utils.showSheetText(scanStr2);
                }).catch((err: BusinessError) => {
                  ToastUtil.showToast("扫码异常！");
                  LogUtil.error("扫码异常：code:" + err.code + " ~ msg:" + err.message);
                });
              } else {
                ToastUtil.showToast("当前设备不支持扫码能力！");
              }
            })
          Button("canIUseScan()")
            .btnStyle()
            .onClick(() => {
              let canIUseScan = ScanUtil.canIUseScan();
              ToastUtil.showToast(`当前设备是否支持码能力：${canIUseScan}`);
            })

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
```

## Creation is not easy, please give Elder Tong a thumbs up 👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   



