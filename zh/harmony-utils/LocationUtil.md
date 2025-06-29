# harmony-utils之LocationUtil，定位相关工具类

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

##### isLocationEnabled  判断位置服务是否已经使能(定位是否开启)

```
 let isLocationEnabled = LocationUtil.isLocationEnabled();
 ToastUtil.showToast(`定位是否开启：${isLocationEnabled}`);
```

##### requestLocationPermissions  申请定位权限

```
LocationUtil.requestLocationPermissions().then((grant) => {
  if (grant) { //已授权
    ToastUtil.showToast("授权成功");
  } else {
    ToastUtil.showToast("请在设置中开启定位权限");
    WantUtil.toAppSetting();
  }
});
```

##### getCurrentLocationEasy  获取当前位置

```
LocationUtil.getCurrentLocationEasy().then((location) => {
  let locationStr = `当前位置1：\n${JSON.stringify(location, null, 2)}\n\n`;
  LocationUtil.getGeoAddressFromLocation(location.latitude, location.longitude, 2).then((address) => {
    locationStr = locationStr + `当前位置2：\n${JSON.stringify(address, null, 2)}`;
    LogUtil.error(locationStr);
  });
}).catch((err: BusinessError) => {
  let locationStr = `当前位置~异常信息：\n错误码： ${err.code}\n错误信息：${err.message}`;
  LogUtil.error(locationStr);
});
```

##### getCurrentLocation 获取当前位置

```
LocationUtil.getCurrentLocation().then((location) => {
  let locationStr = `当前位置：\n${JSON.stringify(location, null, 2)}`;
  LogUtil.error(locationStr);
}).catch((err: BusinessError) => {
  let locationStr = `当前位置~异常信息：\n错误码： ${err.code}\n错误信息：${err.message}`;
  LogUtil.error(locationStr);
});
```

##### getLastLocation  获取上一次位置

```
let lastLocation = LocationUtil.getLastLocation();
let locationStr = `当前位置：\n${JSON.stringify(lastLocation, null, 2)}`;
LogUtil.error(locationStr);
```

##### onLocationChangeEasy  开启位置变化订阅，并发起定位请求

```
private locationCallBack: Callback<geoLocationManager.Location> = (location) => {
  let addrStr = `位置变化订阅1：\n${JSON.stringify(location, null, 2)}`;
  LogUtil.info(addrStr);
}
LocationUtil.onLocationChangeEasy(locationCallBack);
```

##### onLocationChange  开启位置变化订阅，并发起定位请求

```
private locationCallBack: Callback<geoLocationManager.Location> = (location) => {
  let addrStr = `位置变化订阅1：\n${JSON.stringify(location, null, 2)}`;
  LogUtil.info(addrStr);
}

let locationRequest: geoLocationManager.LocationRequest = {
  'priority': geoLocationManager.LocationRequestPriority.FIRST_FIX, //表示快速获取位置优先，如果应用希望快速拿到一个位置，可以将优先级设置为该字段。
  'scenario': geoLocationManager.LocationRequestScenario.UNSET, //表示未设置优先级，表示LocationRequestPriority无效。
  'timeInterval': 10, //表示上报位置信息的时间间隔，单位是秒。默认值为1，取值范围为大于等于0。10秒钟获取一下位置
  'distanceInterval': 0, //表示上报位置信息的距离间隔。单位是米，默认值为0，取值范围为大于等于0。
  'maxAccuracy': 0 //表示精度信息，单位是米。
}; //开启位置变化订阅，默认Request参数
LocationUtil.onLocationChange(locationRequest, locationCallBack);
```

##### offLocationChange  关闭位置变化订阅，并删除对应的定位请求

```
LocationUtil.offLocationChange();
```

##### onLocationError  订阅持续定位过程中的错误码

```
LocationUtil.onLocationError((locationError: geoLocationManager.LocationError) => {
  LogUtil.error("订阅持续定位过程中的错误码: " + locationError);
  ToastUtil.showToast("订阅持续定位过程中的错误码: " + locationError);
});
```

##### offLocationError  取消订阅持续定位过程中的错误码

```
 LocationUtil.offLocationError();
 ToastUtil.showToast("取消订阅成功");
```

##### onLocationEnabledChange  订阅位置服务状态变化

```
LocationUtil.onLocationError((locationError: geoLocationManager.LocationError) => {
  LogUtil.error("订阅持续定位过程中的错误码: " + locationError);
  ToastUtil.showToast("订阅持续定位过程中的错误码: " + locationError);
});
```

##### offLocationEnabledChange  取消订阅位置服务状态变化

```
 LocationUtil.offLocationEnabledChange();
 ToastUtil.showToast("取消订阅成功");
```

##### isGeocoderAvailable  判断地理编码与逆地理编码服务是否可用

```
 let isGeocoderAvailable = LocationUtil.isGeocoderAvailable();
 LogUtil.error(`地理编码与逆地理编码服务是否可用：${isGeocoderAvailable}`);
```

##### getGeoAddressFromLocationName  地理编码,将地理描述转换为具体坐标集合

```
let locationName: string = '上海市浦东新区'; //上海市浦东新区
let address = await LocationUtil.getGeoAddressFromLocationName(locationName)
  .catch((err: BusinessError) => {
    return `异常信息：${err.code}  ---  ${err.message}`;
  });
let addrStr = `地理编码：\n${JSON.stringify(address, null, 2)}`;
LogUtil.info(addrStr);
```

##### getAddressFromLocationName 地理编码,将地理描述转换为具体坐标

```
let locationName: string = '上海市浦东新区'; //上海市浦东新区
let address = await LocationUtil.getAddressFromLocationName(locationName)
  .catch((err: BusinessError) => {
    return `异常信息：${err.code}  ---  ${err.message}`;
  });
let addrStr = `地理编码：\n${JSON.stringify(address, null, 2)}`;
LogUtil.info(addrStr);
```

##### getGeoAddressFromLocation  逆地理编码,将坐标转换为地理描述集合

```
let latitude: number = 32.26;
let longitude: number = 117.618;
let address = await LocationUtil.getGeoAddressFromLocation(latitude, longitude)
  .catch((err: BusinessError) => {
    return `异常信息：${err.code}  ---  ${err.message}`;
  });
let addrStr = `逆地理编码：\n${JSON.stringify(address, null, 2)}`;
LogUtil.info(addrStr);
```

##### getAddressFromLocation  逆地理编码,将坐标转换为地理描述

```
let latitude: number = 32.2;
let longitude: number = 117.6;
let address = await LocationUtil.getAddressFromLocation(latitude, longitude)
  .catch((err: BusinessError) => {
    return `异常信息：${err.code}  ---  ${err.message}`;
  });
let addrStr = `逆地理编码：\n${JSON.stringify(address, null, 2)}`;
LogUtil.info(addrStr);
```

##### getCountryCode  获取当前的国家码

```
 let code = await LocationUtil.getCountryCode();
 ToastUtil.showToast(`当前的国家码：${code}`);
```

##### calculateDistance  计算这两个点间的直线距离，单位为米

```
let fromLatLng: mapCommon.LatLng = { latitude: 38, longitude: 118 };
let toLatLng: mapCommon.LatLng = { latitude: 38.5, longitude: 118.5 };
let distance1 = LocationUtil.calculateDistance(fromLatLng, toLatLng);
LogUtil.error(`距离1：${distance1}米`);

let distance2 = LocationUtil.calculateDistanceEasy(38, 118, 39, 119);
LogUtil.error(`距离2：${distance2}米`);
```

##### convertCoordinate  坐标转换，将WGS84坐标系转换为GCJ02坐标系

```
let latLng: mapCommon.LatLng = { latitude: 31.8462, longitude: 117.2456 };
let latLng1 = LocationUtil.convertCoordinateSync(mapCommon.CoordinateType.WGS84, mapCommon.CoordinateType.GCJ02, latLng);
LogUtil.error(`坐标转换，latLng1：${JSON.stringify(latLng1, null, 2)}`);
let latLng2 = LocationUtil.convertCoordinateEasy(latLng);
LogUtil.error(`坐标转换，latLng2：${JSON.stringify(latLng2, null, 2)}`);
```

## 创作不易，请给童长老点赞👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   

