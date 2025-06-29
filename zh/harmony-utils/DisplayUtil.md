# harmony-utils之DisplayUtil，屏幕相关工具类

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

##### getDefaultDisplaySync  获取当前默认的display对象

```
 let display = DisplayUtil.getDefaultDisplaySync();
 let displayStr = JSON.stringify(display, null, 2);
```

##### getPrimaryDisplaySync  获取主屏信息。除2in1之外的设备获取的是设备自带屏幕的Display对象；2in1设备外接屏幕时获取的是当前主屏幕的Display对象；2in1设备没有外接屏幕时获取的是自带屏幕的Display对象。<API14+>

```
 let display = DisplayUtil.getPrimaryDisplaySync();
 let displayStr = JSON.stringify(display, null, 2);
```

##### getAllDisplays  获取当前所有的display对象，使用Promise异步回调

```
  let allDisplay = await DisplayUtil.getAllDisplays();
  let displayStr = JSON.stringify(allDisplay, null, 2);
```

##### getWidth  获取设备的屏幕宽度，单位为px

```
 let width = DisplayUtil.getWidth();
 ToastUtil.showToast(`当前屏幕宽度为：${width}px`);
```

##### getHeight  获取设备的屏幕高度，单位为px

```
 let height = DisplayUtil.getHeight();
 ToastUtil.showToast(`当前屏幕宽高度：${height}px`);
```

##### getOrientation  获取设备当前显示的方向

```
 let orientation = DisplayUtil.getOrientation();
 ToastUtil.showToast(`设备当前显示的方向：${orientation}`);
```

##### getDisplayState  获取设备的状态

```
 let state = DisplayUtil.getDisplayState();
 ToastUtil.showToast(`当前设备的状态：${state}`);
```

##### getCutoutRect  获取取挖孔屏、刘海屏、瀑布屏等不可用屏幕区域信息。建议应用布局规避该区域

```
 let rect = await DisplayUtil.getCutoutRect();
 let cutoutInfoStr = JSON.stringify(rect, null, 2);
```

##### getCutoutHeight  获取挖孔屏、刘海屏等不可用屏幕区域的高度，单位为px

```
 let h = await DisplayUtil.getCutoutHeight();
 ToastUtil.showToast(`挖孔屏、刘海屏等不可用屏幕区域的高度：${h}`);
```

##### isFoldable  检查设备是否可折叠

```
 let bl = DisplayUtil.isFoldable();
 ToastUtil.showToast(`设备是否可折叠：${bl}`);
```

##### getFoldStatus  获取可折叠设备的当前折叠状态

```
 let status = DisplayUtil.getFoldStatus();
 ToastUtil.showToast(`折叠设备的当前折叠状态：${status}`);
```

##### getFoldDisplayMode  获取可折叠设备的显示模式

```
  let mode = DisplayUtil.getFoldDisplayMode();
  ToastUtil.showToast(`可折叠设备的显示模式：${mode}`);
```

##### onFoldStatusChange  开启折叠设备折叠状态变化的监听

```
ToastUtil.showToast("开启折叠设备折叠状态变化的监听");
DisplayUtil.onFoldStatusChange((foldStatus: display.FoldStatus) => {
  let foldStatusStr = JSON.stringify(foldStatus, null, 2);
});
```

##### offFoldStatusChange  关闭折叠设备折叠状态变化的监听

```
 ToastUtil.showToast("关闭折叠设备折叠状态变化的监听");
 DisplayUtil.offFoldStatusChange();
```

##### onFoldAngleChange  开启折叠设备折叠角度变化的监听。如果是双折轴设备，则有两个角度值；在充电口朝下的状态下，从右到左分别是折轴一和折轴二。

```
ToastUtil.showToast("开启折叠设备折叠角度变化的监听");
DisplayUtil.onFoldAngleChange((angles: Array<number>) => {
  LogUtil.info(`折叠角度变化的监听：${angles}`);
  ToastUtil.showLong(`折叠角度变化的监听：${angles}`);
});
```

##### offFoldAngleChange  关闭折叠设备折叠角度变化的监听

```
 ToastUtil.showToast("关闭折叠设备折叠角度变化的监听");
 DisplayUtil.offFoldAngleChange();
```

##### isCaptured  检查设备是否正在截屏、投屏、录屏

```
 let isCaptured = DisplayUtil.isCaptured();
 ToastUtil.showToast(`设备是否正在截屏、投屏、录屏：${isCaptured}`);
```

##### onCaptureStatusChange  开启屏幕截屏、投屏、录屏状态变化的监听

```
ToastUtil.showToast("开启屏幕截屏、投屏、录屏状态变化的监听");
DisplayUtil.onCaptureStatusChange((captureStatus: boolean) => {
  LogUtil.info(`屏幕截屏、投屏、录屏状态：${captureStatus}`);
  ToastUtil.showLong(`屏幕截屏、投屏、录屏状态：${captureStatus}`);
});
```

##### offCaptureStatusChange  关闭屏幕截屏、投屏、录屏状态变化的监听

```
 ToastUtil.showToast("关闭屏幕截屏、投屏、录屏状态变化的监听");
 DisplayUtil.offCaptureStatusChange();
```

## 创作不易，请给童长老点赞👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   



