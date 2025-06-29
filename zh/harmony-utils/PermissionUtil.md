# harmony-utils之PermissionUtil，授权相关工具类

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

##### requestPermissionsEasy  申请授权，拒绝后并二次向用户申请授权（申请权限，建议使用该方法）

```
let p: Permissions[] = ['ohos.permission.ACTIVITY_MOTION', 'ohos.permission.CAMERA', 'ohos.permission.LOCATION', 'ohos.permission.APPROXIMATELY_LOCATION'];
PermissionUtil.requestPermissionsEasy(p).then((result) => {
  ToastUtil.showToast(`申请授权，结果：${result}`);
})
```

##### checkPermissions  校验当前是否已经授权

```
let p: Permissions = 'ohos.permission.CAMERA'; //相机
PermissionUtil.checkPermissions(p).then((result) => {
ToastUtil.showToast(`检测是否授权，结果：${result}`);
})
```

##### checkRequestPermissions  校验是否授权后并申请授权

```
let p: Permissions = 'ohos.permission.CAMERA'; //相机
PermissionUtil.checkRequestPermissions(p).then((grant) => {
  ToastUtil.showToast(`检测并申请授权，结果：${grant}`);
  if (!grant) {
    WantUtil.toAppSetting(); //拒绝权限，跳转APP设置页面
  }
})
```

##### requestPermissions  申请授权

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

##### requestPermissionOnSetting  二次向用户申请授权（单个权限 或 读写权限组，建议使用该方法）

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

##### requestPermissionOnSettingEasy  二次向用户申请授权（多个权限建议使用该方法）

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

##### requestGlobalSwitch  用于UIAbility/UIExtensionAbility拉起全局开关设置弹框。部分情况下，录音、拍照等功能禁用，应用可拉起此弹框请求用户同意开启对应功能。如果当前全局开关的状态为开启，则不拉起弹框

```
PermissionUtil.requestGlobalSwitch(abilityAccessCtrl.SwitchType.LOCATION).then((result) => {
  ToastUtil.showToast(`申请结果：${result}`);
}).catch((err: BusinessError) => {
  ToastUtil.showToast(err.message);
  LogUtil.error(err);
});
```

## 创作不易，请给童长老点赞👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   



