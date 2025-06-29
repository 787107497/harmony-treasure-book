# harmony-utils: WantUtil, Want tool class

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

##### toSetting jumps to the system settings page (used with the URI constants in WantUtil to jump to more settings pages)

```
 WantUtil.toSetting(WantUtil.URI_BIOMETRICS_AND_PASSWORD); //跳转生物识别和密码
 WantUtil.toSetting(WantUtil.URI_ABOUT_DEVICE); //跳转关于本机界面
 WantUtil.toSetting(WantUtil.URI_SYSTEM_AND_UPDATES); //系统和更新
 WantUtil.toSetting(WantUtil.URI_DISPLAY); //显示和亮度
 WantUtil.toSetting(WantUtil.URI_ACCESSIBILITY_FEATURE); //辅助功能
 WantUtil.toSetting(WantUtil.URI_APPLICATION_AND_SERVICE); //应用与元服务
```

##### toAppSetting Jump toAppSetting

```
WantUtil.toAppSetting();
```

##### toNotificationSetting Jump Notification Setting Page

```
 WantUtil.toNotificationSetting();
```

##### toNetworkSetting Jump to the mobile network settings page

```
 WantUtil.toNetworkSetting();
```

##### toWifiSetting Jump to WLAN Settings Page

```
 WantUtil.toWifiSetting();
```

##### toBluetoothSetting Jump to Bluetooth Settings Page

```
 WantUtil.toBluetoothSetting();
```

##### toNfcSetting Jump to NFC Settings Page

```
 WantUtil.toNfcSetting();
```

##### toVolumeSetting Jump Sound and Vibration Settings Page

```
WantUtil.toVolumeSetting();
```

##### toStorageSetting Jump Storage Settings Page

```
WantUtil.toStorageSetting();
```

##### toBatterySetting Jump Battery Settings Page

```
 WantUtil.toBatterySetting(); 
```

##### toWebBrowser Pull up the system browser

```
WantUtil.toWebBrowser("https://developer.huawei.com/")
  .catch((err: BusinessError) => {
    LogUtil.error(JSON.stringify(err));
    ToastUtil.showToast("拉起失败！");
  });
```

##### toAppGalleryDetail pulls up the application details interface corresponding to the application market

```
WantUtil.toAppGalleryDetail("com.harmony.utils")
  .catch((err: BusinessError) => {
    LogUtil.error(JSON.stringify(err));
    ToastUtil.showToast("拉起失败！");
  });
```

##### toFileManagement Pull up the system file manager

```
WantUtil.toFileManagement()
  .catch((err: BusinessError) => {
    LogUtil.error(JSON.stringify(err));
    ToastUtil.showToast("拉起失败！");
  });
```

##### startMMS pull up the SMS interface and specify the contact person

```
WantUtil.startMMS("13909626520", "张三").then(() => {
  ToastUtil.showToast("拉起短信界面…")
}).catch((err: BusinessError) => {
  LogUtil.error(JSON.stringify(err));
  ToastUtil.showToast("拉起失败！");
});
```

##### openFile calls three-party software to open the file

```
let docPath = FileUtil.getFilesDirPath('download/wps/doc', '测试DOC文件.doc');
let uri = FileUtil.getUriFromPath(docPath);
WantUtil.openFile(uri).catch((error: BusinessError) => {
  ToastUtil.showToast("打开文件失败，" + error.message);
  LogUtil.error(`打开文件异常 ~ code: ${error.code} -·- message: ${error.message}`);
});
```

## Creation is not easy, please give Elder Tong a thumbs up 👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   

