# WindowUtil, window-related tool class

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

##### setPreferredOrientation Sets the display orientation properties of the window

```
WindowUtil.setPreferredOrientation(window.Orientation.LANDSCAPE).then(() => {
  ToastUtil.showToast(`设置成功！`)
}).catch((err: BusinessError) => {
  LogUtil.error(err);
});
```

##### getPreferredOrientation Gets the display direction property of the window, and calls the main window

```
 let orientation = WindowUtil.getPreferredOrientation();
 DialogHelper.showToast(`窗口屏幕方向：${orientation}`);
```

##### setWindowPrivacyMode Sets whether the window is in Privacy Mode. A window set to privacy mode will not be screenshot or recorded.

```
WindowUtil.setWindowPrivacyMode(true).then(() => {
  ToastUtil.showToast("您已设置隐私模式，禁止截屏、录像");
}).catch((err: BusinessError) => {
  LogUtil.error(err);
});
```

##### Is the isPrivacyMode window private mode? The default main window

```
 let isPrivacyMode = WindowUtil.isPrivacyMode();
 ToastUtil.showToast(`窗口是否隐私模式：${isPrivacyMode}`);
```

##### setWindowLayoutFullScreen Sets whether the layout of the window is an immersive layout (the status bar and navigation bar of the immersive layout are still displayed)

```
WindowUtil.setWindowLayoutFullScreen(true).then(() => {
  ToastUtil.showToast(`沉浸式布局已设置成功！`);
}).catch((err: BusinessError) => {
  LogUtil.error(err);
});
```

##### isLayoutFullScreen determines whether the window is immersive, the default main window

```
 let isLayoutFullScreen = WindowUtil.isLayoutFullScreen();
 ToastUtil.showToast(`窗口是否为沉浸式：${isLayoutFullScreen}`);
```

##### setWindowSystemBarProperties Set the properties of the main window three-key navigation bar and status bar

```
WindowUtil.setWindowSystemBarProperties({
  statusBarColor: '#F00FF0',
  statusBarContentColor: '#0FF00F',
  isStatusBarLightIcon: true,
  navigationBarColor: '#F06060',
  navigationBarContentColor: "#0606F0",
  isNavigationBarLightIcon: true
}).then(() => {
  ToastUtil.showToast("设置成功！");
}).catch((err: BusinessError) => {
  LogUtil.error(err);
});
```

##### getWindowSystemBarProperties Get the properties of the three-key navigation bar and status bar in the main window

```
   let properties = WindowUtil.getWindowSystemBarProperties();
   let jsonStr = JSON.stringify(properties, null, 2);
```

##### setImmersiveModeEnabledState Sets whether the current window is turned on to immersive layout. This call will not change the window mode and window size.

```
  WindowUtil.setImmersiveModeEnabledState(true);
```

##### getImmersiveModeEnabledState Check whether the current window has an immersive layout enabled

```
  let enabled = WindowUtil.getImmersiveModeEnabledState();
  ToastUtil.showToast(`是否开启沉浸式布局：${enabled}`);
```

##### setWindowGrayScale Sets the window grayscale. This interface needs to be called after calling loadContent() or setUIContent() to make the window load the page content.

```
 WindowUtil.setWindowGrayScale(1.0);
```

##### setWindowBackgroundColor Sets the background color of the window. Under the Stage model, this interface needs to be used after the loadContent() or setUIContent() call takes effect.

```
  WindowUtil.setWindowBackgroundColor('#9932CC');
  ToastUtil.showToast("设置背景色成功！");
```

##### setWindowSystemBarEnable Sets the visible mode of the three-key navigation bar, status bar, and bottom navigation bar in the main window. The status bar and bottom navigation bar are controlled through status bar and three-key navigation bar are controlled through navigation bar.

```
WindowUtil.setWindowSystemBarEnable(['status', 'navigation']).then(() => {
  ToastUtil.showToast(`设置成功！`);
}).catch((err: BusinessError) => {
  LogUtil.error(err);
});
```

##### setSpecificSystemBarEnabled Sets the display and hide of the three-key navigation bar, status bar, and bottom navigation bar in the main window

```
WindowUtil.setSpecificSystemBarEnabled('navigationIndicator', true).then(() => {
  ToastUtil.showToast(`设置成功！`);
}).catch((err: BusinessError) => {
  LogUtil.error(err);
});
```

##### setWindowKeepScreenOn Sets whether the screen is always on

```
WindowUtil.setWindowKeepScreenOn(true).then(() => {
  ToastUtil.showToast("你已设置常亮");
}).catch((err: BusinessError) => {
  LogUtil.error(err);
});
```

##### isKeepScreenOn Whether the screen is always on

```
 let isKeepScreenOn = WindowUtil.isKeepScreenOn();
 ToastUtil.showToast(`屏幕是否常亮：${isKeepScreenOn}`);
```

##### setWindowBrightness Sets the screen brightness value

```
WindowUtil.setWindowBrightness(0.7).then(() => {
  ToastUtil.showToast(`您已设置亮度!`);
}).catch((err: BusinessError) => {
  LogUtil.error(`异常信息-code: ${err.code} - msg: ${err.message}`)
});
```

##### getBrightness Gets the screen brightness. This parameter is a floating point number, and the brightness range that can be set is [0.0, 1.0], which indicates the maximum brightness value when taken 1.0. If the window does not have a brightness value set, it means that the brightness follows the system. The brightness value obtained at this time is -1

```
 let brightness = WindowUtil.getBrightness();
 ToastUtil.showToast(`屏幕亮度：${brightness}`);
```

##### setWindowFocusable Sets the scene where the window is focused using clicks or other methods, whether the window supports switching the window focus from the focus window before clicking to the window

```
WindowUtil.setWindowFocusable(true).then(() => {
  ToastUtil.showToast("设置成功啦^·^");
}).catch((err: BusinessError) => {
  ToastUtil.showToast("设置失败！");
});
```

##### Is the isFocusable window focused? The default main window

```
  let isFocusable = WindowUtil.isFocusable();
  ToastUtil.showToast(`窗口是否可聚焦：${isFocusable}`);
```

##### setWindowTouchable Set whether the window is touchable

```
WindowUtil.setWindowTouchable(true).then(() => {
  ToastUtil.showToast("设置成功啦^·^");
}).catch((err: BusinessError) => {
  ToastUtil.showToast("设置失败！");
});
```

##### Is the isTouchable window touchable? The default main window

```
  let isTouchable = WindowUtil.isTouchable();
  ToastUtil.showToast(`窗口是否可触摸：${isTouchable}`);
```

##### getWindowProperties Get the properties of the current window, the default main window

```
 let properties = WindowUtil.getWindowProperties();
 let jsonStr = `${JSON.stringify(properties, null, 2)}`;
```

##### getWindowAvoidArea Gets the area to which the content of the current application window is evaded. If the system bar area, notch screen area, gesture area, soft keyboard area, etc. overlap with the window content, the window content needs to be avoided.

```
  let area = WindowUtil.getWindowAvoidArea(window.AvoidAreaType.TYPE_SYSTEM);
  let jsonStr = `${JSON.stringify(area, null, 2)}`;
```

##### getWindowType Gets the window type, default main window

```
let windowType = WindowUtil.getWindowType();
```

##### getWindowStatus Get the mode of the current application window

```
let status = WindowUtil.getWindowStatus();
```

##### isFullScreen determines whether the window is full screen, the default main window

```
let isFullScreen = WindowUtil.isFullScreen();
```

##### isFocused determines whether the current window has been focused

```
let isFocused = WindowUtil.isFocused();
```

##### Is the isTransparent window transparent? The default main window

```
let isTransparent = WindowUtil.isTransparent();
```

##### isWindowShowing determines whether the current window has been displayed, the default main window

```
let isWindowShowing = WindowUtil.isWindowShowing();
```

##### isWindowSupportWideGamut determines whether the current window supports wide color gamut mode, the default main window

```
let isWindowSupportWideGamut = await WindowUtil.isWindowSupportWideGamut();
```

##### setDialogBackGestureEnabled Sets whether the modal window responds to gestures and returns an error code when calling non-modal windows

```
WindowUtil.setDialogBackGestureEnabled(true).then(() => {
  ToastUtil.showToast("设置成功啦^·^");
}).catch((err: BusinessError) => {
  ToastUtil.showToast("设置失败！");
});
```

##### setGestureBackEnabled Sets whether the return gesture function is disabled in the current window. It only takes effect in full screen mode of the main window, and does not take effect in 2in1 device. <API13+>

```
let isGestureBack = WindowUtil.isGestureBackEnabled();
WindowUtil.setGestureBackEnabled(!isGestureBack).then(() => {
  ToastUtil.showToast("设置成功啦^·^");
}).catch((err: BusinessError) => {
  ToastUtil.showToast("设置失败！");
});
```

##### isGestureBackEnabled Gets whether the return gesture function is disabled in the current window. It only takes effect in full screen mode of the main window, and the 2in1 device does not take effect. <API13+>

```
 let isGestureBack = WindowUtil.isGestureBackEnabled();
 ToastUtil.showToast(`当前窗口是否禁用返回：${isGestureBack}`);
```

## Creation is not easy, please give Elder Tong a thumbs up 👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   

