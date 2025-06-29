# harmony-utils之WantUtil，Want工具类

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

##### toSetting  跳转系统设置页面（配合WantUtil里的URI常量一起使用，可跳转更多的设置页面）

```
 WantUtil.toSetting(WantUtil.URI_BIOMETRICS_AND_PASSWORD); //跳转生物识别和密码
 WantUtil.toSetting(WantUtil.URI_ABOUT_DEVICE); //跳转关于本机界面
 WantUtil.toSetting(WantUtil.URI_SYSTEM_AND_UPDATES); //系统和更新
 WantUtil.toSetting(WantUtil.URI_DISPLAY); //显示和亮度
 WantUtil.toSetting(WantUtil.URI_ACCESSIBILITY_FEATURE); //辅助功能
 WantUtil.toSetting(WantUtil.URI_APPLICATION_AND_SERVICE); //应用与元服务
```

##### toAppSetting  跳转应用设置页面

```
WantUtil.toAppSetting();
```

##### toNotificationSetting  跳转通知设置页面

```
 WantUtil.toNotificationSetting();
```

##### toNetworkSetting  跳转移动网络设置页面

```
 WantUtil.toNetworkSetting();
```

##### toWifiSetting  跳转WLAN设置页面

```
 WantUtil.toWifiSetting();
```

##### toBluetoothSetting  跳转蓝牙设置页面

```
 WantUtil.toBluetoothSetting();
```

##### toNfcSetting  跳转NFC设置页面

```
 WantUtil.toNfcSetting();
```

##### toVolumeSetting  跳转声音和振动设置页面

```
WantUtil.toVolumeSetting();
```

##### toStorageSetting  跳转存储设置页面

```
WantUtil.toStorageSetting();
```

##### toBatterySetting  跳转电池设置页面

```
 WantUtil.toBatterySetting(); 
```

##### toWebBrowser  拉起系统浏览器

```
WantUtil.toWebBrowser("https://developer.huawei.com/")
  .catch((err: BusinessError) => {
    LogUtil.error(JSON.stringify(err));
    ToastUtil.showToast("拉起失败！");
  });
```

##### toAppGalleryDetail  拉起应用市场对应的应用详情界面

```
WantUtil.toAppGalleryDetail("com.harmony.utils")
  .catch((err: BusinessError) => {
    LogUtil.error(JSON.stringify(err));
    ToastUtil.showToast("拉起失败！");
  });
```

##### toFileManagement  拉起系统文件管理器

```
WantUtil.toFileManagement()
  .catch((err: BusinessError) => {
    LogUtil.error(JSON.stringify(err));
    ToastUtil.showToast("拉起失败！");
  });
```

##### startMMS  拉起短信界面并指定联系人

```
WantUtil.startMMS("13909626520", "张三").then(() => {
  ToastUtil.showToast("拉起短信界面…")
}).catch((err: BusinessError) => {
  LogUtil.error(JSON.stringify(err));
  ToastUtil.showToast("拉起失败！");
});
```

##### openFile  调用三方软件打开文件

```
let docPath = FileUtil.getFilesDirPath('download/wps/doc', '测试DOC文件.doc');
let uri = FileUtil.getUriFromPath(docPath);
WantUtil.openFile(uri).catch((error: BusinessError) => {
  ToastUtil.showToast("打开文件失败，" + error.message);
  LogUtil.error(`打开文件异常 ~ code: ${error.code} -·- message: ${error.message}`);
});
```

## 创作不易，请给童长老点赞👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   

