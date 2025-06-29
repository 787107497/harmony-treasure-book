# harmony-utils之CrashUtil，异常相关工具类

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

##### onHandled  注册错误观测器（该方法建议在Ability里调用） 。注册后可以捕获到应用产生的js crash，应用崩溃时进程不会退出。将异常信息写入本地文件

```
CrashUtil.onHandled((exceptionInfo)=>{
  LogUtil.error(JSON.stringify(exceptionInfo, null, 2));
});
```

##### onDestroy  注销错误观测器

```
CrashUtil.onDestroy(); //注销错误观测器
ToastUtil.showToast("注销误观测器,成功！");
```

##### isHandled  判断错误观测器是否存在

```
let isHandled = CrashUtil.isHandled();
ToastUtil.showToast(`误观测器是否存在：${isHandled}`);
```

##### getFilePath  获取日志文件路径（用于读取异常文件、导出异常文件）

```
let path = CrashUtil.getFilePath();
LogUtil.error(`异常日志文件路径：${path}`);
```

##### access  判断日志文件是否存在

```
let access = CrashUtil.access();
ToastUtil.showToast(`日志文件是否存在：${access}`);
```

##### delete  删除日志文件

```
CrashUtil.delete();
ToastUtil.showToast(`日志文件删除成功！`);
```

##### getExceptionJson  获取异常日志的JSON字符串

```
if (CrashUtil.access()) {
  let jsonStr = await CrashUtil.getExceptionJson(); //读取JSON
  Utils.showSheetText(jsonStr);
} else {
  ToastUtil.showToast("暂无日志文件");
}
```

##### getExceptionList  获取异常日志的集合

```
if (CrashUtil.access()) {
  let list = await CrashUtil.getExceptionList();
  DialogHelper.showToast(`异常个数：${list.length}`);
} else {
  ToastUtil.showToast("暂无日志文件");
}
```

##### enableAppRecovery  启用应用恢复功能，参数按顺序填入。该接口调用后，应用从启动器启动时第一个Ability支持恢复

```
CrashUtil.enableAppRecovery();
```

##### restartApp  重启APP，并拉起应用启动时第一个Ability，可以配合errorManager相关接口使用

```
CrashUtil.restartApp();
```

##### saveAppState  保存当前App状态 或 主动保存Ability的状态，这个状态将在下次恢复启动时使用。可以配合errorManager相关接口使用

```
CrashUtil.saveAppState(this.context);
```

##### setRestartWant  设置下次恢复主动拉起场景下的Ability。该Ability必须为当前包下的UIAbility

```
let want: Want = {
  bundleName: 'com.harmony.utils',
  abilityName: 'EntryAbility'
};
CrashUtil.setRestartWant(want);
```

 
   



