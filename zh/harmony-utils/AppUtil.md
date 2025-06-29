# harmony-utils之AppUtil，APP相关工具类

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

##### init  初始化方法,缓存全局变量，在UIAbility的onCreate方法中初始化该方法

```
  onCreate(want: Want, launchParam: AbilityConstant.LaunchParam): void {
    AppUtil.init(this.context);
  }
```

##### isApiSupported 检查API版本是否安全

```
   let bl = AppUtil.isApiSupported(18);
```

##### getApplicationContext 获取ApplicationContext

```
   let applicationContext = AppUtil.getApplicationContext();
```

##### getContext 获取UIContext

```
   let uiContext = AppUtil.getUIContext();
```

##### getWindowStage 获取WindowStage

```
  let windowStage = AppUtil.getWindowStage();
  LogUtil.error(JSON.stringify(windowStage, null, 2));
```

##### getMainWindow 获取主窗口

```
 let mainWindow = AppUtil.getMainWindow();
```

##### getConfiguration 获取应用的Configuration

```
 let config = AppUtil.getConfiguration();
```

##### setGrayScale 设置灰阶，APP一键置灰

```
 AppUtil.setGrayScale(1);
```

##### setColorMode 设置应用的颜色模式。仅支持主线程调用。设置颜色模式，包括：深色模式、浅色模式、不设置（跟随系统）

```
  AppUtil.setColorMode(ConfigurationConstant.ColorMode.COLOR_MODE_LIGHT);
```

##### getColorMode 获取应用的颜色模式

```
  let colorMode = AppUtil.getColorMode();
  ToastUtil.showToast(`应用的颜色模式:${colorMode}`);
```

##### setFont 设置应用的字体类型。仅支持主线程调用

```
  font.registerFont({ familyName: 'WCSF', familySrc: $rawfile('wcsf.ttf') });
  AppUtil.setFont('WCSF');
```

##### setFontSizeScale 设置应用字体大小缩放比例。仅支持主线程调用。<API13+>

```
  AppUtil.setFontSizeScale(1.8);
```

##### getFontSizeScale 获取应用字体大小缩放比例

```
  let fontSizeScale = AppUtil.getFontSizeScale();
  ToastUtil.showToast(`应用字体大小缩放比例:${fontSizeScale}`);
```

##### setLanguage 设置应用的语言

```
  AppUtil.setLanguage('zh-cn');
```

##### getLanguage 获取应用的语言

```
 let language = AppUtil.getLanguage();
 ToastUtil.showToast(`应用的语言:${language}`);
```

##### setSupportedProcessCache 设置应用自身是否支持缓存后快速启动

```
  AppUtil.setSupportedProcessCache(true);
```

##### clearUpApplicationData 清理应用本身的数据，同时撤销应用向用户申请的权限

```
DialogHelper.showAlertDialog({
  content: '是否清理应用本身的数据？',
  primaryButton:'取消',
  secondaryButton:'清理',
  onAction: (action) => {
    if (action === DialogAction.SURE) {
      AppUtil.clearUpApplicationData();
    }
  }
});
```

##### killAllProcesses 终止应用的所有进程，进程退出时不会正常走完应用生命周期

```
DialogHelper.showAlertDialog({
  content: '是否终止应用的所有进程？',
  primaryButton:'取消',
  secondaryButton:'终止',
  onAction: (action) => {
    if (action === DialogAction.SURE) {
      AppUtil.killAllProcesses();
    }
  }
});
```

##### restartApp 重启应用并拉起自身指定UIAbility。重启时不会收到onDestroy回调

```
DialogHelper.showAlertDialog({
  autoCancel: false,
  backCancel: false,
  content: '是否重启应用？',
  primaryButton:'取消',
  secondaryButton:'重启',
  onAction: (action) => {
    if (action === DialogAction.SURE) {
      AppUtil.restartApp();
    }
  }
});
```

##### exit 主动退出整个应用；调用该方法后，任务中心的任务默认不会清理，如需清理，需要配置removeMissionAfterTerminate为true

```
DialogHelper.showAlertDialog({
  content: '是否重退出应用？',
  primaryButton:'取消',
  secondaryButton:'退出',
  onAction: (action) => {
    if (action === DialogAction.SURE) {
      AppUtil.exit();
    }
  }
});
```

##### getRunningProcessInformation 获取有关运行进程的信息

```
 let processInformation = await AppUtil.getRunningProcessInformation();
```

##### onApplicationStateChange  注册对当前应用前后台变化的监听

```
  private applicationStateChangeCallback: ApplicationStateChangeCallback = {
    onApplicationForeground() {
      LogUtil.warn('applicationStateChangeCallback onApplicationForeground');
    },
    onApplicationBackground() {
      LogUtil.warn('applicationStateChangeCallback onApplicationBackground');
    }
  };
  
  AppUtil.onApplicationStateChange(this.applicationStateChangeCallback);
```

##### offApplicationStateChange 取消对应用前后台切换事件的监听

```
 AppUtil.offApplicationStateChange(this.applicationStateChangeCallback);
```

##### onEnvironment 注册对系统环境变化的监听

```
  private environmentCallback: EnvironmentCallback = {
    onConfigurationUpdated(config) {
      LogUtil.warn(`onConfigurationUpdated config:\n${JSON.stringify(config, null)}`);
    },
    onMemoryLevel(level) {
      LogUtil.warn(`onMemoryLevel level: ${level}`);
    }
  };
  
  this.callback1 = AppUtil.onEnvironment(this.environmentCallback);
```

##### offEnvironment 取消对系统环境变化的监听

```
  AppUtil.offEnvironment(this.callback1);
```

##### onAbilityLifecycle 注册监听应用内生命周期

```
 private abilityLifecycleCallback: AbilityLifecycleCallback = {
    onAbilityCreate(ability) {
      LogUtil.info(`AbilityLifecycleCallback onAbilityCreate ability: ${ability}`);
    },
    onWindowStageCreate(ability, windowStage) {
      LogUtil.info(`AbilityLifecycleCallback onWindowStageCreate ability: ${ability}`);
      LogUtil.info(`AbilityLifecycleCallback onWindowStageCreate windowStage: ${windowStage}`);
    },
    onWindowStageActive(ability, windowStage) {
      LogUtil.info(`AbilityLifecycleCallback onWindowStageActive ability: ${ability}`);
      LogUtil.info(`AbilityLifecycleCallback onWindowStageActive windowStage: ${windowStage}`);
    },
    onWindowStageInactive(ability, windowStage) {
      LogUtil.info(`AbilityLifecycleCallback onWindowStageInactive ability: ${ability}`);
      LogUtil.info(`AbilityLifecycleCallback onWindowStageInactive windowStage: ${windowStage}`);
    },
    onWindowStageDestroy(ability, windowStage) {
      LogUtil.info(`AbilityLifecycleCallback onWindowStageDestroy ability: ${ability}`);
      LogUtil.info(`AbilityLifecycleCallback onWindowStageDestroy windowStage: ${windowStage}`);
    },
    onAbilityDestroy(ability) {
      LogUtil.info(`AbilityLifecycleCallback onAbilityDestroy ability: ${ability}`);
    },
    onAbilityForeground(ability) {
      LogUtil.info(`AbilityLifecycleCallback onAbilityForeground ability: ${ability}`);
    },
    onAbilityBackground(ability) {
      LogUtil.info(`AbilityLifecycleCallback onAbilityBackground ability: ${ability}`);
    },
    onAbilityContinue(ability) {
      LogUtil.info(`AbilityLifecycleCallback onAbilityContinue ability: ${ability}`);
    }
  };
  
  this.callback2 = AppUtil.onAbilityLifecycle(this.abilityLifecycleCallback);
```

##### offAbilityLifecycle 取消监听应用内生命周期

```
 AppUtil.offAbilityLifecycle(this.callback2);
```

##### getKeyboardAvoidMode 获取虚拟键盘抬起时的页面避让模式（OFFSET-上抬模式、RESIZE-压缩模式）

```
 let mode = AppUtil.getKeyboardAvoidMode();
```

##### setKeyboardAvoidMode 设置虚拟键盘弹出时，页面的避让模式

```
 AppUtil.setKeyboardAvoidMode(KeyboardAvoidMode.OFFSET)
```

##### isPortrait 当前设备是否以竖屏方式显示

```
 let isPortrait = AppUtil.isPortrait();
 ToastUtil.showToast(`当前是否竖屏: ${isPortrait}`);
```

##### isLandscape 当前设备是否以横屏方式显示

```
  let isLandscape = AppUtil.isLandscape();
  ToastUtil.showToast(`当前是否横屏: ${isLandscape}`);
```

##### getStatusBarHeight 获取状态栏的高度，单位为px

```
 let statusBarHeight = AppUtil.getStatusBarHeight();
 ToastUtil.showToast(`状态栏的高度为：${statusBarHeight}px`)
```

##### getNavigationIndicatorHeight 获取底部导航条的高度，单位为px

```
 let indicatorHeight = AppUtil.getNavigationIndicatorHeight();
 ToastUtil.showToast(`底部导航条的高度为：${indicatorHeight}px`)
```

##### setStatusBar 设置沉浸式状态栏

```
  AppUtil.setStatusBar();
```

##### getBundleInfo 获取当前应用的BundleInfo

```
 let bundleInfo = AppUtil.getAppInfoSync();
 let infoStr = JSON.stringify(bundleInfo, null, 2);
```

##### getAppInfo 获取应用程序的配置信息

```
 let appInfo = AppUtil.getAppInfoSync();
 let infoStr = JSON.stringify(appInfo, null, 2);
```

##### getSignatureInfo 获取应用包的签名信息

```
 let signatureInfo = await AppUtil.getSignatureInfo();
 let infoStr = JSON.stringify(signatureInfo, null, 2);
```

##### getBundleName 获取应用包的名称

```
 let bundleName = AppUtil.getBundleName();
```

##### getVersionCode 获取应用版本号

```
 let versionCode = AppUtil.getVersionCode();
```

##### getVersionName 获取应用版本名

```
 let versionName = AppUtil.getVersionName();
```

##### getTargetVersion 获取应用运行目标版本

```
  let targetVersion = AppUtil.getTargetVersion();
```

##### getInstallTime 应用包安装时间

```
 let installTime = AppUtil.getInstallTime();
```

##### getUpdateTime 应用包更新时间

```
 let updateTime = AppUtil.getUpdateTime();
```

##### getAppProvisionType 获取应用程序签名证书文件的类型，分为debug和release两种类型

```
 let appProvisionType = AppUtil.getAppProvisionType();
```

##### debug 标识应用是否处于调试模式，取值为true表示应用处于调试模式，取值为false表示应用处于非调试模式

```
 let debug = AppUtil.debug();
```

## 创作不易，请给童长老点赞👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   
