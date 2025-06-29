# harmony-utils之DialogUtil，弹窗工具类

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

##### setDefaultConfig  设置默认统一样式

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

##### showConfirmDialog  显示弹窗（一个按钮）

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

##### showPrimaryDialog  显示弹窗（两个按钮）

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

##### showDialog  显示弹窗（可多个按钮）

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

##### showActionSheet  列表选择弹窗

```
DialogUtil.showActionSheet({
  message: "请选择",
  sheets: ["功能菜单一", "功能菜单二", "功能菜单三", "功能菜单四", "功能菜单五"],
  onAction: (index) => {
    ToastUtil.showToast("index: " + index);
  }
});
```

##### showCalendarPicker  日历选择器弹窗

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

##### showDatePicker  日期滑动选择器弹窗

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

##### showTimePicker  时间滑动选择器弹窗

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

##### showTextPicker  文本滑动选择器弹窗

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

## 创作不易，请给童长老点赞👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   


