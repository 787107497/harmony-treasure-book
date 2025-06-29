# LocationUtil of harmony-utils, location related tool class

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

##### isLocationEnabled determines whether the location service has been enabled (whether the location is enabled)

```
 let isLocationEnabled = LocationUtil.isLocationEnabled();
 ToastUtil.showToast(`定位是否开启：${isLocationEnabled}`);
```

##### requestLocationPermissions request location permissions

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

##### getCurrentLocationEasy Get the current location

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

##### getCurrentLocation Get the current location

```
LocationUtil.getCurrentLocation().then((location) => {
  let locationStr = `当前位置：\n${JSON.stringify(location, null, 2)}`;
  LogUtil.error(locationStr);
}).catch((err: BusinessError) => {
  let locationStr = `当前位置~异常信息：\n错误码： ${err.code}\n错误信息：${err.message}`;
  LogUtil.error(locationStr);
});
```

##### getLastLocation Get the last location

```
let lastLocation = LocationUtil.getLastLocation();
let locationStr = `当前位置：\n${JSON.stringify(lastLocation, null, 2)}`;
LogUtil.error(locationStr);
```

##### onLocationChangeEasy Enable location change subscription and initiate positioning request

```
private locationCallBack: Callback<geoLocationManager.Location> = (location) => {
  let addrStr = `位置变化订阅1：\n${JSON.stringify(location, null, 2)}`;
  LogUtil.info(addrStr);
}
LocationUtil.onLocationChangeEasy(locationCallBack);
```

##### onLocationChange Enable location change subscription and initiate positioning requests

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

##### offLocationChange Close the location change subscription and delete the corresponding location request

```
LocationUtil.offLocationChange();
```

##### onLocationError Error code during subscription continuous positioning

```
LocationUtil.onLocationError((locationError: geoLocationManager.LocationError) => {
  LogUtil.error("订阅持续定位过程中的错误码: " + locationError);
  ToastUtil.showToast("订阅持续定位过程中的错误码: " + locationError);
});
```

##### offLocationError Error code during unsubscribe to continuous positioning

```
 LocationUtil.offLocationError();
 ToastUtil.showToast("取消订阅成功");
```

##### onLocationEnabledChange Subscription Location Service Status Change

```
LocationUtil.onLocationError((locationError: geoLocationManager.LocationError) => {
  LogUtil.error("订阅持续定位过程中的错误码: " + locationError);
  ToastUtil.showToast("订阅持续定位过程中的错误码: " + locationError);
});
```

##### offLocationEnabledChange Unsubscribe to location service status changes

```
 LocationUtil.offLocationEnabledChange();
 ToastUtil.showToast("取消订阅成功");
```

##### isGeocoderAvailable determines whether geocoding and inverse geocoding services are available

```
 let isGeocoderAvailable = LocationUtil.isGeocoderAvailable();
 LogUtil.error(`地理编码与逆地理编码服务是否可用：${isGeocoderAvailable}`);
```

##### getGeoAddressFromLocationName geocoding, converting geographic descriptions into specific coordinate sets

```
let locationName: string = '上海市浦东新区'; //上海市浦东新区
let address = await LocationUtil.getGeoAddressFromLocationName(locationName)
  .catch((err: BusinessError) => {
    return `异常信息：${err.code}  ---  ${err.message}`;
  });
let addrStr = `地理编码：\n${JSON.stringify(address, null, 2)}`;
LogUtil.info(addrStr);
```

##### getAddressFromLocationName geocoding, converting geographic descriptions into specific coordinates

```
let locationName: string = '上海市浦东新区'; //上海市浦东新区
let address = await LocationUtil.getAddressFromLocationName(locationName)
  .catch((err: BusinessError) => {
    return `异常信息：${err.code}  ---  ${err.message}`;
  });
let addrStr = `地理编码：\n${JSON.stringify(address, null, 2)}`;
LogUtil.info(addrStr);
```

##### getGeoAddressFromLocation Inverse geocoding, convert coordinates into geographic description sets

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

##### getAddressFromLocation Inverse geocoding, convert coordinates to geographic description

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

##### getCountryCode Get the current country code

```
 let code = await LocationUtil.getCountryCode();
 ToastUtil.showToast(`当前的国家码：${code}`);
```

##### calculateDistance calculates the straight line distance between these two points, in meters

```
let fromLatLng: mapCommon.LatLng = { latitude: 38, longitude: 118 };
let toLatLng: mapCommon.LatLng = { latitude: 38.5, longitude: 118.5 };
let distance1 = LocationUtil.calculateDistance(fromLatLng, toLatLng);
LogUtil.error(`距离1：${distance1}米`);

let distance2 = LocationUtil.calculateDistanceEasy(38, 118, 39, 119);
LogUtil.error(`距离2：${distance2}米`);
```

##### convertCoordinate coordinate conversion, convert WGS84 coordinate system to GCJ02 coordinate system

```
let latLng: mapCommon.LatLng = { latitude: 31.8462, longitude: 117.2456 };
let latLng1 = LocationUtil.convertCoordinateSync(mapCommon.CoordinateType.WGS84, mapCommon.CoordinateType.GCJ02, latLng);
LogUtil.error(`坐标转换，latLng1：${JSON.stringify(latLng1, null, 2)}`);
let latLng2 = LocationUtil.convertCoordinateEasy(latLng);
LogUtil.error(`坐标转换，latLng2：${JSON.stringify(latLng2, null, 2)}`);
```

## Creation is not easy, please give Elder Tong a thumbs up 👍

------
[https://github.com/787107497/harmony-utils](https://github.com/787107497/harmony-utils)   
[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[OpenHarmony三方库](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)   
[童长老CSDN博客](https://blog.csdn.net/qq_32922545)   
   

