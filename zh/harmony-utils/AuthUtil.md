# harmony-utils之AuthUtil，生物认证相关工具类

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

##### getAvailableStatus  查询指定类型和等级的认证能力是否支持

```
let status = AuthUtil.getAvailableStatus(userIAM_userAuth.UserAuthType.FACE, userIAM_userAuth.AuthTrustLevel.ATL1)
if (status.status) {
  ToastUtil.showToast("当前设备支持人脸识别");
} else {
  ToastUtil.showToast("当前设备不支持人脸识别");
  LogUtil.error(JSON.stringify(status, null, 2));
}
```

##### onStartEasy  开始认证,使用指纹和密码认证

```
AuthUtil.onStartEasy(true, (result: userAuth.UserAuthResult) => {
  let resultStr = JSON.stringify(result, null, 2);
});
```

##### onStart  开始认证，用户指定类型认证

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

##### cancel  取消认证

```
 AuthUtil.cancel();
```

##### generateChallenge 生成挑战值,用来防重放攻击

```
 let challenge = AuthUtil.generateChallenge();
```

##### getErrorMsg 获取错误msg

```
 const errorTip = AuthUtil.getErrorMsg(result.result, '');
```

## 创作不易，请给童长老点赞👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   



