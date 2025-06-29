# harmony-utils NetworkUtil, network-related tool class

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

##### isDefaultNetMetered Check whether the current data traffic usage on the network is metered

```
 let hasDefaultNet = NetworkUtil.isDefaultNetMeteredSync();
 ToastUtil.showToast(`当前网络上的数据流量使用是否被计量：${hasDefaultNet}`);
```

##### hasDefaultNet Checks whether the default data network is activated

```
let hasDefaultNet = NetworkUtil.hasDefaultNetSync();
ToastUtil.showToast(`默认数据网络是否被激活：${hasDefaultNet}`);
```

##### getDefaultNet Gets the default activated data network

```
  let defaultNet = await NetworkUtil.getDefaultNet();
  let jsonStr = JSON.stringify(defaultNet, null, 2);
```

##### getAppNet Get the network information bound to the app

```
let appNet = await NetworkUtil.getAppNet();
 let jsonStr = JSON.stringify(appNet, null, 2);
```

##### getAllNets Get a list of all connected networks

```
  let allNet = await NetworkUtil.getAllNets();
  let jsonStr = JSON.stringify(allNet, null, 2);
```

##### isNetworkAvailable determines whether the current device network is available

```
let isNetwork = NetworkUtil.isNetworkAvailable();
ToastUtil.showToast(`当前网络是否可用：${isNetwork}`);
```

##### hasNetMobile determines whether the current network is a cellular network (mobile network)

```
let hasNetMobile = NetworkUtil.hasNetMobile();
ToastUtil.showToast(`当前网络是否是蜂窝网络：${hasNetMobile}`);
```

##### hasNetWiFi determines whether the current network is a Wi-Fi network

```
 let hasNetWiFi = NetworkUtil.hasNetWiFi();
 ToastUtil.showToast(`当前网络是否是Wi-Fi网络：${hasNetWiFi}`);
```

##### hasNetEthernet determines whether the current network is an Ethernet network

```
 let hasNetEthernet = NetworkUtil.hasNetEthernet();
 ToastUtil.showToast(`当前网络是否是以太网网络：${hasNetEthernet}`);
```

##### hasNetVPN determines whether the current network is a VPN network

```
 let hasNetVPN = NetworkUtil.hasNetVPN();
 ToastUtil.showToast(`当前网络是否是VPN网络：${hasNetVPN}`);
```

##### hasNetBearType Whether the specified network exists

```
 let hasNet = NetworkUtil.hasNetBearType(connection.NetBearType.BEARER_WIFI);
 ToastUtil.showToast(`是否存在指定的网络：${hasNet}`);
```

##### getNetBearTypes Gets the network type, the array contains only one specific network type

```
let netBearTypes = NetworkUtil.getNetBearTypes();
let jsonStr = JSON.stringify(netBearTypes, null, 2);
```

##### getNetBearType Gets the network type

```
 let type = await NetworkUtil.getNetBearType();
 ToastUtil.showToast(`网络类型：${type}`);
```

##### getNetCapabilities Get the capability information of the network corresponding to netHandle

```
  let netCapabilities = NetworkUtil.getNetCapabilitiesSync();
  let jsonStr = JSON.stringify(netCapabilities, null, 2);
```

##### getConnectionProperties Get the connection information of the network corresponding to netHandle

```
let connectionProperties = NetworkUtil.getConnectionPropertiesSync();
let jsonStr = JSON.stringify(connectionProperties, null, 2);
```

##### getIpAddress Gets the IP address of the current device (after the device is connected to Wi-Fi)

```
 let ip = NetworkUtil.getIpAddress();
 ToastUtil.showToast(ip);
```

##### register subscribes to notifications of specified network status changes, supports multi-event listening callbacks

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

##### unregister Unsubscribe to notifications about default network status changes

```
NetworkUtil.unregister();
ToastUtil.showToast("取消订阅默认网络状态变化监听");
```

##### isNRSupported Determines whether the current device supports NR (New Radio). That is 5G.

```
let isNRSupported = NetworkUtil.isNRSupported();
ToastUtil.showToast(`当前设备是否支持NR：${isNRSupported}`);
```

##### isRadioOn determines whether Radio is open

```
let isRadioOn = await NetworkUtil.isRadioOn();
ToastUtil.showToast(`Radio是否打开：${isRadioOn}`);
```

##### getPrimarySlotId Get the index number of the card slot where the main card is located

```
 let slotId = await NetworkUtil.getPrimarySlotId();
 ToastUtil.showToast(`主卡所在卡槽的索引号：${slotId}`);
```

##### getOperatorName Get the operator name

```
let operatorName = await NetworkUtil.getOperatorName();
ToastUtil.showToast(`运营商名称：${operatorName}`);
```

##### getNetworkState Get network status

```
let networkState = await NetworkUtil.getNetworkState();
let jsonStr = JSON.stringify(networkState, null, 2);
```

##### getNetworkSelectionMode Get the current network selection mode

```
let mode = await NetworkUtil.getNetworkSelectionMode();
let jsonStr = JSON.stringify(mode, null, 2);
```

##### getSignalInformation Gets the list of registered network signal strength information corresponding to the specified SIM card slot

```
 let signalInformation = await NetworkUtil.getSignalInformation();
 let jsonStr = JSON.stringify(signalInformation, null, 2);
```

##### getNetworkType Get network type

```
let networkType = await NetworkUtil.getNetworkType();
ToastUtil.showToast(`网络类型：${networkType}`);
```

##### getNetworkTypeStr Gets the network type and returns the character type

```
 let networkType = await NetworkUtil.getNetworkTypeStr();
 ToastUtil.showToast(`网络类型：${networkType}`);
```

##### getDefaultCellularDataSlotId SIM card to get the default mobile data

```
let slotId = await NetworkUtil.getDefaultCellularDataSlotId();
ToastUtil.showToast(`默认移动数据的SIM卡：${slotId}`);
```

##### getCellularDataFlowType Gets the up and down state of cellular data services

```
 let dataFlowType = await NetworkUtil.getCellularDataFlowType();
 ToastUtil.showToast(`蜂窝数据业务的上下行状态：${dataFlowType}`);
```

##### getCellularDataState Gets the connection status of the packet switching domain (PS domain)

```
 let state = await NetworkUtil.getCellularDataState();
 ToastUtil.showToast(`分组交换域(PS域)的连接状态：${state}`);
```

##### isCellularDataEnabled Check whether cellular data service is enabled

```
let enabled = await NetworkUtil.isCellularDataEnabled();
ToastUtil.showToast(`蜂窝数据业务是否启用：${enabled}`);
```

##### isCellularDataRoamingEnabled Check whether cellular data services are enabled for roaming

```
let enabled = await NetworkUtil.isCellularDataRoamingEnabled();
ToastUtil.showToast(`蜂窝数据业务是否启用漫游：${enabled}`);
```

##### getDefaultCellularDataSimId Gets the SIM card ID of the default mobile data. Bind with SIM card, increment from 1

```
 let simId = NetworkUtil.getDefaultCellularDataSimId();
 ToastUtil.showToast(`默认移动数据的SIM卡ID：${simId}`);
```

##### isSimActive Gets whether the SIM card is activated when the specified card slot is activated

```
let isSimActive = await NetworkUtil.isSimActive(1);
ToastUtil.showToast(`卡槽2SIM卡是否激活：${isSimActive}`);
```

##### hasSimCard Gets whether the SIM card is inserted into the specified card slot

```
  let hasSimCard = await NetworkUtil.hasSimCard(1);
  ToastUtil.showToast(`卡槽2SIM卡是否插卡：${hasSimCard}`);
```

##### getMaxSimCount Get the number of card slots

```
let count = NetworkUtil.getMaxSimCount();
ToastUtil.showToast(`卡槽数量：${count}`);
```

##### getSimOperatorNumeric Gets the PLMN (Public Land Mobile Network) number of the SIM card in the specified card slot.

```
let simOperatorNumeric = await NetworkUtil.getSimOperatorNumeric();
ToastUtil.showToast(`指定卡槽SIM卡的归属PLMN：${simOperatorNumeric}`);
```

##### getSimSpn Get the service provider name of the SIM card specified in the card slot

```
 let simSpn = await NetworkUtil.getSimSpn();
 ToastUtil.showToast(`指定卡槽SIM卡的服务提供商名称：${simSpn}`);
```

##### getSimState Gets the SIM card status of the specified card slot

```
 let simState = await NetworkUtil.getSimState();
 ToastUtil.showToast(`指定卡槽的SIM卡状态：${simState}`);
```

##### getCardType Gets the card type of the SIM card specified in the card slot

```
let cardType = await NetworkUtil.getCardType();
ToastUtil.showToast(`指定卡槽SIM卡的卡类型：${cardType}`);
```

## Creation is not easy, please give Elder Tong a thumbs up 👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   








