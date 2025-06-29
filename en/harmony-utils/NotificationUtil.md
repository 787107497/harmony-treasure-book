# NotificationUtil, notification tool class

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

##### setDefaultConfig Sets the default unified configuration for notifications

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

##### isNotificationEnabled Query whether the notification is authorized

```
let isEnabled = await NotificationUtil.isNotificationEnabled();
ToastUtil.showToast(`查询通知是否授权: ${isEnabled}`);
```

##### authorizeNotification requests notification authorization, and the first call will pop up the window for the user to choose.

```
NotificationUtil.authorizeNotification((grant) => {
  ToastUtil.showToast(`授权通知服务: ${grant ? '成功' : '失败'}`);
  if (!grant) {
    WantUtil.toNotificationSetting(); //跳转通知设置页面
  }
});
```

##### isSupportTemplate Checks whether the template exists, and currently only progress bar templates are supported.

```
let blTemplate = await NotificationUtil.isSupportTemplate();
ToastUtil.showToast(`查询模板是否存在: ${blTemplate}`);
```

##### isDistributedEnabled Query whether the device supports distributed notifications

```
let blDistributedEnabled = await NotificationUtil.isDistributedEnabled();
ToastUtil.showToast(`查询设备是否支持分布式通知: ${blDistributedEnabled}`);
```

##### publishBasic Publish normal text notifications

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

##### publishMultiLine Publish multi-text notifications

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

##### publishLongText Publish long text notification

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

##### publishPicture Publish notifications with pictures

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

##### publishTemplate Publish Template Notification

```
NotificationUtil.publishTemplate({
  title: "鸿蒙工具包",
  text: "HarmonyOS工具包，封装了常用工具类，提供一系列简单易用的方法。帮助开发者快速构建鸿蒙应用",
  fileName: "漂亮小姐姐.mp4",
  progressValue: 72,
}).then((id) => {
  ToastUtil.showToast(`通知发送成功，id为：${id}`);
  this.notificationIds.push(id);
}).catch((err: BusinessError) => {
  ToastUtil.showToast(`通知发送失败，${err.message}`);
});
```

##### cancel cancel

```
NotificationUtil.cancel(1);
```

##### cancelGroup Cancel notifications under the specified group of this application

```
NotificationUtil.cancelGroup("group_msg");
```

##### cancelAll Cancel all notifications

```
NotificationUtil.cancelAll();
ToastUtil.showToast(`取消所有通知，成功！`);
```

##### setBadge Set the number of desktop angle markers

```
NotificationUtil.setBadge(96);
```

##### clearBadge Clear the corner mark of the desktop

```
NotificationUtil.clearBadge();
```

##### setBadgeFromNotificationCount Sets the number of desktop corner markers, from the number of notifications

```
NotificationUtil.setBadgeFromNotificationCount().then(() => {
  ToastUtil.showToast("设置角标成功");
}).catch((err: BusinessError) => {
  ToastUtil.showToast("设置角标失败，" + NotificationUtil.getErrorMsg(err.code, err.message));
  LogUtil.error(`设置角标异常：${NotificationUtil.getErrorMsg(err.code, err.code + " - " + err.message)}`);
});
```

##### getActiveNotificationCount Gets the number of notifications not deleted by the current application

```
let count = await NotificationUtil.getActiveNotificationCount();
ToastUtil.showToast(`当前通知数量为：${count}`);
```

##### getActiveNotifications Get the list of notifications that are not deleted by the current application

```
 let notifications = await NotificationUtil.getActiveNotifications();
```

##### generateNotificationId Generate notification id (using timestamp as id)

```
 let id = NotificationUtil.generateNotificationId(); //通知id
```

##### getDefaultWantAgent Create a Want that pulls up the Ability

```
let wantAgent = await NotificationUtil.getDefaultWantAgent();
```

##### getCompressedPicture Gets the image of the compressed notification (the total number of bytes of the image pixel cannot exceed 2MB)

```
let lPicture = await NotificationUtil.getCompressedPicture($r("app.media.test_as1"));
```

##### getCompressedIcon Gets the compressed notification icon (the total number of bytes of the icon pixels does not exceed 192KB)

```
let smallIcon = await NotificationUtil.getCompressedIcon($r('app.media.test_as5'));
let largeIcon = await NotificationUtil.getCompressedIcon($r('app.media.test_as1'));
```

## Creation is not easy, please give Elder Tong a thumbs up 👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   

