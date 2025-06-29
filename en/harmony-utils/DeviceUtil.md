# Harmony-utils DeviceUtil, device-related tool class

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

##### getDeviceId Get the device ID (it remains unchanged after uninstalling the APP, and permissions are required: ohos.permission.STORE_PERSISTENT_DATA)

```
  let id = DeviceUtil.getDeviceId();
  DialogHelper.showToast(`当前设备号为：${id}`);
```

##### deleteDeviceId Remove the device ID

```
  DeviceUtil.deleteDeviceId();
  ToastUtil.showToast("移除设备ID成功！")
```

##### getODID Get the developer's anonymous device identifier, ODID

```
 let ODID = DeviceUtil.getODID();
 DialogHelper.showToast(`开发者匿名设备标识符为：${ODID}`);
```

##### getOAID Get the open anonymous device identifier, OAID

```
PermissionUtil.requestPermissionsEasy("ohos.permission.APP_TRACKING_CONSENT").then(async (grant) => {
  if (grant) {
    DeviceUtil.getOAID().then((id) => {
      ToastUtil.showToast("开放匿名设备标识符位：" + id);
    }).catch((err: BusinessError) => {
      ToastUtil.showToast(`开放匿名设备标识符获取失败，${err.message}！`);
    });
  } else {
    ToastUtil.showToast("您拒绝了权限！")
  }
});
```

##### getAAID Get the application anonymous identifier, AAID

```
  let AAID = await DeviceUtil.getAAID();
  DialogHelper.showToast(`AAID为：${AAID}`);
```

##### deleteAAID Delete the app anonymous identifier, AAID

```
 DeviceUtil.deleteAAID();     
```

##### getSerial Gets the device serial number. Description: Can be used as a unique identification code for the device. Example: The serial number varies with the device. Permission required: ohos.permission.sec.ACCESS_UDID (currently only for system applications and is not open to three-party applications)

```
 let str = DeviceUtil.getSerial();
```

##### getUdid Get the device Udid. Permission required: ohos.permission.sec.ACCESS_UDID (currently only for system applications and is not open to three-party applications)

```
 let str = DeviceUtil.getUdid();
```

##### getBrand Get the device brand name. Example: HUAWEI

```
 let str = DeviceUtil.getBrand();
```

##### getProductModel Get certified model. Example: ALN-AL00

```
 let str = DeviceUtil.getProductModel();
```

##### getBrandModel Get the device brand name Certified model. Example: HUAWEI ALN-AL00

```
 let str = DeviceUtil.getBrandModel();
```

##### getMarketName Gets the external product series name. Example: HUAWEI Mate 60 Pro

```
 let str = DeviceUtil.getMarketName();
```

##### getHardwareModel Gets the hardware version number. Example: HL1CMSM

```
 let str = DeviceUtil.getHardwareModel();
```

##### getManufacture Gets the name of the device manufacturer. Example: HUAWEI

```
 let str = DeviceUtil.getManufacture();
```

##### getOsFullName Get the system version

```
 let str = DeviceUtil.getOsFullName();
```

##### getDisplayVersion Gets the product version. Example: ALN-AL00 5.0.0.1(XXX)

```
 let str = DeviceUtil.getDisplayVersion();
```

##### getBuildVersion Gets the Build version number, identifying the version number of the compiled build

```
 let str = DeviceUtil.getBuildVersion();
```

##### getSdkApiVersion Gets the system software API version. Example: 12

```
 let str = DeviceUtil.getSdkApiVersion();
```

##### getOsVersion Gets the OS version number (Major version number, example: 5; Senior version number, example: 0; Feature version number, example: 0)

```
 let str = DeviceUtil.getOsVersion();
```

##### getAbiList Application binary interface (Abi). Example: arm64-v8a

```
 let str = DeviceUtil.getAbiList();
```

##### getOsReleaseType Gets the system's publishing type, with values: Canary, Beta, Release

```
 let str = DeviceUtil.getOsReleaseType();
```

##### getDeviceType Gets the current device type

```
 let str = DeviceUtil.getDeviceType();
```

##### getDeviceTypeStr Gets the current device type and returns the string

```
 let str = DeviceUtil.getDeviceTypeStr();
```

##### getConfiguration Gets the configuration of the device

```
  let configuration = DeviceUtil.getConfigurationSync();
  let jsonStr = JSON.stringify(configuration, null, 2);
```

##### getDirection Gets the current device screen direction

```
  let direction = DeviceUtil.getDirection();
```

##### getDeviceCapability Get the DeviceCapability of the device

```
  let deviceCapability = DeviceUtil.getDeviceCapabilitySync();
  let jsonStr = JSON.stringify(deviceCapability, null, 2);
```

##### getScreenDensity Gets the current device screen density

```
  let density = DeviceUtil.getScreenDensity();
  ToastUtil.showToast(`前设备屏幕密度: ${density}`)
```

##### getBatterySOC Gets the percentage of battery remaining in the current device

```
  let result = DeviceUtil.getBatterySOC();
```

##### getBatteryCapacityLevel Gets the current device battery level

```
  let result = DeviceUtil.getBatteryCapacityLevel();
```

##### getHealthStatus Get the current device battery health status

```
  let result = DeviceUtil.getHealthStatus();
```

##### getBatteryTemperature Gets the temperature of the current device battery in 0.1 degrees Celsius

```
  let result = DeviceUtil.getBatteryTemperature();
```

##### getVoltage Gets the voltage of the current device battery, unit to microvoltage

```
  let result = DeviceUtil.getVoltage();
```

##### getNowCurrent Get the current of the current device battery, unit mAh

```
  let result = DeviceUtil.getNowCurrent();
```

##### isActive Detects whether the current device is active. Devices with screens are in a light screen state, and devices without screens are in a non-sleep state

```
  let result = DeviceUtil.isActive();
```

##### isStandby Detects whether the current device enters standby low power battery life mode

```
  let result = DeviceUtil.isStandby();
```

##### getPowerMode Gets the power mode of the current device

```
  let result = DeviceUtil.getPowerMode();
```

##### startVibration Turn on device vibration

```
  DeviceUtil.getNowCurrent();
```

##### stopVibration stops the device vibration (according to VIBRATOR_STOP_MODE_TIME mode)

```
  DeviceUtil.stopVibration();
```

## Creation is not easy, please give Elder Tong a thumbs up 👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   


