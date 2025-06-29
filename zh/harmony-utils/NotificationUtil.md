# harmony-utils之NotificationUtil，通知工具类

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

##### setDefaultConfig  设置通知的默认统一配置

```
let wantAgent = await NotificationUtil.getDefaultWantAgent();
let smallIcon = await NotificationUtil.getCompressedIcon($r('app.media.test_as5'));
let largeIcon = await NotificationUtil.getCompressedIcon($r('app.media.test_as1'));
let lPicture = await NotificationUtil.getCompressedPicture($r("app.media.test_as1"));

NotificationUtil.setDefaultConfig((config) => {
  config.wantAgent = wantAgent
  config.removalWantAgent = wantAgent
  config.smallIcon = smallIcon
  config.largeIcon = largeIcon
  config.isFloatingIcon = true
  config.tapDismissed = true
  config.additionalText = "默认的统一配置"
  config.lockscreenPicture = lPicture
})
```

##### isNotificationEnabled  查询通知是否授权

```
let isEnabled = await NotificationUtil.isNotificationEnabled();
ToastUtil.showToast(`查询通知是否授权: ${isEnabled}`);
```

##### authorizeNotification  请求通知授权，第一次调用会弹窗让用户选择。

```
NotificationUtil.authorizeNotification((grant) => {
  ToastUtil.showToast(`授权通知服务: ${grant ? '成功' : '失败'}`);
  if (!grant) {
    WantUtil.toNotificationSetting(); //跳转通知设置页面
  }
});
```

##### isSupportTemplate   查询模板是否存在，目前仅支持进度条模板。

```
let blTemplate = await NotificationUtil.isSupportTemplate();
ToastUtil.showToast(`查询模板是否存在: ${blTemplate}`);
```

##### isDistributedEnabled  查询设备是否支持分布式通知

```
let blDistributedEnabled = await NotificationUtil.isDistributedEnabled();
ToastUtil.showToast(`查询设备是否支持分布式通知: ${blDistributedEnabled}`);
```

##### publishBasic  发布普通文本通知

```
let wantAgent = await NotificationUtil.getDefaultWantAgent();
let id = NotificationUtil.generateNotificationId(); //通知id
let basicOptions: NotificationBasicOptions = {
  id: id,
  title: "鸿蒙工具包",
  text: "HarmonyOS工具包，封装了常用工具类，提供一系列简单易用的方法。帮助开发者快速构建鸿蒙应用",
  wantAgent: wantAgent
}
NotificationUtil.publishBasic(basicOptions).then((id) => {
  ToastUtil.showToast(`通知发送成功，id为：${id}`);
  this.notificationIds.push(id);
}).catch((err: BusinessError) => {
  ToastUtil.showToast(`通知发送失败，${err.message}`);
});
```

##### publishMultiLine  发布多文本通知

```
let multiLineOptions: NotificationMultiLineOptions = {
  title: "鸿蒙工具包",
  text: "HarmonyOS工具包，封装了常用工具类，提供一系列简单易用的方法。帮助开发者快速构建鸿蒙应用",
  briefText: "222222222222222222222222222222222",
  longTitle: "HarmonyOS工具包",
  lines: ["帮助初学者了解API", "封装了常用工具类", "提供一系列简单易用的方法",
    "帮助开发者快速构建鸿蒙应用"]
}
NotificationUtil.publishMultiLine(multiLineOptions).then((id) => {
  ToastUtil.showToast(`通知发送成功，id为：${id}`);
  this.notificationIds.push(id);
}).catch((err: BusinessError) => {
  ToastUtil.showToast(`通知发送失败，${err.message}`);
});
```

##### publishLongText  发布长文本通知

```
NotificationUtil.publishLongText({
  title: "鸿蒙工具包",
  text: "HarmonyOS工具包，封装了常用工具类，提供一系列简单易用的方法。帮助开发者快速构建鸿蒙应用",
  longText: "harmony-utils 一款高效的OpenHarmony/HarmonyOS工具包，封装了常用工具类，提供一系列简单易用的方法。帮助初学者了解API，帮助开发者快速构建鸿蒙应用",
  briefText: "111111111111111111111111111111111111111111",
  expandedTitle: "OpenHarmony/HarmonyOS工具包",
}).then((id) => {
  ToastUtil.showToast(`通知发送成功，id为：${id}`);
  this.notificationIds.push(id);
}).catch((err: BusinessError) => {
  ToastUtil.showToast(`通知发送失败，${err.message}`);
});
```

##### publishPicture  发布带有图片的通知

```
let media = await ImageUtil.getPixelMapFromMedia($r('app.media.test_as5'));
let pixelMap = await NotificationUtil.getCompressedPicture(media);
LogUtil.error("图片大小3：" + (pixelMap.getPixelBytesNumber() / 1024))
NotificationUtil.publishPicture({
  title: "鸿蒙工具包",
  text: "HarmonyOS工具包，封装了常用工具类。帮助开发者快速构建鸿蒙应用",
  briefText: "33333333333333333333333333333333",
  expandedTitle: "OpenHarmony/HarmonyOS工具包",
  picture: pixelMap
}).then((id) => {
  ToastUtil.showToast(`通知发送成功，id为：${id}`);
  this.notificationIds.push(id);
}).catch((err: BusinessError) => {
  ToastUtil.showToast(`通知发送失败，${err.message}`);
});
```

##### publishTemplate  发布模板通知

```
NotificationUtil.publishTemplate({
  title: "鸿蒙工具包",
  text: "HarmonyOS工具包，封装了常用工具类，提供一系列简单易用的方法。帮助开发者快速构建鸿蒙应用",
  fileName: "测试图片.mp4",
  progressValue: 72,
}).then((id) => {
  ToastUtil.showToast(`通知发送成功，id为：${id}`);
  this.notificationIds.push(id);
}).catch((err: BusinessError) => {
  ToastUtil.showToast(`通知发送失败，${err.message}`);
});
```

##### cancel  取消通知

```
NotificationUtil.cancel(1);
```

##### cancelGroup  取消本应用指定组下的通知

```
NotificationUtil.cancelGroup("group_msg");
```

##### cancelAll  取消所有通知

```
NotificationUtil.cancelAll();
ToastUtil.showToast(`取消所有通知，成功！`);
```

##### setBadge  设置桌面角标个数

```
NotificationUtil.setBadge(96);
```

##### clearBadge  清空桌面角标

```
NotificationUtil.clearBadge();
```

##### setBadgeFromNotificationCount  设置桌面角标数量，来自于通知数量

```
NotificationUtil.setBadgeFromNotificationCount().then(() => {
  ToastUtil.showToast("设置角标成功");
}).catch((err: BusinessError) => {
  ToastUtil.showToast("设置角标失败，" + NotificationUtil.getErrorMsg(err.code, err.message));
  LogUtil.error(`设置角标异常：${NotificationUtil.getErrorMsg(err.code, err.code + " - " + err.message)}`);
});
```

##### getActiveNotificationCount  获取当前应用未删除的通知数量

```
let count = await NotificationUtil.getActiveNotificationCount();
ToastUtil.showToast(`当前通知数量为：${count}`);
```

##### getActiveNotifications  获取当前应用未删除的通知列表

```
 let notifications = await NotificationUtil.getActiveNotifications();
```

##### generateNotificationId  生成通知id（用时间戳当id）

```
 let id = NotificationUtil.generateNotificationId(); //通知id
```

##### getDefaultWantAgent  创建一个可拉起Ability的Want

```
let wantAgent = await NotificationUtil.getDefaultWantAgent();
```

##### getCompressedPicture  获取压缩通知的图片（图像像素的总字节数不能超过2MB）

```
let lPicture = await NotificationUtil.getCompressedPicture($r("app.media.test_as1"));
```

##### getCompressedIcon  获取压缩通知图标（图标像素的总字节数不超过192KB）

```
let smallIcon = await NotificationUtil.getCompressedIcon($r('app.media.test_as5'));
let largeIcon = await NotificationUtil.getCompressedIcon($r('app.media.test_as1'));
```

## 创作不易，请给童长老点赞👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   

