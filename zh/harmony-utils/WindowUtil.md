# harmony-utils之WindowUtil，窗口相关工具类

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

##### setPreferredOrientation  设置窗口的显示方向属性

```
WindowUtil.setPreferredOrientation(window.Orientation.LANDSCAPE).then(() => {
  ToastUtil.showToast(`设置成功！`)
}).catch((err: BusinessError) => {
  LogUtil.error(err);
});
```

##### getPreferredOrientation  获取窗口的显示方向属性，主窗口调用

```
 let orientation = WindowUtil.getPreferredOrientation();
 DialogHelper.showToast(`窗口屏幕方向：${orientation}`);
```

##### setWindowPrivacyMode  设置窗口是否为隐私模式。设置为隐私模式的窗口，窗口内容将无法被截屏或录屏

```
WindowUtil.setWindowPrivacyMode(true).then(() => {
  ToastUtil.showToast("您已设置隐私模式，禁止截屏、录像");
}).catch((err: BusinessError) => {
  LogUtil.error(err);
});
```

##### isPrivacyMode  窗口是否隐私模式，默认主窗口

```
 let isPrivacyMode = WindowUtil.isPrivacyMode();
 ToastUtil.showToast(`窗口是否隐私模式：${isPrivacyMode}`);
```

##### setWindowLayoutFullScreen  设置窗口的布局是否为沉浸式布局（该沉浸式布局状态栏、导航栏仍然显示）

```
WindowUtil.setWindowLayoutFullScreen(true).then(() => {
  ToastUtil.showToast(`沉浸式布局已设置成功！`);
}).catch((err: BusinessError) => {
  LogUtil.error(err);
});
```

##### isLayoutFullScreen  判断窗口是否为沉浸式，默认主窗口

```
 let isLayoutFullScreen = WindowUtil.isLayoutFullScreen();
 ToastUtil.showToast(`窗口是否为沉浸式：${isLayoutFullScreen}`);
```

##### setWindowSystemBarProperties  设置主窗口三键导航栏、状态栏的属性

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

##### getWindowSystemBarProperties  获取主窗口三键导航栏、状态栏的属性

```
   let properties = WindowUtil.getWindowSystemBarProperties();
   let jsonStr = JSON.stringify(properties, null, 2);
```

##### setImmersiveModeEnabledState  设置当前窗口是否开启沉浸式布局，该调用不会改变窗口模式和窗口大小

```
  WindowUtil.setImmersiveModeEnabledState(true);
```

##### getImmersiveModeEnabledState 查询当前窗口是否已经开启沉浸式布局

```
  let enabled = WindowUtil.getImmersiveModeEnabledState();
  ToastUtil.showToast(`是否开启沉浸式布局：${enabled}`);
```

##### setWindowGrayScale  设置窗口灰阶。该接口需要在调用loadContent()或setUIContent()使窗口加载页面内容后调用。

```
 WindowUtil.setWindowGrayScale(1.0);
```

##### setWindowBackgroundColor  设置窗口的背景色。Stage模型下，该接口需要在loadContent()或setUIContent()调用生效后使用

```
  WindowUtil.setWindowBackgroundColor('#9932CC');
  ToastUtil.showToast("设置背景色成功！");
```

##### setWindowSystemBarEnable  设置主窗口三键导航栏、状态栏、底部导航条的可见模式，状态栏与底部导航条通过status控制、三键导航栏通过navigation控制

```
WindowUtil.setWindowSystemBarEnable(['status', 'navigation']).then(() => {
  ToastUtil.showToast(`设置成功！`);
}).catch((err: BusinessError) => {
  LogUtil.error(err);
});
```

##### setSpecificSystemBarEnabled  设置主窗口三键导航栏、状态栏、底部导航条的显示和隐藏

```
WindowUtil.setSpecificSystemBarEnabled('navigationIndicator', true).then(() => {
  ToastUtil.showToast(`设置成功！`);
}).catch((err: BusinessError) => {
  LogUtil.error(err);
});
```

##### setWindowKeepScreenOn  设置屏幕是否为常亮状态

```
WindowUtil.setWindowKeepScreenOn(true).then(() => {
  ToastUtil.showToast("你已设置常亮");
}).catch((err: BusinessError) => {
  LogUtil.error(err);
});
```

##### isKeepScreenOn  屏幕是否常亮

```
 let isKeepScreenOn = WindowUtil.isKeepScreenOn();
 ToastUtil.showToast(`屏幕是否常亮：${isKeepScreenOn}`);
```

##### setWindowBrightness  设置屏幕亮度值

```
WindowUtil.setWindowBrightness(0.7).then(() => {
  ToastUtil.showToast(`您已设置亮度!`);
}).catch((err: BusinessError) => {
  LogUtil.error(`异常信息-code: ${err.code} - msg: ${err.message}`)
});
```

##### getBrightness  获取屏幕亮度。该参数为浮点数，可设置的亮度范围为[0.0, 1.0]，其取1.0时表示最大亮度值。如果窗口没有设置亮度值，表示亮度跟随系统，此时获取到的亮度值为-1

```
 let brightness = WindowUtil.getBrightness();
 ToastUtil.showToast(`屏幕亮度：${brightness}`);
```

##### setWindowFocusable  设置使用点击或其他方式使该窗口获焦的场景时，该窗口是否支持窗口焦点从点击前的获焦窗口切换到该窗口

```
WindowUtil.setWindowFocusable(true).then(() => {
  ToastUtil.showToast("设置成功啦^·^");
}).catch((err: BusinessError) => {
  ToastUtil.showToast("设置失败！");
});
```

##### isFocusable  窗口是否可聚焦，默认主窗口

```
  let isFocusable = WindowUtil.isFocusable();
  ToastUtil.showToast(`窗口是否可聚焦：${isFocusable}`);
```

##### setWindowTouchable  设置窗口是否为可触状态

```
WindowUtil.setWindowTouchable(true).then(() => {
  ToastUtil.showToast("设置成功啦^·^");
}).catch((err: BusinessError) => {
  ToastUtil.showToast("设置失败！");
});
```

##### isTouchable  窗口是否可触摸，默认主窗口

```
  let isTouchable = WindowUtil.isTouchable();
  ToastUtil.showToast(`窗口是否可触摸：${isTouchable}`);
```

##### getWindowProperties  获取当前窗口的属性，默认主窗口

```
 let properties = WindowUtil.getWindowProperties();
 let jsonStr = `${JSON.stringify(properties, null, 2)}`;
```

##### getWindowAvoidArea  获取当前应用窗口内容规避的区域。如系统栏区域、刘海屏区域、手势区域、软键盘区域等与窗口内容重叠时，需要窗口内容避让的区域

```
  let area = WindowUtil.getWindowAvoidArea(window.AvoidAreaType.TYPE_SYSTEM);
  let jsonStr = `${JSON.stringify(area, null, 2)}`;
```

##### getWindowType  获取窗口类型，默认主窗口

```
let windowType = WindowUtil.getWindowType();
```

##### getWindowStatus  获取当前应用窗口的模式

```
let status = WindowUtil.getWindowStatus();
```

##### isFullScreen  判断窗口是否全屏，默认主窗口

```
let isFullScreen = WindowUtil.isFullScreen();
```

##### isFocused  判断当前窗口是否已获焦

```
let isFocused = WindowUtil.isFocused();
```

##### isTransparent 窗口是否透明，默认主窗口

```
let isTransparent = WindowUtil.isTransparent();
```

##### isWindowShowing  判断当前窗口是否已显示，默认主窗口

```
let isWindowShowing = WindowUtil.isWindowShowing();
```

##### isWindowSupportWideGamut  判断当前窗口是否支持广色域模式，，默认主窗口

```
let isWindowSupportWideGamut = await WindowUtil.isWindowSupportWideGamut();
```

##### setDialogBackGestureEnabled  设置模态窗口是否响应手势返回事件，非模态窗口调用返回错误码

```
WindowUtil.setDialogBackGestureEnabled(true).then(() => {
  ToastUtil.showToast("设置成功啦^·^");
}).catch((err: BusinessError) => {
  ToastUtil.showToast("设置失败！");
});
```

##### setGestureBackEnabled  设置当前窗口是否禁用返回手势功能，仅主窗全屏模式下生效，2in1设备下不生效。<API13+>

```
let isGestureBack = WindowUtil.isGestureBackEnabled();
WindowUtil.setGestureBackEnabled(!isGestureBack).then(() => {
  ToastUtil.showToast("设置成功啦^·^");
}).catch((err: BusinessError) => {
  ToastUtil.showToast("设置失败！");
});
```

##### isGestureBackEnabled  获取当前窗口是否禁用返回手势功能，仅主窗全屏模式下生效，2in1设备不生效。<API13+>

```
 let isGestureBack = WindowUtil.isGestureBackEnabled();
 ToastUtil.showToast(`当前窗口是否禁用返回：${isGestureBack}`);
```

## 创作不易，请给童长老点赞👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   

