# Harmony-utils AuthUtils, biometric related tool category

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

##### getAvailableStatus query whether the authentication capability of the specified type and level supports

```
let status = AuthUtil.getAvailableStatus(userIAM_userAuth.UserAuthType.FACE, userIAM_userAuth.AuthTrustLevel.ATL1)
if (status.status) {
  ToastUtil.showToast("当前设备支持人脸识别");
} else {
  ToastUtil.showToast("当前设备不支持人脸识别");
  LogUtil.error(JSON.stringify(status, null, 2));
}
```

##### onStartEasy Start authentication, use fingerprint and password authentication

```
AuthUtil.onStartEasy(true, (result: userAuth.UserAuthResult) => {
  let resultStr = JSON.stringify(result, null, 2);
});
```

##### onStart starts authentication, user-specified type authentication

```
AuthUtil.onStart({
  authType: [userAuth.UserAuthType.FACE],
  authTrustLevel: userAuth.AuthTrustLevel.ATL3,
  title: '请验证人脸',
  showTip: true
}, (result) => {
  let resultStr = JSON.stringify(result, null, 2);
});
```

##### cancel cancel

```
 AuthUtil.cancel();
```

##### generateChallenge generates challenge values ​​to prevent replay attacks

```
 let challenge = AuthUtil.generateChallenge();
```

##### getErrorMsg Get error msg

```
 const errorTip = AuthUtil.getErrorMsg(result.result, '');
```


## Full Code Example

------

```
import { router } from '@kit.ArkUI';
import { AuthUtil, LogUtil, ToastUtil } from '@pura/harmony-utils';
import { DescribeBean } from '../../model/DescribeBean';
import userIAM_userAuth from '@ohos.userIAM.userAuth';
import userAuth from '@ohos.userIAM.userAuth';
import { MockSetup } from '@ohos/hamock';
import { TitleBarView } from '../../component/TitleBarView';
import { Utils } from '../../utils/Utils';

/**
 * 手机的生物认证（指纹、人脸、密码）工具类
 */
@Entry
@Component
struct Index {
  private scroller: Scroller = new Scroller();
  @State describe: DescribeBean = router.getParams() as DescribeBean;


  @MockSetup
  mock() {
    this.describe = new DescribeBean("AuthUtil", "手机的生物认证（指纹、人脸、密码）工具类");
  }

  build() {
    Column() {
      TitleBarView({ describe: this.describe })
      Divider()
      Scroll(this.scroller) {
        Column() {
          Button("getAvailableStatus()")
            .btnStyle()
            .onClick(() => {
              let status = AuthUtil.getAvailableStatus(userIAM_userAuth.UserAuthType.FACE, userIAM_userAuth.AuthTrustLevel.ATL1)
              if (status.status) {
                ToastUtil.showToast("当前设备支持人脸识别")
              } else {
                ToastUtil.showToast("当前设备不支持人脸识别");
                LogUtil.error(JSON.stringify(status, null, 2));
              }
            })
          Button("getAvailableStatus()")
            .btnStyle()
            .onClick(() => {
              let status = AuthUtil.getAvailableStatus(userIAM_userAuth.UserAuthType.FINGERPRINT, userIAM_userAuth.AuthTrustLevel.ATL2)
              if (status.status) {
                ToastUtil.showToast("当前设备支持指纹识别")
              } else {
                ToastUtil.showToast("当前设备不支持指纹识别")
                LogUtil.error(JSON.stringify(status, null, 2));
              }
            })
          Button("getAvailableStatus()")
            .btnStyle()
            .onClick(() => {
              let status = AuthUtil.getAvailableStatus(userIAM_userAuth.UserAuthType.PIN, userIAM_userAuth.AuthTrustLevel.ATL2)
              if (status.status) {
                ToastUtil.showToast("当前设备支持口令识别")
              } else {
                ToastUtil.showToast("当前设备不支持口令识别");
                LogUtil.error(JSON.stringify(status, null, 2));
              }
            })
          Button("onStartEasy()")
            .btnStyle()
            .onClick(() => {
              AuthUtil.onStartEasy(true, (result: userAuth.UserAuthResult) => {
                let resultStr = JSON.stringify(result, null, 2);
                Utils.showSheetText(resultStr);
              });
            })
          Button("onStart()")
            .btnStyle()
            .onClick(() => {
              AuthUtil.onStart({
                authType: [userAuth.UserAuthType.FACE],
                authTrustLevel: userAuth.AuthTrustLevel.ATL3,
                title: '请验证人脸',
                showTip: true
              }, (result) => {
                let resultStr = JSON.stringify(result, null, 2);
                Utils.showSheetText(resultStr);
              });
            })
          Button("cancel()")
            .btnStyle()
            .onClick(() => {
              AuthUtil.cancel();
            })
          Button("generateChallenge")
            .btnStyle()
            .onClick(() => {
              let challenge = AuthUtil.generateChallenge();
              Utils.showSheetText(`挑战值: ${challenge}`);
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
   



