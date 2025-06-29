# harmony-utils: DisplayUtil, screen related tool class

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

##### getDefaultDisplaySync Gets the current default display object

```
 let display = DisplayUtil.getDefaultDisplaySync();
 let displayStr = JSON.stringify(display, null, 2);
```

##### getPrimaryDisplaySync Get home screen information. Devices other than 2in1 obtain the Display object with the device's own screen; when the 2in1 device connects to the external screen, it obtains the Display object with the current home screen; when the 2in1 device does not have an external screen, it obtains the Display object with the screen. <API14+>

```
 let display = DisplayUtil.getPrimaryDisplaySync();
 let displayStr = JSON.stringify(display, null, 2);
```

##### getAllDisplays Get all current display objects and use Promise asynchronous callback

```
  let allDisplay = await DisplayUtil.getAllDisplays();
  let displayStr = JSON.stringify(allDisplay, null, 2);
```

##### getWidth Gets the screen width of the device in px

```
 let width = DisplayUtil.getWidth();
 ToastUtil.showToast(`当前屏幕宽度为：${width}px`);
```

##### getHeight Get the screen height of the device in px

```
 let height = DisplayUtil.getHeight();
 ToastUtil.showToast(`当前屏幕宽高度：${height}px`);
```

##### getOrientation Gets the current display direction of the device

```
 let orientation = DisplayUtil.getOrientation();
 ToastUtil.showToast(`设备当前显示的方向：${orientation}`);
```

##### getDisplayState Gets the status of the device

```
 let state = DisplayUtil.getDisplayState();
 ToastUtil.showToast(`当前设备的状态：${state}`);
```

##### getCutoutRect Get information on unavailable screen areas such as hole-punch screen, notch screen, and waterfall screen. It is recommended to use layout to avoid this area

```
 let rect = await DisplayUtil.getCutoutRect();
 let cutoutInfoStr = JSON.stringify(rect, null, 2);
```

##### getCutoutHeight Get the height of the unavailable screen area such as hole-punch screen, notch screen, etc., in px

```
 let h = await DisplayUtil.getCutoutHeight();
 ToastUtil.showToast(`挖孔屏、刘海屏等不可用屏幕区域的高度：${h}`);
```

##### isFoldable Check if the device is foldable

```
 let bl = DisplayUtil.isFoldable();
 ToastUtil.showToast(`设备是否可折叠：${bl}`);
```

##### getFoldStatus Gets the current folding status of the foldable device

```
 let status = DisplayUtil.getFoldStatus();
 ToastUtil.showToast(`折叠设备的当前折叠状态：${status}`);
```

##### getFoldDisplayMode Gets the display mode of the foldable device

```
  let mode = DisplayUtil.getFoldDisplayMode();
  ToastUtil.showToast(`可折叠设备的显示模式：${mode}`);
```

##### onFoldStatusChange enables monitoring of folding state changes in folding device

```
ToastUtil.showToast("开启折叠设备折叠状态变化的监听");
DisplayUtil.onFoldStatusChange((foldStatus: display.FoldStatus) => {
  let foldStatusStr = JSON.stringify(foldStatus, null, 2);
});
```

##### offFoldStatusChange Turn off monitoring of folding state changes in folding device

```
 ToastUtil.showToast("关闭折叠设备折叠状态变化的监听");
 DisplayUtil.offFoldStatusChange();
```

##### onFoldAngleChange Turns on monitoring of folding angle changes in folding device. If it is a bifold shaft device, there are two angle values; when the charging port is facing downward, the folding shaft one and folding shaft two are respectively from right to left.

```
ToastUtil.showToast("开启折叠设备折叠角度变化的监听");
DisplayUtil.onFoldAngleChange((angles: Array<number>) => {
  LogUtil.info(`折叠角度变化的监听：${angles}`);
  ToastUtil.showLong(`折叠角度变化的监听：${angles}`);
});
```

##### offFoldAngleChange Turn off monitoring of folding angle changes in folding device

```
 ToastUtil.showToast("关闭折叠设备折叠角度变化的监听");
 DisplayUtil.offFoldAngleChange();
```

##### isCapture Check whether the device is taking screenshots, projecting, and recording screens.

```
 let isCaptured = DisplayUtil.isCaptured();
 ToastUtil.showToast(`设备是否正在截屏、投屏、录屏：${isCaptured}`);
```

##### onCaptureStatusChange enables monitoring of screenshots, projections, and recording status changes

```
ToastUtil.showToast("开启屏幕截屏、投屏、录屏状态变化的监听");
DisplayUtil.onCaptureStatusChange((captureStatus: boolean) => {
  LogUtil.info(`屏幕截屏、投屏、录屏状态：${captureStatus}`);
  ToastUtil.showLong(`屏幕截屏、投屏、录屏状态：${captureStatus}`);
});
```

##### offCaptureStatusChange Close monitoring of changes in screen capture, projection, and recording status

```
 ToastUtil.showToast("关闭屏幕截屏、投屏、录屏状态变化的监听");
 DisplayUtil.offCaptureStatusChange();
```

## Creation is not easy, please give Elder Tong a thumbs up 👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   



