# harmony-utils之NetworkUtil，网络相关工具类

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

##### isDefaultNetMetered  检查当前网络上的数据流量使用是否被计量

```
 let hasDefaultNet = NetworkUtil.isDefaultNetMeteredSync();
 ToastUtil.showToast(`当前网络上的数据流量使用是否被计量：${hasDefaultNet}`);
```

##### hasDefaultNet  检查默认数据网络是否被激活

```
let hasDefaultNet = NetworkUtil.hasDefaultNetSync();
ToastUtil.showToast(`默认数据网络是否被激活：${hasDefaultNet}`);
```

##### getDefaultNet  获取默认激活的数据网络

```
  let defaultNet = await NetworkUtil.getDefaultNet();
  let jsonStr = JSON.stringify(defaultNet, null, 2);
```

##### getAppNet  获取App绑定的网络信息

```
let appNet = await NetworkUtil.getAppNet();
 let jsonStr = JSON.stringify(appNet, null, 2);
```

##### getAllNets  获取所有处于连接状态的网络列表

```
  let allNet = await NetworkUtil.getAllNets();
  let jsonStr = JSON.stringify(allNet, null, 2);
```

##### isNetworkAvailable  判断当前设备网络是否可用

```
let isNetwork = NetworkUtil.isNetworkAvailable();
ToastUtil.showToast(`当前网络是否可用：${isNetwork}`);
```

##### hasNetMobile  判断当前网络是否是蜂窝网络（移动网络）

```
let hasNetMobile = NetworkUtil.hasNetMobile();
ToastUtil.showToast(`当前网络是否是蜂窝网络：${hasNetMobile}`);
```

##### hasNetWiFi   判断当前网络是否是Wi-Fi网络

```
 let hasNetWiFi = NetworkUtil.hasNetWiFi();
 ToastUtil.showToast(`当前网络是否是Wi-Fi网络：${hasNetWiFi}`);
```

##### hasNetEthernet  判断当前网络是否是以太网网络

```
 let hasNetEthernet = NetworkUtil.hasNetEthernet();
 ToastUtil.showToast(`当前网络是否是以太网网络：${hasNetEthernet}`);
```

##### hasNetVPN  判断当前网络是否是VPN网络

```
 let hasNetVPN = NetworkUtil.hasNetVPN();
 ToastUtil.showToast(`当前网络是否是VPN网络：${hasNetVPN}`);
```

##### hasNetBearType  是否存在指定的网络

```
 let hasNet = NetworkUtil.hasNetBearType(connection.NetBearType.BEARER_WIFI);
 ToastUtil.showToast(`是否存在指定的网络：${hasNet}`);
```

##### getNetBearTypes  获取网络类型，数组里面只包含了一种具体的网络类型

```
let netBearTypes = NetworkUtil.getNetBearTypes();
let jsonStr = JSON.stringify(netBearTypes, null, 2);
```

##### getNetBearType  获取网络类型

```
 let type = await NetworkUtil.getNetBearType();
 ToastUtil.showToast(`网络类型：${type}`);
```

##### getNetCapabilities  获取netHandle对应的网络的能力信息

```
  let netCapabilities = NetworkUtil.getNetCapabilitiesSync();
  let jsonStr = JSON.stringify(netCapabilities, null, 2);
```

##### getConnectionProperties  获取netHandle对应的网络的连接信息

```
let connectionProperties = NetworkUtil.getConnectionPropertiesSync();
let jsonStr = JSON.stringify(connectionProperties, null, 2);
```

##### getIpAddress  获取当前设备的IP地址(设备连接Wi-Fi后)

```
 let ip = NetworkUtil.getIpAddress();
 ToastUtil.showToast(ip);
```

##### register  订阅指定网络状态变化的通知，支持多事件监听回调

```
NetworkUtil.register((netHandle) => {
  LogUtil.error(`订阅网络可用事件回调：${JSON.stringify(netHandle)}`);
}, () => {
  LogUtil.error(`订阅网络不可用事件回调。`);
}, (netCapabilityInfo) => {
  LogUtil.error(`订阅网络能力变化事件回调：${JSON.stringify(netCapabilityInfo)}`);
}, (nNetConnectionPropertyInfo) => {
  LogUtil.error(`订阅网络连接信息变化事件回调：${JSON.stringify(nNetConnectionPropertyInfo)}`);
}, (netBlockStatusInfo) => {
  LogUtil.error(`订阅网络阻塞状态事件回调：${JSON.stringify(netBlockStatusInfo)}`);
}, (netHandle) => {
  LogUtil.error(`订阅网络丢失事件回调：${JSON.stringify(netHandle)}`);
});
```

##### unregister  取消订阅默认网络状态变化的通知

```
NetworkUtil.unregister();
ToastUtil.showToast("取消订阅默认网络状态变化监听");
```

##### isNRSupported   判断当前设备是否支持NR(New Radio)。也就是5G。

```
let isNRSupported = NetworkUtil.isNRSupported();
ToastUtil.showToast(`当前设备是否支持NR：${isNRSupported}`);
```

##### isRadioOn  判断Radio是否打开

```
let isRadioOn = await NetworkUtil.isRadioOn();
ToastUtil.showToast(`Radio是否打开：${isRadioOn}`);
```

##### getPrimarySlotId  获取主卡所在卡槽的索引号

```
 let slotId = await NetworkUtil.getPrimarySlotId();
 ToastUtil.showToast(`主卡所在卡槽的索引号：${slotId}`);
```

##### getOperatorName  获取运营商名称

```
let operatorName = await NetworkUtil.getOperatorName();
ToastUtil.showToast(`运营商名称：${operatorName}`);
```

##### getNetworkState  获取网络状态

```
let networkState = await NetworkUtil.getNetworkState();
let jsonStr = JSON.stringify(networkState, null, 2);
```

##### getNetworkSelectionMode  获取当前选网模式

```
let mode = await NetworkUtil.getNetworkSelectionMode();
let jsonStr = JSON.stringify(mode, null, 2);
```

##### getSignalInformation  获取指定SIM卡槽对应的注册网络信号强度信息列表

```
 let signalInformation = await NetworkUtil.getSignalInformation();
 let jsonStr = JSON.stringify(signalInformation, null, 2);
```

##### getNetworkType  获取网络类型

```
let networkType = await NetworkUtil.getNetworkType();
ToastUtil.showToast(`网络类型：${networkType}`);
```

##### getNetworkTypeStr  获取网络类型，返回字符类型

```
 let networkType = await NetworkUtil.getNetworkTypeStr();
 ToastUtil.showToast(`网络类型：${networkType}`);
```

##### getDefaultCellularDataSlotId  获取默认移动数据的SIM卡

```
let slotId = await NetworkUtil.getDefaultCellularDataSlotId();
ToastUtil.showToast(`默认移动数据的SIM卡：${slotId}`);
```

##### getCellularDataFlowType  获取蜂窝数据业务的上下行状态

```
 let dataFlowType = await NetworkUtil.getCellularDataFlowType();
 ToastUtil.showToast(`蜂窝数据业务的上下行状态：${dataFlowType}`);
```

##### getCellularDataState  获取分组交换域(PS域)的连接状态

```
 let state = await NetworkUtil.getCellularDataState();
 ToastUtil.showToast(`分组交换域(PS域)的连接状态：${state}`);
```

##### isCellularDataEnabled  检查蜂窝数据业务是否启用

```
let enabled = await NetworkUtil.isCellularDataEnabled();
ToastUtil.showToast(`蜂窝数据业务是否启用：${enabled}`);
```

##### isCellularDataRoamingEnabled  检查蜂窝数据业务是否启用漫游

```
let enabled = await NetworkUtil.isCellularDataRoamingEnabled();
ToastUtil.showToast(`蜂窝数据业务是否启用漫游：${enabled}`);
```

##### getDefaultCellularDataSimId   获取默认移动数据的SIM卡ID。与SIM卡绑定，从1开始递增

```
 let simId = NetworkUtil.getDefaultCellularDataSimId();
 ToastUtil.showToast(`默认移动数据的SIM卡ID：${simId}`);
```

##### isSimActive  获取指定卡槽SIM卡是否激活

```
let isSimActive = await NetworkUtil.isSimActive(1);
ToastUtil.showToast(`卡槽2SIM卡是否激活：${isSimActive}`);
```

##### hasSimCard  获取指定卡槽SIM卡是否插卡

```
  let hasSimCard = await NetworkUtil.hasSimCard(1);
  ToastUtil.showToast(`卡槽2SIM卡是否插卡：${hasSimCard}`);
```

##### getMaxSimCount  获取卡槽数量

```
let count = NetworkUtil.getMaxSimCount();
ToastUtil.showToast(`卡槽数量：${count}`);
```

##### getSimOperatorNumeric  获取指定卡槽SIM卡的归属PLMN（Public Land Mobile Network）号

```
let simOperatorNumeric = await NetworkUtil.getSimOperatorNumeric();
ToastUtil.showToast(`指定卡槽SIM卡的归属PLMN：${simOperatorNumeric}`);
```

##### getSimSpn  获取指定卡槽SIM卡的服务提供商名称

```
 let simSpn = await NetworkUtil.getSimSpn();
 ToastUtil.showToast(`指定卡槽SIM卡的服务提供商名称：${simSpn}`);
```

##### getSimState  获取指定卡槽的SIM卡状态

```
 let simState = await NetworkUtil.getSimState();
 ToastUtil.showToast(`指定卡槽的SIM卡状态：${simState}`);
```

##### getCardType  获取指定卡槽SIM卡的卡类型

```
let cardType = await NetworkUtil.getCardType();
ToastUtil.showToast(`指定卡槽SIM卡的卡类型：${cardType}`);
```

## 创作不易，请给童长老点赞👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   








