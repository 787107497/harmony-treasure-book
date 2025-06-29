# DialogUtil, pop-up tool class

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

##### setDefaultConfig Set the default uniform style

```
DialogUtil.setDefaultConfig((config) => {
  config.title = "温馨提示"
  config.subtitle = "弹窗副标题"
  config.alignment = DialogAlignment.Top
  config.borderWidth = 1.2
  config.autoCancel = true
});

DialogUtil.setDefaultConfig((config) => {
  config.title = "友好提示"
  config.alignment = DialogAlignment.Center
  config.borderWidth = 1
  config.borderColor = Color.Blue
});

DialogUtil.setDefaultConfig((config) => {
  config.title = "提示"
  config.alignment = DialogAlignment.Bottom
  config.borderColor = Color.Blue
  config.borderWidth = 0
  config.autoCancel = false
});
```

##### showConfirmDialog displays pop-up window (a button)

```
DialogUtil.showConfirmDialog({
  title: "温馨提示",
  message: 'APP已更新最新版本！',
  confirm: "确定",
  onAction: () => {
    ToastUtil.showToast("点击了“确定”按钮");
  }
});

DialogUtil.showConfirmDialog({
  backCancel: false,
  title: "温馨提示",
  message: 'APP已更新最新版本！',
  confirm: {
    value: "确定",
    action: () => {
      ToastUtil.showToast("点击了“确定”按钮");
    }
  }
});
```

##### showPrimaryDialog display pop-up window (two buttons)

```
DialogUtil.showPrimaryDialog({
  message: '最新版本可提供更多的工具和功能，欢迎下载更新！！！',
  primaryButton: "取消",
  secondaryButton: "更新",
  onAction: (action) => {
    if (action == DialogAction.ONE) {
      ToastUtil.showToast("点击了“取消”按钮");
    } else if (action == DialogAction.TWO) {
      ToastUtil.showToast("点击了“更新”按钮");
    }
  }
});

DialogUtil.showPrimaryDialog({
  title: "温馨提示",
  message: '最新版本可提供更多的工具和功能，欢迎下载更新！',
  primaryButton: {
    value: "取消",
    fontColor: Color.Black,
    action: () => {
      ToastUtil.showToast("点击了“取消”按钮");
    }
  },
  secondaryButton: {
    value: "更新",
    fontColor: Color.Red,
    action: () => {
      ToastUtil.showToast("点击了“更新”按钮");
    }
  },
  onWillDismiss: (dismissDialogAction: DismissDialogAction) => {
    LogUtil.error("onWillDismiss: " + JSON.stringify(dismissDialogAction))
  }
});
```

##### showDialog display pop-up window (multiple buttons)

```
DialogUtil.showDialog({
  title: "温馨提示",
  message: "最新版本可提供更多的工具和功能",
  buttons: ["取消", "稍后", "更新", "升级"],
  onAction: (action) => {
    ToastUtil.showToast(`点击了：${buttons[Math.abs(action)-1]}`);
  }
});

DialogUtil.showDialog({
  title: "温馨提示",
  message: "最新版本可提供更多的工具和功能",
  buttonDirection: DialogButtonDirection.HORIZONTAL,
  buttons: [{
    value: "取消",
    fontColor: Color.Blue,
    action: () => {
      ToastUtil.showToast(`点击了"取消"`);
    }
  }, {
    value: "稍后",
    fontColor: Color.Green,
    action: () => {
      ToastUtil.showToast(`点击了"稍后"`);
    }
  }, {
    value: "更新",
    fontColor: Color.Red,
    action: () => {
      ToastUtil.showToast(`点击了"更新"`);
    }
  }]
});
```

##### showActionSheet list selection pop-up window

```
DialogUtil.showActionSheet({
  message: "请选择",
  sheets: ["功能菜单一", "功能菜单二", "功能菜单三", "功能菜单四", "功能菜单五"],
  onAction: (index) => {
    ToastUtil.showToast("index: " + index);
  }
});
```

##### showCalendarPicker calendar selector pop-up window

```
let date = DateUtil.getToday();
DialogUtil.showCalendarPicker({
  selected: date,
  onAccept: (value) => {
    LogUtil.error(`选择了： ${JSON.stringify(value)}}`);
    ToastUtil.showToast(DateUtil.getFormatDateStr(value, "yyyy年MM月dd日"));
  },
  onCancel: () => {
    ToastUtil.showToast(`取消了`);
  }
});
```

##### showDatePicker DateSliding Selector Popup

```
let date = DateUtil.getToday();
DialogUtil.showDatePicker({
  selected: date,
  showTime: true,
  onDateAccept: (value) => {
    LogUtil.error(`选择了： ${JSON.stringify(value)}}`);
    ToastUtil.showToast(DateUtil.getFormatDateStr(value, "yyyy年MM月dd日 HH:mm"));
  },
  onCancel: () => {
    ToastUtil.showToast(`取消了`);
  }
});
```

##### showTimePicker Time Sliding Selector Popup

```
let date = DateUtil.getToday();
DialogUtil.showTimePicker({
  selected: date,
  format: TimePickerFormat.HOUR_MINUTE,
  useMilitaryTime: true,
  onAccept: (value) => {
    LogUtil.error(`选择了： ${JSON.stringify(value)}}`);
    ToastUtil.showToast(`${value.hour}时${value.minute}分`);
  },
  onCancel: () => {
    ToastUtil.showToast(`取消了`);
  }
});
```

##### showTextPicker Text Sliding Selector Popup

```
private readonly array: string[] = ["黑龙江省", "哈尔滨市", "道里区", "砂山", "砀山", "高薪区"];
@State selectValue: string = '';

DialogUtil.showTextPicker({
  range: array,
  value: this.selectValue,
  onAccept: (result) => {
    LogUtil.error(`选择了： ${JSON.stringify(result)}}`);
    this.selectValue = result.value as string;
    ToastUtil.showToast(`${this.selectValue}`);
  },
  onCancel: () => {
    ToastUtil.showToast(`取消了`);
  }
});
```

## Creation is not easy, please give Elder Tong a thumbs up 👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   


