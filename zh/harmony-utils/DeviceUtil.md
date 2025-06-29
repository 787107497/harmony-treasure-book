# harmony-utils之DeviceUtil，设备相关工具类

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

##### getDeviceId  获取设备ID（卸载APP后依旧不变，需要权限：ohos.permission.STORE_PERSISTENT_DATA）

```
  let id = DeviceUtil.getDeviceId();
  DialogHelper.showToast(`当前设备号为：${id}`);
```

##### deleteDeviceId  移除设备ID

```
  DeviceUtil.deleteDeviceId();
  ToastUtil.showToast("移除设备ID成功！")
```

##### getODID  获取开发者匿名设备标识符，ODID

```
 let ODID = DeviceUtil.getODID();
 DialogHelper.showToast(`开发者匿名设备标识符为：${ODID}`);
```

##### getOAID  获取开放匿名设备标识符，OAID

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

##### getAAID  获取应用匿名标识符，AAID

```
  let AAID = await DeviceUtil.getAAID();
  DialogHelper.showToast(`AAID为：${AAID}`);
```

##### deleteAAID  删除应用匿名标识符，AAID

```
 DeviceUtil.deleteAAID();     
```

##### getSerial  获取设备序列号。说明：可作为设备唯一识别码。示例：序列号随设备差异。需要权限：ohos.permission.sec.ACCESS_UDID (目前只限系统应用使用，不对三方应用开放)

```
 let str = DeviceUtil.getSerial();
```

##### getUdid  获取设备Udid。需要权限：ohos.permission.sec.ACCESS_UDID (目前只限系统应用使用，不对三方应用开放)

```
 let str = DeviceUtil.getUdid();
```

##### getBrand  获取设备品牌名称。示例：HUAWEI

```
 let str = DeviceUtil.getBrand();
```

##### getProductModel  获取认证型号。示例：ALN-AL00

```
 let str = DeviceUtil.getProductModel();
```

##### getBrandModel  获取设备品牌名称 认证型号。示例：HUAWEI ALN-AL00

```
 let str = DeviceUtil.getBrandModel();
```

##### getMarketName  获取外部产品系列名称。示例：HUAWEI Mate 60 Pro

```
 let str = DeviceUtil.getMarketName();
```

##### getHardwareModel  获取硬件版本号。示例：HL1CMSM

```
 let str = DeviceUtil.getHardwareModel();
```

##### getManufacture  获取设备厂家名称。示例：HUAWEI

```
 let str = DeviceUtil.getManufacture();
```

##### getOsFullName   获取系统版本

```
 let str = DeviceUtil.getOsFullName();
```

##### getDisplayVersion  获取产品版本。示例：ALN-AL00 5.0.0.1(XXX)

```
 let str = DeviceUtil.getDisplayVersion();
```

##### getBuildVersion  获取Build版本号，标识编译构建的版本号

```
 let str = DeviceUtil.getBuildVersion();
```

##### getSdkApiVersion  获取系统软件API版本。示例：12

```
 let str = DeviceUtil.getSdkApiVersion();
```

##### getOsVersion  获取OS版本号（Major版本号,示例：5；Senior版本号，示例：0；Feature版本号，示例：0）

```
 let str = DeviceUtil.getOsVersion();
```

##### getAbiList  应用二进制接口（Abi）。示例：arm64-v8a

```
 let str = DeviceUtil.getAbiList();
```

##### getOsReleaseType  获取系统的发布类型，取值为：Canary、Beta、Release

```
 let str = DeviceUtil.getOsReleaseType();
```

##### getDeviceType  获取当前设备类型

```
 let str = DeviceUtil.getDeviceType();
```

##### getDeviceTypeStr  获取当前设备类型，返回字符串

```
 let str = DeviceUtil.getDeviceTypeStr();
```

##### getConfiguration  获取设备的Configuration

```
  let configuration = DeviceUtil.getConfigurationSync();
  let jsonStr = JSON.stringify(configuration, null, 2);
```

##### getDirection  获取当前设备屏幕方向

```
  let direction = DeviceUtil.getDirection();
```

##### getDeviceCapability  获取设备的DeviceCapability

```
  let deviceCapability = DeviceUtil.getDeviceCapabilitySync();
  let jsonStr = JSON.stringify(deviceCapability, null, 2);
```

##### getScreenDensity  获取当前设备屏幕密度

```
  let density = DeviceUtil.getScreenDensity();
  ToastUtil.showToast(`前设备屏幕密度: ${density}`)
```

##### getBatterySOC  获取当前设备剩余电池电量百分比

```
  let result = DeviceUtil.getBatterySOC();
```

##### getBatteryCapacityLevel  获取当前设备电池电量的等级

```
  let result = DeviceUtil.getBatteryCapacityLevel();
```

##### getHealthStatus  获取当前设备电池的健康状态

```
  let result = DeviceUtil.getHealthStatus();
```

##### getBatteryTemperature  获取当前设备电池的温度，单位0.1摄氏度

```
  let result = DeviceUtil.getBatteryTemperature();
```

##### getVoltage  获取当前设备电池的电压，单位微伏

```
  let result = DeviceUtil.getVoltage();
```

##### getNowCurrent  获取当前设备电池的电流，单位毫安

```
  let result = DeviceUtil.getNowCurrent();
```

##### isActive  检测当前设备是否处于活动状态。有屏的设备为亮屏状态，无屏的设备为非休眠状态

```
  let result = DeviceUtil.isActive();
```

##### isStandby  检测当前设备是否进入待机低功耗续航模式

```
  let result = DeviceUtil.isStandby();
```

##### getPowerMode  获取当前设备的电源模式

```
  let result = DeviceUtil.getPowerMode();
```

##### startVibration  开启设备振动

```
  DeviceUtil.getNowCurrent();
```

##### stopVibration 停止设备振动（按照VIBRATOR_STOP_MODE_TIME模式）

```
  DeviceUtil.stopVibration();
```

## 创作不易，请给童长老点赞👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   


