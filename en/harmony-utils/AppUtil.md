# AppUtil, APP-related tool class

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

##### init initialization method, cache global variables, and initialize the method in UIAbility's onCreate method

```
  onCreate(want: Want, launchParam: AbilityConstant.LaunchParam): void {
    AppUtil.init(this.context);
  }
```

##### isApiSupported Check whether the API version is safe

```
   let bl = AppUtil.isApiSupported(18);
```

##### getApplicationContext Get ApplicationContext

```
   let applicationContext = AppUtil.getApplicationContext();
```

##### getContext Get UIContext

```
   let uiContext = AppUtil.getUIContext();
```

##### getWindowStage Get WindowStage

```
  let windowStage = AppUtil.getWindowStage();
  LogUtil.error(JSON.stringify(windowStage, null, 2));
```

##### getMainWindow Get the main window

```
 let mainWindow = AppUtil.getMainWindow();
```

##### getConfiguration Gets the application's Configuration

```
 let config = AppUtil.getConfiguration();
```

##### setGrayScale sets grayscale, and APP sets grayscale with one click

```
 AppUtil.setGrayScale(1);
```

##### setColorMode Sets the applied color mode. Only main thread calls are supported. Set color mode, including: dark mode, light mode, and no settings (follow the system)

```
  AppUtil.setColorMode(ConfigurationConstant.ColorMode.COLOR_MODE_LIGHT);
```

##### getColorMode Gets the color mode of the application

```
  let colorMode = AppUtil.getColorMode();
  ToastUtil.showToast(`应用的颜色模式:${colorMode}`);
```

##### setFont Sets the font type of the application. Only main thread calls are supported

```
  font.registerFont({ familyName: 'WCSF', familySrc: $rawfile('wcsf.ttf') });
  AppUtil.setFont('WCSF');
```

##### setFontSizeScale Sets the applied font size scaling ratio. Only main thread calls are supported. <API13+>

```
  AppUtil.setFontSizeScale(1.8);
```

##### getFontSizeScale Get the applied font size scaling ratio

```
  let fontSizeScale = AppUtil.getFontSizeScale();
  ToastUtil.showToast(`应用字体大小缩放比例:${fontSizeScale}`);
```

##### setLanguage Sets the language of the application

```
  AppUtil.setLanguage('zh-cn');
```

##### getLanguage Gets the language of the application

```
 let language = AppUtil.getLanguage();
 ToastUtil.showToast(`应用的语言:${language}`);
```

##### setSupportedProcessCache Sets whether the application itself supports cache and starts quickly

```
  AppUtil.setSupportedProcessCache(true);
```

##### clearUpApplicationData cleans up the application's own data and revokes the application's permission to apply to the user.

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

##### killAllProcesses terminates all processes of the application. The application life cycle will not be completed normally when the process exits.

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

##### restartApp Restart the app and pull up its own specified UIAbility. No onDestroy callback is received during restart

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

##### exit voluntarily exits the entire application; after calling this method, the tasks in the task center will not be cleaned by default. If you need to clean it, you need to configure removeMissionAfterTerminate to true

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

##### getRunningProcessInformation Gets information about running the process

```
 let processInformation = await AppUtil.getRunningProcessInformation();
```

##### onApplicationStateChange Register to listen for changes in the front and backend of the current application

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

##### offApplicationStateChange Cancel listening to the application's front and backend switch events

```
 AppUtil.offApplicationStateChange(this.applicationStateChangeCallback);
```

##### onEnvironment Register monitoring of system environment changes

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

##### offEnvironment Cancel monitoring of system environment changes

```
  AppUtil.offEnvironment(this.callback1);
```

##### onAbilityLifecycle Register to listen for in-app lifecycle

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

##### offAbilityLifecycle Cancel the in-app lifecycle

```
 AppUtil.offAbilityLifecycle(this.callback2);
```

##### getKeyboardAvoidMode Gets the page avoidance mode when virtual keyboard is lifted (OFFSET-up mode, RESIZE-compression mode)

```
 let mode = AppUtil.getKeyboardAvoidMode();
```

##### setKeyboardAvoidMode Sets the avoidance mode of the page when the virtual keyboard pops up

```
 AppUtil.setKeyboardAvoidMode(KeyboardAvoidMode.OFFSET)
```

##### isPortrait Whether the current device is displayed in a vertical screen

```
 let isPortrait = AppUtil.isPortrait();
 ToastUtil.showToast(`当前是否竖屏: ${isPortrait}`);
```

##### isLandscape Whether the current device is displayed in landscape mode

```
  let isLandscape = AppUtil.isLandscape();
  ToastUtil.showToast(`当前是否横屏: ${isLandscape}`);
```

##### getStatusBarHeight Gets the height of the status bar in px

```
 let statusBarHeight = AppUtil.getStatusBarHeight();
 ToastUtil.showToast(`状态栏的高度为：${statusBarHeight}px`)
```

##### getNavigationIndicatorHeight Get the height of the bottom navigation bar in px

```
 let indicatorHeight = AppUtil.getNavigationIndicatorHeight();
 ToastUtil.showToast(`底部导航条的高度为：${indicatorHeight}px`)
```

##### setStatusBar Set the immersive status bar

```
  AppUtil.setStatusBar();
```

##### getBundleInfo Get the BundleInfo of the current application

```
 let bundleInfo = AppUtil.getAppInfoSync();
 let infoStr = JSON.stringify(bundleInfo, null, 2);
```

##### getAppInfo Get the configuration information of the application

```
 let appInfo = AppUtil.getAppInfoSync();
 let infoStr = JSON.stringify(appInfo, null, 2);
```

##### getSignatureInfo Get the signature information of the application package

```
 let signatureInfo = await AppUtil.getSignatureInfo();
 let infoStr = JSON.stringify(signatureInfo, null, 2);
```

##### getBundleName Gets the name of the application package

```
 let bundleName = AppUtil.getBundleName();
```

##### getVersionCode Get the application version number

```
 let versionCode = AppUtil.getVersionCode();
```

##### getVersionName Get the application version name

```
 let versionName = AppUtil.getVersionName();
```

##### getTargetVersion Get the target version of the application running

```
  let targetVersion = AppUtil.getTargetVersion();
```

##### getInstallTime application package installation time

```
 let installTime = AppUtil.getInstallTime();
```

##### getUpdateTime application package update time

```
 let updateTime = AppUtil.getUpdateTime();
```

##### getAppProvisionType Gets the type of application signature certificate file, divided into two types: debug and release

```
 let appProvisionType = AppUtil.getAppProvisionType();
```

##### debug indicates whether the application is in debug mode. The value of true means the application is in debug mode. The value of false means the application is in non-debug mode.

```
 let debug = AppUtil.debug();
```

## Creation is not easy, please give Elder Tong a thumbs up 👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   
