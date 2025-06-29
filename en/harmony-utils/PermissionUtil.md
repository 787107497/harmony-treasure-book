# PermissionUtils of harmony-utils, authorization related tool classes

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

##### requestPermissionsEasy Apply for authorization, after rejection, and apply for authorization to the user again (apply for permission, it is recommended to use this method)

```
let p: Permissions[] = ['ohos.permission.ACTIVITY_MOTION', 'ohos.permission.CAMERA', 'ohos.permission.LOCATION', 'ohos.permission.APPROXIMATELY_LOCATION'];
PermissionUtil.requestPermissionsEasy(p).then((result) => {
  ToastUtil.showToast(`申请授权，结果：${result}`);
})
```

##### checkPermissions Check if it is currently authorized

```
let p: Permissions = 'ohos.permission.CAMERA'; //相机
PermissionUtil.checkPermissions(p).then((result) => {
ToastUtil.showToast(`检测是否授权，结果：${result}`);
})
```

##### checkRequestPermissions After verifying whether authorization is authorized and apply for authorization

```
let p: Permissions = 'ohos.permission.CAMERA'; //相机
PermissionUtil.checkRequestPermissions(p).then((grant) => {
  ToastUtil.showToast(`检测并申请授权，结果：${grant}`);
  if (!grant) {
    WantUtil.toAppSetting(); //拒绝权限，跳转APP设置页面
  }
})
```

##### requestPermissions

```
let p: Permissions[] = ['ohos.permission.ACTIVITY_MOTION', 'ohos.permission.CAMERA','ohos.permission.LOCATION', 'ohos.permission.APPROXIMATELY_LOCATION'];
PermissionUtil.requestPermissions(p).then((grant) => {
  if (grant) {
    ToastUtil.showToast(`申请授权，已通过...`);
  } else { //拒绝权限，二次向用户申请授权
    PermissionUtil.requestPermissionOnSettingEasy(p).then((result) => {
      ToastUtil.showToast(`申请授权，结果：${result}`);
    });
  }
})
```

##### requestPermissionOnSetting Secondary application for authorization to the user (single permissions or read and write permission groups, this method is recommended)

```
let ps: Permissions[] = ['ohos.permission.READ_IMAGEVIDEO', 'ohos.permission.WRITE_IMAGEVIDEO'];
PermissionUtil.requestPermissions(ps).then((result) => {
  if (result) {
    ToastUtil.showToast(`最佳使用案例授权，已通过...`);
  } else {
    PermissionUtil.requestPermissionOnSetting(ps).then((grant) => {
      ToastUtil.showToast(`最佳使用案例，结果：${grant}`);
    })
  }
})
```

##### requestPermissionOnSettingEasy Secondary application for authorization to the user (this method is recommended for multiple permissions)

```
let p: Permissions[] = ['ohos.permission.ACTIVITY_MOTION', 'ohos.permission.CAMERA','ohos.permission.LOCATION', 'ohos.permission.APPROXIMATELY_LOCATION'];
PermissionUtil.requestPermissions(p).then((grant) => {
  if (grant) {
    ToastUtil.showToast(`申请授权，已通过...`);
  } else { //拒绝权限，二次向用户申请授权
    PermissionUtil.requestPermissionOnSettingEasy(p).then((result) => {
      ToastUtil.showToast(`申请授权，结果：${result}`);
    });
  }
})
```

##### requestGlobalSwitch is used for UIAbility/UIExtensionAbility to pull up the global switch to set the pop-up box. In some cases, recording, taking photos and other functions are disabled. The application can pull up this box and ask the user to agree to enable the corresponding functions. If the current global switch is on, the pop-up box will not be pulled

```
PermissionUtil.requestGlobalSwitch(abilityAccessCtrl.SwitchType.LOCATION).then((result) => {
  ToastUtil.showToast(`申请结果：${result}`);
}).catch((err: BusinessError) => {
  ToastUtil.showToast(err.message);
  LogUtil.error(err);
});
```

## Creation is not easy, please give Elder Tong a thumbs up 👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   



