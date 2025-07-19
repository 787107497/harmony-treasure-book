# harmony-utils(API12+)

## 🏆Introduction and Description

[harmony-utils](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils) A HarmonyOS tool library with rich features and extremely easy to use, with the help of many practical tools, is committed to helping developers quickly build Hongmeng applications. Its encapsulated tools cover APP, device, screen, authorization, notification, inter-thread communication, pop-up frames, toast, biometric authentication, user preferences, taking photos, albums, scanning codes, files, logs, exception capture, characters, strings, numbers, collections, dates, random, base64, encryption, decryption, JSON and other functions, which can meet various development needs.    
[picker_utils](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fpicker_utils) It is a sub-store split by harmony-utils, including PickerUtil, PhotoHelper, and ScanUtil.

> **📚 Warm reminder: **
> 📕 Harmony-utils is a lightweight framework that integrates more than 50 tool classes, but it is only 130KB in size. Achieve the ultimate balance between tool count and lightweight performance.
> 📙 Starting from version 1.3.2, the methods in the harmony-utils tool library will no longer be directly discarded. Please feel free to use it in third-party libraries and projects.
> 📒 In the update record, each version number has the corresponding minimum development tool version, such as: "DevEco Studio 5.1.0 Release".
> 📗 Please read the documentation carefully and view the use case before using the framework. 🙏
> 📘 See, please! Follow the official account of "Elder Tong" quickly, and you are waiting for you to unlock it.
> 📔 Creation is not easy, please give Elder Tong a thumbs up 👍[github❤️](https://github.com/787107497/harmony-utils) [gitee❤️](https://gitee.com/tongyuyan/harmony-utils) [三方库❤️](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)

## 🌞Download, installation and use instructions 🙏

`ohpm i @pura/harmony-utils`   
OpenHarmony ohpm environment configuration and more, please refer to[如何安装 OpenHarmony ohpm 包](https://ohpm.openharmony.cn/#/cn/help/downloadandinstall)
 ```
全局初始化方法，从1.2.0版本开始，在UIAbility的onCreate方法中初始化 AppUtil.init()
    
  onCreate(want: Want, launchParam: AbilityConstant.LaunchParam): void {
    AppUtil.init(this.context);
  }
 ```

## 📂Module Introduction

| Module | Introduction |
|:----------------------------------------------------------------------------------|:-------------------------------------------------------------------------------------------------------------|
| AppUtil | APP-related tool categories |
| DeviceUtil | Device-related tools |
| WindowUtil | Window related tool classes |
| DisplayUtil | Screen related tools |
| PermissionUtil | Application Authorization Tools |
| AuthUtil | Mobile phone biometric authentication (fingerprint, face, password) tools |
| NetworkUtil | Network related tools |
| FileUtil | File operation related tool categories |
| ImageUtil | Picture-related tools |
| PreviewUtil | File Preview Tools |
| LocationUtil | Positioning Tool Class (WGS-84 Coordinate System) |
| LogUtil | Log Tools |
| CrashUtil | Global exception capture, crash log collection |
| EmitterUtil | Emitter tool class (for inter-thread communication) |
| WantUtil | Want Tools |
| KvUtil | Key-value database tool class |
| PreferencesUtil | Preferences (User Preferences) Tool Class |
| CacheUtil | Cache Tools |
| LRUCacheUtil | LRUCache Cache Tool Class |
| NotificationUtil | Notification Tools |
| SnapshotUtil | Component screenshot and window screenshot tool class.                                                                                                |
| KeyboardUtil | Keyboard Tools |
| PasteboardUtil | Clipboard Tools |
| AssetUtil | Key Asset Storage Service Tools |
| ResUtil | Resource Tools |
| ObjectUtil | Object Tool Class |
| JSONUtil | JSON Tool Class |
| DateUtil | Date Tools |
| Base64Util | Base64 Tools |
| StrUtil | String Tool Class |
| CharUtil | Character Tools |
| NumberUtil | number tool class |
| ArrayUtil | Collection Tools |
| RandomUtil | Random Tools |
| RegexUtil | Regular Tools |
| TypeUtil | Type Checking Tool Class |
| FormatUtil | Format Tools |
| ClickUtil | Throttle, anti-shake tool class (used to click events to prevent buttons from being clicked repeatedly) |
| TempUtil | Temperature conversion tool category |
| DialogUtil | Pop-up tool class (AlertDialog) |
| ToastUtil | Toast Tools (promptAction) |
| SM2, SM3, SM4, <br/>AES, DES, RSA, <br/>MD5, SHA, ECDSA, <br/>CryptoUtil, <br/>CryptoHelper | Encryption and decryption algorithm tool class<br/>CryptoUtil: Encryption and decryption utility class, used with each encryption module. <br/>CryptoHelper: Encrypt and decrypt data type conversion.                                     |
| PickerUtil | Selection and saving of photos, files (files, pictures, videos, audio), tools.[拆分至 picker_utils](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fpicker_utils) |
| PhotoHelper | Photo Album related tool category.[拆分至 picker_utils](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fpicker_utils)                     |
| ScanUtil | Code tool category (scan code, code image generation, picture identification).[拆分至 picker_utils](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fpicker_utils)          |

<br>

## AppUtil (APP-related tool class)[使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/utils/AppUtilPage.ets)

| Methods | Introduction |
|:------------------------------------------|:-------------------------------------------------------------------------|
| init | Initialization method, cache global variables, and initialize the method in UIAbility's onCreate method |
| isApiSupported | Check whether the API version is safe |
| getApplicationContext | Ability to get application-level context, ApplicationContext |
| getContext | Get context, common.UIAbilityContext |
| getUIContext | Get UIContext |
| getWindowStage | Get WindowStage |
| getMainWindow | Get the main window |
| getConfiguration | Get the application's Configuration |
| setGrayScale | Set grayscale, APP has one-click graying |
| setColorMode | Set the applied color mode. Only main thread calls are supported. Set color mode, including: dark mode, light mode, no setting (follow system) |
| getColorMode | Get the color mode of the application |
| setFont | Set the font type of the application. Only main thread calls are supported |
| setFontSizeScale | Set the applied font size scaling ratio. Only main thread calls are supported. <API13+> |
| getFontSizeScale | Get the app font size scaling |
| setLanguage | Set the language of the application |
| getLanguage | Get the language of the application |
| setSupportedProcessCache | Set whether the application itself supports cache and starts quickly |
| clearUpApplicationData | Clean up the application's own data and revoke the application's permissions to the user.                                                |
| killAllProcesses | Terminate all processes of the application, and the application life cycle will not be completed normally when the process exits.                                             |
| restartApp | Restart the app and pull up the specified UIAbility of itself. The onDestroy callback will not be received during restart.                                 |
| exit | Actively exit the entire application; after calling this method, the tasks in the task center will not be cleaned by default. If you need to clean it, you need to configure removeMissionAfterTerminate to true. |
| getRunningProcessInformation | Get information about running the process |
| onApplicationStateChange | Register listening to changes before and after the current application |
| offApplicationStateChange | Cancel listening to the application's front and backend switching events |
| onEnvironment | Register monitoring of system environment changes |
| offEnvironment | Cancel monitoring of system environment changes |
| onAbilityLifecycle | Register to listen for in-app lifecycle |
| offAbilityLifecycle | Cancel listen for in-app lifecycle |
| getKeyboardAvoidMode | Get page avoidance mode when virtual keyboard is lifted (OFFSET-up mode, RESIZE-compression mode) |
| setKeyboardAvoidMode | Set the page avoidance mode when the virtual keyboard pops up |
| isPortrait | Is the current device displayed in a vertical screen |
| isLandscape | Is the current device displayed in landscape mode |
| getStatusBarHeight | Get the height of the status bar in px |
| getNavigationIndicatorHeight | Get the height of the bottom navigation bar in px.                                                        |
| setStatusBar | Set the immersive status bar (need to be used with getStatusBarHeight and getNavigationIndicatorHeight) |
| getBundleInfo<br/>getBundleInfoSync | Get the BundleInfo for the current application |
| getAppInfo<br/>getAppInfoSync | Get application configuration information |
| getSignatureInfo<br/>getSignatureInfoSync | Get the signature information of the application package |
| getBundleName | Get the name of the application package |
| getVersionCode | Get application version number |
| getVersionName | Get application version name |
| getTargetVersion | Get the target version of the application running |
| getInstallTime | Application Package Installation Time |
| getUpdateTime | Application Package Update Time |
| getAppProvisionType | Get the type of application signature certificate file, divided into two types: debug and release.                                     |
| debug | Indicates whether the application is in debug mode. A value of true means the application is in debug mode. A value of false means the application is in non-debug mode.                      |

## DeviceUtil (device-related tool class)[使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/utils/DeviceUtilPage.ets)

| Methods | Introduction |
|:------------------------------------------------|:--------------------------------------------------------------|
| getDeviceId | Get the device ID (it remains unchanged after uninstalling the APP, and permissions are required: ohos.permission.STORE_PERSISTENT_DATA) |
| deleteDeviceId | Remove Device ID |
| getODID | Get the developer's anonymous device identifier, ODID.                                            |
| getOAID | Get the open anonymous device identifier, OAID.                                             |
| getAAID | Get AAID.                                                       |
| deleteAAID | DeleteAAID.                                                       |
| getSerial | Get the device serial number. Description: Can be used as a unique identification code for the device. Example: The serial number varies with the device.                            |
| getUdid | Get the device Udid.                                                     |
| getBrand | Get the device brand name. Example: HUAWEI.                                           |
| getProductModel | Get certified model. Example: ALN-AL00.                                           |
| getBrandModel | Get the device brand name Certified model. Example: HUAWEI ALN-AL00.                             |
| getMarketName | Get the external product series name. Example: HUAWEI Mate 60 Pro.                             |
| getHardwareModel | Get the hardware version number. Example: HL1CMSM.                                           |
| getManufacture | Get the device manufacturer name. Example: HUAWEI.                                           |
| getOsFullName | Get system version |
| getDisplayVersion | Get the product version. Example: ALN-AL00 5.0.0.1(XXX) |
| getBuildVersion | Get the Build version number, identifying the version number of the compiled and built |
| getSdkApiVersion | Get the system software API version. Example: 12 |
| getOsVersion | Get the OS version number (Major version number, example: 5; Senior version number, example: 0; Feature version number, example: 0).        |
| getAbiList | Application binary interface (Abi). Example: arm64-v8a |
| getOsReleaseType | Get the system's publishing type, the values ​​are: Canary, Beta, Release |
| getDeviceType | Get the current device type |
| getDeviceTypeStr | Get the current device type and return the string.                                               |
| getConfiguration<br/>getConfigurationSync | Get the device's Configuration |
| getDirection | Get the current device screen direction |
| getDeviceCapability<br/>getDeviceCapabilitySync | Get DeviceCapability for DeviceCapability |
| getScreenDensity | Get the current device screen density |
| getBatterySOC | Get the percentage of battery remaining in the current device.                                              |
| getBatteryCapacityLevel | Get the current device battery level.                                                |
| getHealthStatus | Get the current health status of the device battery.                                                |
| getBatteryTemperature | Get the current device battery temperature, unit 0.1 degrees Celsius.                                         |
| getVoltage | Get the voltage of the current device battery, unit to microvolts.                                             |
| getNowCurrent | Get the current of the current device battery in milliamperes.                                             |
| isActive | Detect whether the current device is active. Devices with screens are in a light screen state, while devices without screens are in a non-sleep state.                        |
| isStandby | Detect whether the current device enters standby low-power battery life mode.                                          |
| getPowerMode | Get the power mode of the current device.                                                  |
| startVibration | Turn on device vibration |
| stopVibration | Stop the device vibration (according to VIBRATOR_STOP_MODE_TIME mode) |

## WindowUtil (window-related tool class)[使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/utils/WindowUtilPage.ets)

| Methods | Introduction |
|:-----------------------------|:------------------------------------------------------------------------------------|
| setPreferredOrientation | Set the display direction properties of the window |
| getPreferredOrientation | Get the display direction property of the window, and the main window is called.                                                                  |
| setWindowPrivacyMode | Set whether the window is in Privacy Mode. For a window set to privacy mode, the content of the window will not be screenshot or recorded |
| isPrivacyMode | Whether the window is privacy mode, the default main window.                                                                     |
| setWindowLayoutFullScreen | Set whether the layout of the window is an immersive layout (the status bar and navigation bar of the immersive layout are still displayed) |
| isLayoutFullScreen | Determine whether the window is immersive, the default main window.                                                                   |
| setWindowSystemBarProperties | Set the properties of the three-key navigation bar and status bar in the main window.                                                                  |
| getWindowSystemBarProperties | Get the properties of the three-key navigation bar and status bar in the main window.                                                                  |
| setImmersiveModeEnabledState | Set whether the current window is turned on to immersive layout. This call will not change the window mode and window size.                                                   |
| getImmersiveModeEnabledState | Check whether the current window has enabled immersive layout.                                                                  |
| setWindowGrayScale | Set window grayscale. This interface needs to be called after calling loadContent() or setUIContent() to make the window load the page content.                            |
| setWindowBackgroundColor | Set the background color of the window. Under the Stage model, this interface needs to be used after the loadContent() or setUIContent() call takes effect |
| setWindowSystemBarEnable | Set the visible mode of the three-key navigation bar, status bar, and bottom navigation bar in the main window. The status bar and bottom navigation bar are controlled through status and the three-key navigation bar are controlled through navigation.                  |
| setSpecificSystemBarEnabled | Set the display and hide of the three-key navigation bar, status bar, and bottom navigation bar in the main window.                                                         |
| setWindowKeepScreenOn | Set whether the screen is always on |
| isKeepScreenOn | Is the screen always lit |
| setWindowBrightness | Set screen brightness value |
| getBrightness | Get screen brightness. This parameter is a floating point number, and the brightness range that can be set is [0.0, 1.0], which indicates the maximum brightness value when taken 1.0. If the window does not set the brightness value, it means that the brightness follows the system, and the brightness value obtained at this time is -1. |
| setWindowFocusable | Sets the scene where the window is focused by clicking or other means, whether the window supports switching the window focus from the focus window before clicking to the window |
| isFocusable | Whether the window is focused, the default main window.                                                                      |
| setWindowTouchable | Set whether the window is touchable |
| isTouchable | Whether the window is touchable, the default main window.                                                                      |
| getWindowProperties | Get the properties of the current window, the default main window.                                                                    |
| getWindowAvoidArea | Get the area to which the current application window content is evaded. For example, when the system bar area, notch screen area, gesture area, soft keyboard area, etc. overlap with the window content, the window content needs to be avoided.                       |
| getWindowType | Gets the window type, default main window.                                                                       |
| getWindowStatus | Get the current application window mode |
| isFullScreen | Determine whether the window is full screen, the default main window.                                                                     |
| isFocused | Determine whether the current window has been focused |
| isTransparent | Whether the window is transparent, the default main window.                                                                       |
| isWindowShowing | Determine whether the current window has been displayed, the default main window.                                                                  |
| isWindowSupportWideGamut | Determine whether the current window supports wide color gamut mode, the default main window.                                                             |
| setDialogBackGestureEnabled | Set whether the modal window responds to gestures and returns an event, and calls to non-modal windows return an error code |
| setGestureBackEnabled | Set whether the return gesture function is disabled in the current window. It only takes effect in full screen mode of the main window, and does not take effect in 2in1 device. <API13+> |
| isGestureBackEnabled | Get whether the return gesture function is disabled in the current window. It only takes effect in full screen mode of the main window, and the 2in1 device does not take effect. <API13+> |
| createWindow | Create a child window or system window and use Promise asynchronous callback.                                                          |
| findWindow | Find the window corresponding to name.                                                                       |
| getLastWindow | Get the topmost subwindow in the current application. If there is no application subwindow, it returns to the application main window.                                                    |
| shiftAppWindowFocus | Transfer window focus from the source window to the target window in the same application, only the focus transfer of the main window and child window of the application is supported.                                              |

## DisplayUtil (screen related tool class)[使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/utils/DisplayUtilPage.ets)

| Methods | Introduction |
|:-----------------------|:--------------------------------------------------------------------------------------------------------------|
| getDefaultDisplaySync | Get the current default display object |
| getPrimaryDisplaySync | Get home screen information. Devices other than 2in1 obtain the Display object with the device's own screen; when the 2in1 device connects to the external screen, it obtains the Display object with the current home screen; when the 2in1 device does not have an external screen, it obtains the Display object with the screen. <API14+> |
| getAllDisplays | Get all current display objects, use Promise asynchronous callback |
| getWidth | Get the screen width of the device in px |
| getHeight | Get the screen height of the device in px |
| getOrientation | Get the current direction of the device |
| getDisplayState | Get the device's status |
| getCutoutRect | Get information on unavailable screen areas such as hole-punch screen, notch screen, waterfall screen, etc. It is recommended to apply layout to avoid this area |
| getCutoutHeight | Get the height of unavailable screen areas such as hole-punch screen, notch screen, unit is px |
| isFoldable | Check if the device is foldable |
| getFoldStatus | Get the current folding status of the foldable device |
| getFoldDisplayMode | Get the display mode of the foldable device |
| onFoldStatusChange | Turn on monitoring of folding state changes in folding device |
| offFoldStatusChange | Turn off monitoring of folding state changes in folding device |
| onFoldAngleChange | Turn on monitoring of folding angle changes in folding device. If it is a bifold shaft device, there are two angle values; when the charging port is facing downward, the folding shaft one and folding shaft two are respectively from right to left.                                                   |
| offFoldAngleChange | Close the monitoring of folding angle changes in folding equipment |
| isCaptured | Check whether the device is taking screenshots, projecting, or recording screens.                                                                                             |
| onCaptureStatusChange | Turn on monitoring of screen capture, projection, and recording status changes.                                                                                          |
| offCaptureStatusChange | Close monitoring of changes in screen capture, projection, and recording status.                                                                                          |

## PermissionUtil (apply for authorization tool category)[使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/utils/PermissionUtilPage.ets)

| Methods | Introduction |
|:-------------------------------|:------------------------------------------------------------------------------------------------------|
| requestPermissionsEasy | Apply for authorization, and apply for authorization to the user again after refusing (apply for permission, it is recommended to use this method).                                                                     |
| checkPermissions | Verify that it is currently authorized |
| checkRequestPermissions | After verifying whether to authorize and apply for authorization |
| requestPermissions | Apply for authorization |
| requestPermissionOnSetting | Secondary application for authorization to the user (single permissions or read and write permission groups, this method is recommended).                                                                      |
| requestPermissionOnSettingEasy | Secondary application for authorization to the user (this method is recommended for multiple permissions).                                                                               |
| requestGlobalSwitch | Used to UIAbility/UIExtensionAbility to pull up the global switch to set the pop-up box. In some cases, recording, taking photos and other functions are disabled. The application can pull up this box and ask the user to agree to enable the corresponding functions. If the current global switch status is on, the pop-up box will not be pulled up. |

## AuthUtil (biological authentication (fingerprint, face, password) tool category for mobile phones)[使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/utils/AuthUtilPage.ets)

| Methods | Introduction |
|:-------------------|:-------------------|
| getAvailableStatus | Query whether the authentication capability of the specified type and level supports |
| onStartEasy | Start Authentication, Use fingerprint and password authentication |
| onStart | Start authentication, user-specified type authentication |
| cancel | cancel |
| generateChallenge | Generate Challenge to prevent replay attacks |
| getErrorMsg | Get error msg |

## NetworkUtil (network-related tool class)[使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/utils/NetworkUtilPage.ets)

| Methods | Introduction |
|:------------------------------------------------------------------|:------------------------------------------------|
| isDefaultNetMetered<br/>isDefaultNetMeteredSync | Check whether the current data traffic usage on the network is metered |
| hasDefaultNet<br/>hasDefaultNetSync | Check whether the default data network is activated |
| getDefaultNet<br/>getDefaultNetSync | Get the default activated data network |
| getAppNet<br/>getAppNetSync | Get App-bound network information |
| getAllNets<br/>getAllNetsSync | Get a list of all connected networks |
| isNetworkAvailable | Determine whether the current device network is available |
| hasNetMobile | Determine whether the current network is a cellular network (mobile network).                            |
| hasNetWiFi | Determine whether the current network is a Wi-Fi network.                               |
| hasNetEthernet | Determine whether the current network is an Ethernet network.                                 |
| hasNetVPN | Determine whether the current network is a VPN network.                                 |
| hasNetBearType | Whether the specified network exists |
| getNetBearTypes | Get the network type, the array only contains one specific network type.                       |
| getNetBearType | Get network type |
| getNetCapabilities<br/>getNetCapabilitiesSync | Get the capability information of the network corresponding to netHandle |
| getConnectionProperties<br/>getConnectionPropertiesSync | Get the connection information of the network corresponding to netHandle |
| getIpAddress | Get the IP address of the current device (after the device is connected to Wi-Fi) |
| register | Subscribe to notifications of specified network status changes, support multi-event listening callbacks |
| unregister | Unsubscribe to notifications about default network status changes |
| isNRSupported | Determine whether the current device supports NR (New Radio). That is 5G.                  |
| isRadioOn | Determine whether Radio is open |
| getPrimarySlotId | Get the index number of the card slot where the main card is located |
| getOperatorName | Get operator name |
| getNetworkState | Get network status |
| getNetworkSelectionMode | Get the current network selection mode |
| getSignalInformation | Get the list of registered network signal strength information corresponding to the specified SIM card slot.                       |
| getNetworkType | Get network type |
| getNetworkTypeStr | Get the network type and return the character type.                                  |
| getDefaultCellularDataSlotId<br/>getDefaultCellularDataSlotIdSync | SIM card to get default mobile data |
| getCellularDataFlowType | Get the up and down state of cellular data services |
| getCellularDataState | Get the connection status of the packet switching domain (PS domain) |
| isCellularDataEnabled<br/>isCellularDataEnabledSync | Check whether cellular data service is enabled |
| isCellularDataRoamingEnabled<br/>isCellularDataRoamingEnabledSync | Check whether cellular data services are enabled |
| getDefaultCellularDataSimId | Get the SIM card ID of the default mobile data. Bind with SIM card, incrementing from 1.                 |
| isSimActive<br/>isSimActiveSync | Get whether the SIM card is activated when the specified card slot is activated |
| hasSimCard<br/>hasSimCardSync | Get whether the SIM card is inserted into the specified card slot |
| getMaxSimCount | Get the number of card slots |
| getSimOperatorNumeric<br/>getSimOperatorNumericSync | Get the home PLMN (Public Land Mobile Network) number of the SIM card in the specified card slot. |
| getSimSpn<br/>getSimSpnSync | Get the service provider name of the SIM card specified in the card slot |
| getSimState<br/>getSimStateSync | Get the SIM card status of the specified card slot |
| getCardType <br/> getCardTypeSync | Get the card type of the SIM card in the specified card slot |

## FileUtil (file operation related tool class)[使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/utils/FileUtilPage.ets)

| Methods | Introduction |
|:-------------------------------------------------|:------------------------------------------------------------------------------------|
| getFilesDirPath | Get the folder path or file path in the file directory |
| getCacheDirPath | Get the folder path or file path in the cache directory |
| getTempDirPath | Get the folder path or file path in the temporary directory |
| hasDirPath | Determine whether it is the complete path |
| getFileUri | Get FileUri through URI or path |
| getFileName | Get file name through URI or path |
| getFilePath | Get file path through URI or path |
| getParentUri | Get the URI of the corresponding file parent directory through URI or path |
| getParentPath | Get the path name of the corresponding file parent directory through a URI or path |
| getUriFromPath | Get file URI in synchronous way |
| getFileExtention | Get file suffix based on file name |
| getFileDirSize | Get the size of all files in the specified folder or the specified file size |
| isFile | Determine whether a file is a normal file |
| isDirectory | Determine whether the file is a directory |
| rename<br/>renameSync | Rename file or folder, use Promise asynchronous callback |
| mkdir<br/>mkdirSync | Create a directory. When recursion is specified as true, you can create a directory at multiple levels |
| rmdir<br/>rmdirSync | Delete the entire directory and use Promise asynchronous callback |
| unlink<br/>unlinkSync | Delete a single file, use Promise asynchronous callback |
| access<br/> accessSync | Check whether the file exists and use Promise asynchronous callback |
| open<br/>openSync | Open file, support using URI to open files |
| read<br/>readSync | Read data from file |
| readText<br/>readTextSync | Read files based on text (that is, directly read the text content of the files) |
| write<br/>writeSync | Write data to file |
| writeEasy | Write data to a file and close the file |
| close<br/>closeSync | Close File |
| listFile<br/>listFileSync | List all file names in the folder, supports recursive listing of all file names (including subdirectories), supports file filtering |
| stat<br/>statSync | Get file detailed attribute information |
| copy | Copy files or directories, support copy progress monitoring |
| copyFile<br/>copyFileSync | Copy File |
| moveFile<br/>moveFileSync | Move File |
| moveDir<br/> moveDirSync | Move the source folder to the destination path |
| truncate<br/>truncateSync | Truncate File |
| lstat<br/>lstatSync | Get link file information |
| fsync<br/>fsyncSync | Synchronize file data |
| fdatasync<br/>fdatasyncSync | Implement file content data synchronization |
| createStream<br/>createStreamSync | Open file stream based on file path |
| fdopenStream<br/>fdopenStreamSync | Open file stream based on file descriptor |
| mkdtemp<br/>mkdtempSync | Create a temporary directory |
| dup | Convert file descriptors to File |
| utimes | Modify file recent access time attributes |
| getFormatFileSize | Format file size |
| persistPermission<br>persistPermissionEasy | PersistPermissionEasy | PersistPermissionEasy | PersistPermissionEasy | PersistPermissionEasy | PersistPermissionEasy | PersistPermissionEasy | PersistPermissionEasy | PersistPermissionEasy | PersistPermissionEasy | PersistPermissionEasy | PersistPermissionEasy (Permission required: ohos.permission.FILE_ACCESS_PERSIST) |
| revokePermission<br>revokePermissionEasy | Unpersistence authorization for multiple selected files or directories uri. (Permission required: ohos.permission.FILE_ACCESS_PERSIST) |
| activatedPermission<br>activatePermissionEasy | Enable permissions that have been persisted authorized, otherwise the permissions that have been persisted authorized cannot be used. (Permission required: ohos.permission.FILE_ACCESS_PERSIST) |
| deactivatePermission<br>deactivatePermissionEasy | Cancel multiple authorized files or directories. (Permission required: ohos.permission.FILE_ACCESS_PERSIST) |
| checkPersistentPermission | Verify the selected multiple file or directory URI persistence authorization. (Permission required: ohos.permission.FILE_ACCESS_PERSIST) |

## ImageUtil (image-related tool class)[使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/utils/ImageUtilPage.ets)

| Methods | Introduction |
|:--------------------------|:----------------------------------|
| base64ToPixelMap | Picture base64 string to PixelMap |
| pixelMapToBase64Str | PixelMap to picture base64 string |
| savePixelMap | Save pixelMap to local |
| saveImageSource | Save ImageSource to local |
| createImageSource | Create image source instance |
| createIncrementalSource | Create an image source instance in incremental way |
| packingFromPixelMap | Picture compression or repackaging, use Promise to return the result |
| packingFromImageSource | Image compression or repackaging, use Promise to return the result |
| packToFileFromPixelMap | Encode the PixelMap image source and package it directly into the file |
| packToFileFromImageSource | Encode the ImageSource image source and package it directly into the file |
| getPixelMapFromMedia | User gets the picture in media under the resource directory PixelMap |
| compressedImage | Image compression |
| compressPhoto | Picture compression, return to the compressed picture file path |

## PreviewUtil (file preview tool class)[使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/utils/PreviewUtilPage.ets)

| Methods | Introduction |
|:--------------------|:-------------------------------------|
| generatePreviewInfo | Build PreviewInfo from file uri |
| openPreview | Open the preview window by passing in file preview information. Repeated calls within 1 second are invalid |
| openPreviewEasy | Open the preview window through the uri of the file. Repeated calls within 1 second are invalid |
| canPreview | Determine whether the file can be previewed based on the uri of the file |
| hasDisplayed | Determine whether the preview window already exists |
| closePreview | Close the preview window, only effective if the preview window exists |
| loadData | Load preview file information. Only effective if the preview window exists |
| loadDataEasy | Load preview file information. Only effective if the preview window exists |
| onSharePreview | Call other app preview files |
| getTypeDescriptor | Get TypeDescriptor (descriptive class for standardized data types) |
| getMimeType | Get file mimeType according to file suffix name |
| getIconFileStr | Get the icon of the corresponding file type according to the file suffix name |

## LocationUtil (positioning tool class (WGS-84 coordinate system))[使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/utils/LocationUtilPage.ets)

| Methods | Introduction |
|:--------------------------------------------|:---------------------------------------------------------------------------|
| isLocationEnabled | Determine whether the location service has been enabled (registered is enabled).                                                      |
| requestLocationPermissions | Apply for positioning permissions |
| getCurrentLocationEasy | Get current location |
| getCurrentLocation | Get current location |
| getLastLocation | Get the last location |
| onLocationChangeEasy | Enable location change subscription and initiate positioning request.                                                          |
| onLocationChange | Enable location change subscription and initiate positioning request |
| offLocationChange | Close the location change subscription and delete the corresponding location request |
| onLocationError | Error codes during subscription continuous positioning |
| offLocationError | Error codes during unsubscribe to continuous positioning |
| onLocationEnabledChange | Subscription Location Service Status Change |
| offLocationEnabledChange | Unsubscribe to location service status changes |
| isGeocoderAvailable | Determine whether geocoding and inverse geocoding services are available |
| getAddressFromLocationName | Geocode, convert geographic description to specific coordinates |
| getGeoAddressFromLocationName | Geocode, converting geographic description into a specific coordinate set |
| getAddressFromLocation | Inverse geocoding, convert coordinates to geographic description |
| getGeoAddressFromLocation | Inverse geocoding, convert coordinates to geodescription collection |
| getCountryCode | Get the current country code |
| calculateDistance | Calculate the straight line distance between these two points in meters |
| calculateDistanceEasy | Calculate the straight line distance between these two points based on the specified two latitude and longitude coordinate points, in meters |
| convertCoordinate<br/>convertCoordinateSync | Coordinate conversion, convert WGS84 coordinate system to GCJ02 coordinate system |
| convertCoordinateEasy | Coordinate conversion, convert WGS84 coordinate system to GCJ02 coordinate system |
| getErrorMsg | Get positioning related error msg |

## LogUtil (log tool class)[使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/utils/LogUtilPage.ets)

| Methods | Introduction |
|:-----------|:---------------------------------------------|
| init | Initialize log parameters (this method is recommended to be called in Ability) |
| setDomain | Set the domain identifier corresponding to the log, the range is 0x0~0xFFFF. (This method is recommended to be called in Ability) |
| setTag | Set the log identifier (this method is recommended to be called in Ability) |
| setShowLog | Whether to print the log (this method is recommended to be called in Ability) |
| setHilog | Log printing method (this method is recommended to be called in Ability) |
| debug | Print DEBUG level log |
| info | Print INFO level log |
| warn | Print WARN level log |
| error | Print ERROR level log |
| fatal | Print FATAL level log |
| print | Print log, no borders.                                    |

## CrashUtil (global exception capture, crash log collection)[使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/utils/CrashUtilPage.ets)

| Methods | Introduction |
|:------------------|:-------------------------------------------------------------------------|
| onHandled | Register an error observer (this method is recommended to be called in Ability). After registration, you can capture the js crash generated by the application, and the process will not exit when the application crashes. Write exception information to local file |
| onDestroy | Log out the error observer |
| isHandled | Determine whether the error observer exists |
| getFilePath | Get the log file path (used to read exception files and export exception files) |
| access | Determine whether the log file exists |
| delete | Delete log file |
| getExceptionJson | Get the JSON string for the exception log |
| getExceptionList | Get collection of exception logs |
| enableAppRecovery | Enable the application recovery function and fill in the parameters in order. After this interface is called, the first Ability supports recovery when the application starts from the initiator.                         |
| restartApp | Restart APP and pull up the first Ability when the application starts. You can use it with the errorManager related interface |
| saveAppState | Save the current App status or actively save the state of Ability, which will be used the next time you resume startup. It can be used with errorManager-related interface |
| setRestartWant | Set the next time you restore the Ability in the scene actively pulling up. This Ability must be the UIAbility under the current package |

## EmitterUtil (Emitter tool class (for inter-thread communication))[使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/utils/EmitterUtilPage.ets)

| Methods | Introduction |
|:-----------------|:--------------------|
| post | Send Event |
| onSubscribe | Subscription Events |
| onceSubscribe | Single subscription specified event |
| unSubscribe | Unsubscribe |
| getListenerCount | Get the number of subscriptions for the specified event |
| on | Subscribe to events, support Callback |
| once | single subscription to specified events, support Callback |
| off | Unsubscribe to event, support Callback |

## WantUtil (Want tool class)[使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/utils/WantUtilPage.ets)

| Methods | Introduction |
|:----------------------|:-------------------------------------------|
| toSetting | Jump the system settings page (used with the URI constants in WantUtil to jump to more settings pages) |
| toAppSetting | Jump to App Settings Page |
| toNotificationSetting | Jump notification settings page |
| toNetworkSetting | Jump to the mobile network settings page |
| toWifiSetting | Jump to WLAN Settings Page |
| toBluetoothSetting | Jump Bluetooth Settings Page |
| toNfcSetting | Jump NFC Settings Page |
| toVolumeSetting | Jump sound and vibration settings page |
| toStorageSetting | Jump Storage Settings Page |
| toBatterySetting | Jump Battery Settings Page |
| toWebBrowser | Pull up the system browser |
| toAppGalleryDetail | Pull up the application details interface corresponding to the application market |
| toFileManagement | Pull up the system file manager |
| startMMS | Pull up the SMS interface and specify the contact person |
| openFile | Call three-party software to open the file |

## KvUtil (key value database tool class)[使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/utils/KvUtilPage.ets)

| Methods | Introduction |
|:-----------------------------------------------------------------|:--------------------------|
| put | Add key-value pairs of the specified type to the database |
| get<br/>getString<br/>getNumber<br/>getBoolean<br/>getUint8Array | Get the value of the specified key |
| delete | Delete data with specified key value from the database |
| putBatch | Batch insert key-value pairs into SingleKVStore database |
| deleteBatch | Batch delete key-value pairs in SingleKVStore database |
| getEntries | Get all key-value pairs that match the specified key prefix |
| backup | Backup database with a specified name |
| restore | Restore | Recover database from specified database file |
| deleteBackup | Delete backup file according to the specified name |
| onDataChange | Subscribe to data change notifications for specified types |
| offDataChange | Unsubscribe to data change notification |

## PreferencesUtil (Preferences tool class)[使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/utils/PreferencesUtilPage.ets)

| Methods | Introduction |
|:------------------------------|:------------------------------------------------------------|
| init | Initialization |
| put<br/>putSync | Cache data |
| get<br/>getSync | Get cached value |
| getString<br/>getStringSync | Get cached value of string type |
| getNumber<br/>getNumberSync | Get cached value of type number |
| getBoolean<br/>getBooleanSync | Get cached value of boolean type |
| has<br/>hasSync | Check whether the cache instance contains the stored key-value pair for the given key |
| getBoolean<br/>getBooleanSync | Get cached value of boolean type |
| delete<br/>deleteSync | Delete cache value |
| clear<br/>clearSync | Clear cache |
| deletePreferences | Remove the specified Preferences instance from the cache. If the Preferences instance has a corresponding persistent file, its persistent file will be deleted at the same time. |
| onChange | Subscribe to data change. After the value of the subscribed Key is changed, the callback callback is triggered after the flush method is executed |
| offChange | Unsubscribe to data changes |
| onDataChange | Accurate subscription data changes. Only after the subscribed key value changes, the callback callback is triggered after the flush method is executed |
| offDataChange | Cancel the exact subscription data change |

## CacheUtil (cache tool class)[使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/utils/CacheUtilPage.ets)

| Methods | Introduction |
|:--------|:-----------|
| has | Whether the cached data exists |
| get | Get the cached data |
| put | Save data into cache |
| remove | Delete the cache corresponding to the key |
| isEmpty | Determine whether the cache is empty |
| clear | Clear cached data |

## LRUCacheUtil (LRUCache Cache Tool Class)[使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/utils/LRUCacheUtilPage.ets)

| Methods | Introduction |
|:---------------|:----------------------|
| getInstance | Get singleton of LRUCacheUtil |
| has | Determine whether the cache corresponding to the key is included |
| get | Get the cache corresponding to the key |
| put | Add cache to lruCache |
| remove | Delete the cache corresponding to the key |
| isEmpty | Determine whether the lruCache cache is empty |
| getCapacity | Get the capacity of the current buffer |
| updateCapacity | Reset the capacity of lruCache |
| clear | Clear cache data and reset lruCache size |

## NotificationUtil (notification tool class)[使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/utils/NotificationUtilPage.ets)

| Methods | Introduction |
|:----------------------------------------------------|:----------------------------|
| setDefaultConfig | Set the default unified configuration for notifications |
| isNotificationEnabled<br/>isNotificationEnabledSync | Query whether the notification is authorized |
| authorizeNotification | Request notification authorization, and the first call will pop up the window for the user to choose.       |
| isSupportTemplate | Check whether the template exists, currently only progress bar templates are supported.        |
| isDistributedEnabled | Query whether the device supports distributed notifications |
| publishBasic | Publish normal text notification |
| publishMultiLine | Publish multi-text notification |
| publishLongText | Publish long text notification |
| publishPicture | Publish notifications with pictures |
| publishTemplate | Publish Template Notification |
| cancel | cancel notice |
| cancelGroup | Cancel notifications under the specified group of this application |
| cancelAll | Cancel All Notifications |
| setBadge | Set the number of desktop angle marks |
| clearBadge | Clear the corner marker on the desktop |
| setBadgeFromNotificationCount | Set the number of desktop corner markers, from the number of notifications |
| getActiveNotificationCount | Get the number of notifications that are not deleted by the current application |
| getActiveNotifications | Get the list of notifications that are not deleted by the current application |
| addSlot | Create a notification channel of a specified type |
| getSlot | Get a notification channel of a specified type |
| getSlots | Get all notification channels for this application |
| removeSlot | Delete notification channel of the type specified by this application |
| removeAllSlots | Delete all notification channels for this application |
| generateNotificationId | Generate notification id (using timestamp as id) |
| getDefaultWantAgent | Create a Want that pulls up Ability |
| getCompressedPicture | Get compressed notification image (the total number of bytes of image pixels cannot exceed 2MB) |
| getCompressedIcon | Get the compressed notification icon (the total number of bytes of the icon pixels does not exceed 192KB) |

## SnapshotUtil (component screenshot and window screenshot tool class)[使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/utils/SnapshotUtilPage.ets)

| Methods | Introduction |
|:-----------------------|:---------------------------------|
| get<br/>getSync | Get screenshots of the loaded component, pass in the component id of the component, find the corresponding component to take screenshots |
| createFromBuilder | Render CustomBuilder custom components in the application background and output their screenshots |
| snapshot | Get window screenshot, use Promise asynchronous callback |
| onSnapshotListener | Turn on monitoring of system screenshot events |
| removeSnapshotListener | Close the monitoring of system screenshot events |

## KeyboardUtil (keyboard tool class)[使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/utils/KeyboardUtilPage.ets)

| Methods | Introduction |
|:-----------------------|:------------------|
| show | Pull up the keyboard |
| hide | Hide keyboard |
| onKeyboardListener | Subscribe to input method soft keyboard to show and hide events |
| removeKeyboardListener | Unsubscribe to input method soft keyboard to show or hide events |

## PasteboardUtil (clipboard tool class)[使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/utils/PasteboardUtilPage.ets)

| Methods | Introduction |
|:----------------------------------------|:--------------------------------------------------|
| requestPermissions | Apply for clipboard permissions |
| getSystemPasteboard | Get System Clipboard Object |
| hasData<br/>hasDataSync | Determine whether there is any content in the system clipboard |
| setData<br/>setDataSync | Write data to the system clipboard |
| getData<br/>getDataSync | Read the system clipboard content |
| setDataText<br/>setDataTextSync | Write plain text data to the system clipboard |
| getDataText<br/>getDataTextSync | Read the plain text content of the system clipboard |
| setDataHtml<br/>setDataHtmlSync | Write HTML data to the system clipboard |
| getDataHtml<br/>getDataHtmlSync | Read system clipboard HTML content |
| setDataUri<br/>setDataUriSync | Write URI data to the system clipboard |
| getDataUri<br/>getDataUriSync | Read the URI content of the system clipboard |
| setDataWant<br/>setDataWantSync | Write Want data to the system clipboard |
| getDataWant<br/>getDataWantSync | Read the Want content of the system clipboard |
| setDataPixelMap<br/>setDataPixelMapSync | Write PixelMap data to the system clipboard |
| getDataPixelMap<br/>getDataPixelMapSync | Read the system clipboard PixelMap content |
| getDataStr<br/>getDataStrSync | Read strings in the system clipboard |
| getDataEasy | Read content in the system clipboard (plain text content, HTML content, URI content, Want content, PixelMap content) |
| clearData<br/>clearDataSync | Clear system clipboard content |

## AssetUtil (key asset storage service tool class)[使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/utils/AssetUtilPage.ets)

| Methods | Introduction |
|:----------------------|:------------|
| add<br/>addSync | Add a key asset |
| get<br/>getSync | Query key assets |
| remove<br/>removeSync | Delete key assets |
| canIUse | Whether the current device supports this module |

## ResUtil (resource tool class)[使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/utils/ResUtilPage.ets)

| Methods | Introduction |
|:----------------------------------------------------|:-------------------------------------------------------------------|
| getResourceManager | Get the ability to provide access to application resources |
| getBoolean | Get the boolean result corresponding to the specified resource |
| getBooleanByName | Get the boolean result corresponding to the specified resource name |
| getNumber | Get the integer value or float value corresponding to the specified resource |
| getNumberByName | Get the integer value or float value corresponding to the specified resource name |
| getStringValue<br/>getStringSync | Get the string corresponding to the specified resource |
| getStringByName<br/>getStringByNameSync | Get the string corresponding to the specified resource name |
| getStringArrayValue<br/>getStringArrayValueSync | Get the string array corresponding to the specified resource |
| getStringArrayByName<br/>getStringArrayByNameSync | Get the string array corresponding to the specified resource name |
| getPluralStringValue<br/>getPluralStringValueSync | Get a single-plural numeric string represented by the specified resource object based on the specified number |
| getPluralStringByName<br/>getPluralStringByNameSync | Get a single-plural numeric string represented by the specified resource name based on the specified number |
| getColor<br/>getColorSync | Get the color value corresponding to the specified resource (decimal) |
| getColorByName<br/>getColorByNameSync | Get the color value corresponding to the specified resource name (decimal) |
| getMediaContent<br/>getMediaContentSync | Get the default or specified screen density media file content corresponding to the specified resource |
| getMediaByName<br/>getMediaByNameSync | Get the default or specified screen density media file content corresponding to the specified resource name |
| getMediaContentBase64<br/>getMediaContentBase64Sync | Get the default or specified screen density picture resource Base64 encoding corresponding to the specified resource ID |
| getMediaBase64ByName<br/>getMediaBase64ByNameSync | Get the default or specified screen density picture resource Base64 encoding corresponding to the specified resource name |
| getRawFileContent<br/>getRawFileContentSync | Get the content of the corresponding rawfile file in the resources/rawfile directory |
| getRawFileContentStr<br/>getRawFileContentStrSync | Get the content of the corresponding rawfile file in the resources/rawfile directory (string) |
| getRawFileList<br/>getRawFileListSync | Get the folder and file list in the resources/rawfile directory (if there is no file in the folder, it will not be returned; if there is a file in the folder, it will return the folder and file list) |
| getRawFd | User obtains the descriptor information of the corresponding rawfile file in the resources/rawfile directory |
| closeRawFd<br/> closeRawFdSync | User closes the descriptor information of the rawfile file in the resources/rawfile directory |
| addResource | When the application runs, load the specified resource path to achieve resource coverage |
| removeResource | When the user runs, remove the specified resource path and restore the resource before it was overwritten |
| isRawDir | The user determines whether the specified path is a directory under rawfile (true: means it is a directory under rawfile, false: means it is not a directory under rawfile) |
| getConfiguration<br/>getConfigurationSync | Get the device's Configuration |
| getDeviceCapability<br/>getDeviceCapabilitySync | Get DeviceCapability for DeviceCapability |

## ObjectUtil (Object Tool Class)[使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/utils/ObjectUtilPage.ets)

| Methods | Introduction |
|-----------------|:---------------------------------|
| getHash | Get the Hash value of the object |
| getClassName | Get the Class name of the object |
| getMethodsNames | Get all method names of the object |
| isString | Determine whether it is a String |
| isNull | Determine whether the object is empty |
| isEmpty | Determine whether the attribute content is empty |
| shallowCopy | shallowCopy |
| deepCopy | Deep Copy Object |
| assign | Merge two or more objects |
| objToClass | obj to class to solve the problem of missing method after obj as class |
| deleteRecord | DeleteElements in Record |
| getValue | Get object value through key |
| setValue | Dynamically add or modify attributes to object obj |

## JSONUtil (JSON tool class)[使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/utils/JSONUtilPage.ets)

| Methods | Introduction |
|:--------------|:---------------|
| jsonToBean | JSON string to object |
| beanToJsonStr | Object to JSON string |
| jsonToArray | JSON string to Array |
| jsonToMap | JSON string to Map |
| mapToJsonStr | Map to JSON string |
| isJSONStr | Determine whether it is a string format json |

## DateUtil (date tool class)[使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/utils/DateUtilPage.ets)

| Methods | Introduction |
|:----------------------|:----------------------------|
| getFormatDate | Get the formatted date and format the incoming date as Date |
| getFormatDateStr | Get the formatted date and format the incoming date into a string of the specified format |
| getToday | Get today's date |
| getTodayTime | Get the timestamp for today |
| getTodayStr | Get the time of today, string type |
| isToday | Determine whether the date is today |
| getNowYear | Get the current year |
| getNowMonth | Get the current month |
| getNowDay | Get Current Day |
| isLeapYear | Determine whether it is a leap year |
| getDaysByYear | Get the number of days in the specified year |
| getDaysByMonth | Get the number of days in the specified month |
| isSameYear | Determine whether two dates are the same year |
| isSameMonth | Determine whether two dates are the same month |
| isSameWeek | Determine whether two dates are the same week |
| isSameDay | Determine whether it is the same day |
| isWeekend | Determine whether the specified date is a weekend in the calendar |
| compareDays | Compare the number of days when the specified date is different |
| compareDate | Compare the number of milliseconds of the specified date |
| getAmountDay | Get the date of the previous or the date of the next |
| getAmountDayStr | Get the date of the previous few days or the date of the next few days, return the string |
| getBeforeDay | Get the previous day date |
| getBeforeDayStr | Get the date of the previous day, return the string |
| getAfterDay | Day after obtain |
| getAfterDayStr | Get the date after the day, return the string |
| getWeekOfMonth | Get what week of the month a given date is |
| getWeekDay | Get the given date is the day of the week |
| getLastDayOfMonth | Get what day the last day of a given year and month |
| getFormatTime | Format Time Date String (DateTimeFormat) |
| getFormatRange | Format time date field string (DateTimeFormat) |
| getFormatRelativeTime | Format Relative Time |
| getTipDateStr | Format timestamps to get prompt time strings |

## Base64Util (Base64 tool class)[使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/utils/Base64UtilPage.ets)

| Methods | Introduction |
|:--------------------------------|:-----------------------------|
| decode<br/>encodeSync | Decode, decode through input parameters and output corresponding Uint8Array object |
| encode<br/>decodeSync | Encoding, output Uint8Array object after inputting parameters |
| encodeToStr<br/>encodeToStrSync | Encode, output the corresponding text after inputting parameters |

## StrUtil (String tool class)[使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/utils/StrUtilPage.ets)

| Methods | Introduction |
|:-------------------|:--------------------------------------|
| isNull | Determine whether the string is empty (undefined, null) |
| isNotNull | Determine whether the string is non-empty |
| isEmpty | Determine whether the string is empty (undefined, null, string length is 0) |
| isNotEmpty | Determine whether the string is non-empty |
| isBlank | Determine whether the string is empty and whitespace (whitespace includes spaces, tabs, full-width spaces and uninterrupted spaces) |
| isNotBlank | Determine whether the string is non-empty |
| trim | Remove spaces at both ends of strings |
| trimAll | Remove all spaces in string |
| replace | replace the matching regular in the string to the given string |
| replaceAll | ReplaceAll | Replace all matching regulars in the string to the given string |
| startsWith | Determine whether a string starts with the given string |
| endsWith | Determine whether a string ends in the given string |
| repeat | repeat string number |
| toLower | Convert the entire string to lowercase |
| toUpper | Convert the entire string to uppercase |
| capitalize | Convert the first letter of the string to uppercase, and the rest to lowercase |
| equal | Determine whether two incoming values ​​or strings are equal |
| notEqual | Determine whether two incoming values ​​or strings are not equal |
| strToUint8Array | String to Uint8Array |
| unit8ArrayToStr | Uint8Array to string |
| strToBase64 | String to Base64 string |
| base64ToStr | Base64 string to string |
| strToBuffer | String to ArrayBuffer |
| bufferToStr | ArrayBuffer to string |
| bufferToUint8Array | ArrayBuffer to Uint8Array |
| unit8ArrayToBuffer | Uint8Array to ArrayBuffer |
| getErrorStr | Get the JSON string of Error |
| getErrnoToString | Get detailed information corresponding to the system error code |

## CharUtil (character tool class)[使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/utils/CharUtilPage.ets)

| Methods | Introduction |
|:-------------|:-------------------------------|
| isDigit | Determine whether the string char is a number |
| isLetter | Determine whether the string char is a letter |
| isLowerCase | Determine whether the string char is a lowercase letter |
| isUpperCase | Determine whether the string char is capital letter |
| isSpaceChar | Determine whether the string char is a space character |
| isWhitespace | Determine whether the string char is a whitespace |
| isRTL | Determine whether the string char is a character from right to left language |
| isIdeograph | Determine whether the string char is an ideographic text |
| isBlankChar | Determine whether there is a blank symbol. White space symbols include spaces, tab characters, full-width spaces and uninterrupted spaces |
| isAscii | Determine whether the character is within the ASCII range (0~127) |

## NumberUtil (number tool class)[使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/utils/NumberUtilPage.ets)

| Methods | Introduction |
|:--------------|:--------------|
| isNaN | Check if the value is NaN |
| isFinite | Check if the value is a finite number |
| isInteger | Check if the value is an integer |
| isSafeInteger | Check if the value is a safe integer |
| isNumber | Determine whether it is a numerical value |
| isEven | Check if the number is even |
| isOdd | Check if the number is odd |
| toNumber | Convert string to Number |
| toInt | Convert string to integer |
| toFloat | Convert string to floating point |
| average | Calculate the average of the numbers |
| add | Add |
| sub | subtraction |
| sum | sum |
| toDecimal | Construct Decimal |
| addDecimal | Addition Decimal |
| subDecimal | Subtraction Decimal |
| sumDecimal | SumDecimal |


## ArrayUtil (collection tool class)[使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/utils/ArrayUtilPage.ets)

| Methods | Introduction |
|:------------|:----------------------------|
| isNotEmpty | Determine whether a collection is a non-empty collection |
| isEmpty | Determine whether a set is an empty set |
| removeEmpty | Remove empty values ​​from string array |
| trim | Removes the spaces before and after each value of the string array |
| distinct | Deduplicate the array, and after deduplicate it, generate a new array, the original array remains unchanged |
| reverse | Inverting the array will modify the original array |
| filter | Array filtering, filtering and returning required elements through filter function implementation |
| append | Splice data, use extension operators, and do not affect the original array.        |
| min | Get the minimum value of the array (value, string, date) |
| max | Get the maximum value of the array (value, string, date) |
| flatten | tiled 2D array |
| union | Tile a 2D array and deduplicate |
| chunk | Array chunking |
| contains | Determine whether the set contains a certain value |
| remove | Remove a value from the collection |

## RandomUtil (random tool class)[使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/utils/RandomUtilPage.ets)

| Methods | Introduction |
|:-------------------------|:----------------------------------------------|
| getRandomBoolean | Generate random Boolean values ​​|
| getRandomInt | Generate random integers (the range can be specified) |
| getRandomNumber | Generate random numbers in a specified range |
| getRandomLimit | Generate random numbers in the specified range [0,limit) |
| getRandomChineseChar | Generate a random Chinese character |
| getRandomChinese | Generate random Chinese characters |
| getRandomStr | Randomgenerates strings of specified length based on the specified string |
| getRandomDataBlob | Generate DataBlob of randomly specified length |
| getRandomUint8Array | Generate Uint8Array of randomly specified length |
| getRandomColor | Generate random colors, hexadecimal |
| generateUUID36 | Generate 36-bit UUID with - |
| generateUUID32 | Generate 32-bit UUID with - |
| generateRandomUUID | Generate a random RFC 4122 version 4 string type UUID using Encrypted Secure Random Number Generator |
| generateRandomBinaryUUID | Generate Random RFC 4122 Version 4 Uint8Array Type UUID using Encrypted Secure Random Number Generator |

## RegexUtil (regular tool class)[使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/utils/RegexUtilPage.ets)

| Methods | Introduction |
|:------------|:----------------------------------|
| isMatch | Whether the given content matches the regular (used with regular constants in RegexUtil) |
| isPhone | Determine whether the incoming phone number is formatted correctly |
| isDigits | Check if the string contains only numeric characters |
| isEmail | Determine whether the incoming email is formatted correctly |
| isEmoji | Determine whether a string contains emoticons |
| isValidCard | Verify the validity of ID number |

## TypeUtil (Type Checking Tool Class)[使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/utils/TypeUtilPage.ets)

| Methods | Introduction |
|:--------------------|:-------------------------------------|
| isBoolean | Determine whether it is Boolean type |
| isNumber | Determine whether it is Number type |
| isString | Determine whether it is String type |
| isObject | Determine whether it is Object type |
| isArray | Determine whether it is an array type |
| isResource | Determine whether it is Resource type |
| isResourceStr | Determine whether it is ResourceStr type |
| isFunction | Determine whether it is a function type |
| isMap | Check if it is Map type |
| isWeakMap | Check if it is WeakMap type |
| isSet | Check whether it is Set type |
| isWeakSet | Check if it is WeakSet type |
| isDate | Check if it is Date type |
| isArrayBuffer | Check whether it is ArrayBuffer type |
| isSharedArrayBuffer | Check if it is SharedArrayBuffer type |
| isAnyArrayBuffer | Check if it is ArrayBuffer or SharedArrayBuffer type |
| isUint8Array | Check if it is a Uint8Array array type |
| isUint16Array | Check if it is a Uint16Array array type |
| isUint32Array | Check if it is a Uint32Array array type |
| isInt8Array | Check if it is an Int8Array array type |
| isInt16Array | Check if it is an Int16Array array type |
| isInt32Array | Check if it is an Int32Array array type |
| isTypedArray | Check if it is TypedArray |
| isAsyncFunction | Check if it is an asynchronous function type |
| isPromise | Check if it is a Promise type |
| isProxy | Check if it is Proxy type |
| isRegExp | Check if it is RegExp type |
| isDataView | Check if it is DataView type |
| isExternal | Check if it is native External type |
| isNativeError | Check if it is Error type |

## FormatUtil (format tool class)[使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/utils/FormatUtilPage.ets)

| Methods | Introduction |
|:---------------------|:----------------------------|
| isPhone | Determine whether the incoming phone number is formatted correctly |
| getPhoneFormat | Format phone numbers |
| getPhoneLocationName | Get phone number home |
| transliterator | Convert input string from source format to target format (convert Chinese characters to pinyin) |
| getFormatPercentage | Format percentage to convert numbers from percentage string |
| getFormatPhone | Format mobile phone number, hide the four middle digits |
| getFormatCardNo | Format ID number, hide the middle part number |
| getFormatFileSize | Format file size |
| getTruncateText | Shorten the long text, the excess is represented by an ellipsis |
| getIconFont | parse iconFont characters |
| getQueryValue | Get the parameters in the url, the value corresponding to the Key |
| getParamsUrl | Splice parameters on the url and return the new url |

## ClickUtil (throttling, anti-shake tool category)[使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/utils/ClickUtilPage.ets)

| Methods | Introduction |
|:---------|:---------------------------------|
| throttle | Throttle: Only trigger once within a certain period of time |
| debounce | Anti-shake: within a certain period of time, only the last operation will be executed, and the function will be executed after waiting milliseconds |

## TempUtil (temperature conversion tool class)[使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/utils/TempUtilPage.ets)

| Methods | Introduction |
|:----|:--------|
| C2F | degrees Celsius to degrees Fahrenheit |
| F2C | Fahrenheit to Celsius |
| C2K | Celsius to Kelvin |
| K2C | Kelvin to Celsius |
| F2K | Fahrenheit to Kelvin |
| K2F | Kelvin to Fahrenheit |

## DialogUtil (pop-up tool class)[使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/utils/DialogUtilPage.ets)

| Methods | Introduction |
|:-------------------|:------------|
| setDefaultConfig | Set default uniform style |
| showConfirmDialog | Show pop-up window (a button) |
| showPrimaryDialog | Show pop-up window (two buttons) |
| showDialog | Display pop-up window (multiple buttons) |
| showActionSheet | List selection pop-up |
| showCalendarPicker | Calendar Selector Popup |
| showDatePicker | Date Sliding Selector Popup |
| showTimePicker | Time Sliding Selector Popup |
| showTextPicker | Text Sliding Selector Popup |

## ToastUtil (toast tool class)[使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/utils/ToastUtilPage.ets)

| Methods | Introduction |
|:-----------------|:-----------------|
| setDefaultConfig | Set default uniform style |
| showToast | Pop up toast, default duration is 2s |
| showShort | Pop up short toast, default duration is: 1.5s |
| showLong | Pop up long toast, default duration is: 10s |

## SM2 (SM2 encryption and decryption)[使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/crypto/SM2Page.ets)

| Methods | Introduction |
|:--------------------------------------------|:------------------------------------------|
| encrypt<br/>encryptSync | Encrypt |
| decrypt<br/>decryptSync | Decrypt |
| generateKeyPair<br/> generateKeyPairSync | GenerateKeyPairKeyPair |
| getConvertKeyPair<br/>getConvertKeyPairSync | Get the converted asymmetric key KeyPair |
| getSM2PubKey | Get the convert SM2 public key, convert the SM2 public key in C1C2C3 format to the ASN.1 format required by Hongmeng |
| getSM2PriKey | Get Convert SM2 Private Key |
| getCipherTextSpec | Get convert SM2 ciphertext format, ASN.1 format to C1C2C3 or C1C3C2 |
| sign<br/>signSync | Sign data |
| verify<br/>verifySync | Verify the data |
| signSegment<br/>signSegmentSync | SegmentSync |
| verifySegment<br/>verifySegmentSync | Perform segment verification of data |

## SM3 (SM3 tool class)[使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/crypto/SM3Page.ets)

| Methods | Introduction |
|:------------------------------------|:--------------|
| digest<br/>digestSync | SM3 Summary |
| digestSegment<br/>digestSegmentSync | SM3 segment summary |
| hmac<br/>hmacSync | SM3 message authentication code calculation |
| hmacSegment<br/>hmacSegmentSync | SM3 message authentication code calculation, segmentation |

## SM4 (SM4 encryption and decryption)[使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/crypto/SM4Page.ets)

| Methods | Introduction |
|:--------------------------------------------|:-------------|
| encrypt<br/>encryptSync | Encrypt |
| decrypt<br/>decryptSync | Decrypt |
| encryptGCM<br/>encryptGCMSync | Encrypt (GCM mode) |
| decryptGCM<br/>decryptGCMSync | Decrypt (GCM mode) |
| encryptCBC<br/>encryptCBCSync | Encrypt (CBC mode) |
| decryptCBC<br/> decryptCBCSync | Decrypt (CBC mode) |
| encryptECB<br/>encryptECBSync | Encrypt (ECB mode) |
| decryptECB<br/>decryptECBSync | Decrypt (ECB mode) |
| encryptGCMSegment<br/>encryptGCMSegmentSync | Encrypt (GCM mode) segmentation |
| decryptGCMSegment<br/> decryptGCMSegmentSync | Decrypt (GCM mode) segmentation |
| generateSymKey<br/> generateSymKeySync | Generate SymKey |

## AES (AES encryption and decryption)[使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/crypto/AESPage.ets)

| Methods | Introduction |
|:--------------------------------------------|:-------------|
| encrypt<br/>encryptSync | Encrypt |
| decrypt<br/>decryptSync | Decrypt |
| encryptGCM<br/>encryptGCMSync | Encrypt (GCM mode) |
| decryptGCM<br/>decryptGCMSync | Decrypt (GCM mode) |
| encryptCBC<br/>encryptCBCSync | Encrypt (CBC mode) |
| decryptCBC<br/> decryptCBCSync | Decrypt (CBC mode) |
| encryptECB<br/>encryptECBSync | Encrypt (ECB mode) |
| decryptECB<br/>decryptECBSync | Decrypt (ECB mode) |
| encryptGCMSegment<br/>encryptGCMSegmentSync | Encrypt (GCM mode) segmentation |
| decryptGCMSegment<br/> decryptGCMSegmentSync | Decrypt (GCM mode) segmentation |
| generateSymKey<br/> generateSymKeySync | Generate SymKey |

## DES (DES encryption and decryption)[使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/crypto/DESPage.ets)

| Methods | Introduction |
|:--------------------------------------|:-------------|
| encrypt<br/>encryptSync | Encrypt |
| decrypt<br/>decryptSync | Decrypt |
| encryptECB<br/>encryptECBSync | Encrypt (ECB mode) |
| decryptECB<br/>decryptECBSync | Decrypt (ECB mode) |
| encryptCBC<br/>encryptCBCSync | Encrypt (CBC mode) |
| decryptCBC<br/> decryptCBCSync | Decrypt (CBC mode) |
| generateSymKey<br/> generateSymKeySync | Generate SymKey |

## RSA (RSA encryption and decryption)[使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/crypto/RSAPage.ets)

| Methods | Introduction |
|:--------------------------------------------|:-----------------------|
| encrypt<br/>encryptSync | Encrypt |
| decrypt<br/>decryptSync | Decrypt |
| encryptSegment<br/>encryptSegmentSync | Encrypt, segmentation |
| decryptSegment<br/>decryptSegmentSync | Decrypt, segmentation |
| generateKeyPair<br/> generateKeyPairSync | GenerateKeyPairKeyPair |
| getConvertKeyPair<br/>getConvertKeyPairSync | Get the converted asymmetric key KeyPair |
| sign<br/>signSync | Sign data |
| verify<br/>verifySync | Verify the data |
| signSegment<br/>signSegmentSync | SegmentSync |
| verifySegment<br/>verifySegmentSync | Perform segment verification of data |
| recover<br/>recoverSync | Sign the data and restore the original data, currently only RSA supports |

## MD5 (MD5 tool class)[使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/crypto/MD5Page.ets)

| Methods | Introduction |
|:------------------------------------|:-----------|
| digest<br/>digestSync | MD5 Summary |
| digestSegment<br/>digestSegmentSync | MD5 abstract, segmentation |
| hmac<br/>hmacSync | Message authentication code calculation |
| hmacSegment<br/>hmacSegmentSync | Message authentication code calculation, segmentation |

## SHA (SHA tool class)[使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/crypto/SHAPage.ets)

| Methods | Introduction |
|:------------------------------------|:-----------|
| digest<br/>digestSync | SHA Summary |
| digestSegment<br/>digestSegmentSync | SHA abstract, segmentation |
| hmac<br/>hmacSync | Message authentication code calculation |
| hmacSegment<br/>hmacSegmentSync | Message authentication code calculation, segmentation |

## ECDSA (ECDSA tool class)[使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/crypto/ECDSAPage.ets)

| Methods | Introduction |
|:------------------------------------|:----------|
| sign<br/>signSync | Sign data |
| verify<br/>verifySync | Verify the data |
| signSegment<br/>signSegmentSync | SegmentSync |
| verifySegment<br/>verifySegmentSync | Perform segment verification of data |

## CryptoUtil (encryption and decryption utility class, used with each encryption module)

| Methods | Introduction |
|:--------------------------------------------|:------------------|
| encrypt<br/>encryptSync | Encrypt |
| decrypt<br/>decryptSync | Decrypt |
| generateSymKey<br/> generateSymKeySync | Generate SymKey |
| getConvertSymKey<br/>getConvertSymKeySync | Get the converted symmetric key SymKey |
| generateKeyPair<br/> generateKeyPairSync | GenerateKeyPairKeyPair |
| getConvertKeyPair<br/>getConvertKeyPairSync | Get the converted asymmetric key KeyPair |
| getPemKeyPair | Get the specified data to generate an asymmetric key |
| generateIvParamsSpec | Generate IvParamsSpec |
| getIvParamsSpec | Get Convert IvParamsSpec |
| generateGcmParamsSpec | GenerateGcmParamsSpec |
| getGcmParamsSpec | Get Convert GcmParamsSpec |
| sign<br/>signSync | Sign data |
| verify<br/>verifySync | Verify the data |
| signSegment<br/>signSegmentSync | SegmentSync |
| verifySegment<br/>verifySegmentSync | Perform segment verification of data |
| dynamicKey<br/>dynamicKeySync | Key Negotiation |
| digest<br/>digestSync | Abstract |
| digestSegment<br/>digestSegmentSync | Abstract, segmentation |
| hmac<br/>hmacSync | Message authentication code calculation |
| hmacSegment<br/>hmacSegmentSync | Message authentication code calculation, segmentation |

## CryptoHelper (encrypted and decrypted data type conversion, used with each encryption module)

| Methods | Introduction |
|:-------------------------|:----------------------|
| strToDataBlob | String to DataBlob |
| dataBlobToStr | DataBlob to String |
| strToUint8Array | String to Uint8Array |
| uint8ArrayToStr | Uint8Array to String |
| getSymKeyDataBlob | Get the key of type DataBlob |
| getKeyDataBlob | Get the public or private key of type DataBlob |
| getRandomUint8Array | Generate random Uint8Array based on the incoming size |
| getUint8ArrayPaddingZero | Uint8Array Zero Operation |
| toHexWithPaddingZero | Zero Compensation Operation |
| stringToHex | string to Hex string |
| uint8ArrayToString | Bytes to Understandable String |

## PickerUtil (photographing, file selection and saving, tool class)[拆分至 picker_utils](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fpicker_utils)

| Methods | Introduction |
|:---------------------|:----------------------------------------------------|
| camera<br>cameraEasy | Call the system camera, take photos, record videos |
| selectPhoto | Pull up the photoPicker interface by selecting mode, users can select one or more pictures/videos |
| savePhoto | Pull up photoPicker in the save mode to save the file name of the picture or video resource. If there are no parameters, the user needs to enter it by default |
| selectDocument | Pull up the documentPicker interface by selecting mode, users can select one or more files |
| saveDocument | Pull up the documentPicker interface through the save mode, and users can save one or more files |
| selectAudio | Pull up the audioPicker interface by selecting mode, users can select one or more audio files |
| saveAudio | Pull up the audioPicker interface through save mode, and users can save one or more audio files |

## PhotoHelper (album related, tool category)[拆分至 picker_utils](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fpicker_utils)

| Methods | Introduction |
|:-----------------------------|:---------------------------------------|
| select<br>selectEasy | Pull up the photoPicker interface by selecting mode, users can select one or more pictures/videos |
| save | Apply for permission to save pictures or videos to the album.                     |
| showAssetsCreationDialog | Pop-up window authorization save, call the interface to pull up the save confirmation pop-up window.                   |
| showAssetsCreationDialogEasy | Pop-up window authorization save, call the interface to pull up the save confirmation pop-up window, and save.               |
| applyChanges | Save security controls, submit media change requests, insert pictures/videos.               |
| getPhotoAsset | Get the PhotoAsset object of the corresponding uri, used to read file information |

## ScanUtil (code tool class (scan code, code image generation, picture identification))[拆分至 picker_utils](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fpicker_utils)

| Methods | Introduction |
|:----------------------|:-------------------------------|
| startScanForResult | Call the default interface to scan the code and use the Promise method to asynchronously return the decoding result |
| generateBarcode | Code diagram generation, use Promise to return the generated code diagram asynchronously |
| decode | Call picture identification and use Promise to return the identification result asynchronously |
| decodeImage | Call image data identification capability, use Promise asynchronous callback to return code identification results |
| onPickerScanForResult | Pull up the gallery through picker and select the picture, and call the picture identification code |
| canIUseScan | Determine whether the current device supports code capabilities |


## Code Example

------

```
import { font, KeyboardAvoidMode, router } from '@kit.ArkUI';
import { AppUtil, LogUtil, StrUtil, ToastUtil } from '@pura/harmony-utils';
import { DescribeBean } from '../../model/DescribeBean';
import { MockSetup } from '@ohos/hamock';
import { TitleBarView } from '../../component/TitleBarView';
import {
  AbilityLifecycleCallback,
  ApplicationStateChangeCallback,
  ConfigurationConstant,
  EnvironmentCallback
} from '@kit.AbilityKit';
import { DialogAction, DialogHelper } from '@pura/harmony-dialog';
import { JSON } from '@kit.ArkTS';
import { Utils } from '../../utils/Utils';

/**
 * APP相关工具类
 */
@Entry
@Component
struct Index {
  private scroller: Scroller = new Scroller();
  @State describe: DescribeBean = router.getParams() as DescribeBean;
  @State mode: number = KeyboardAvoidMode.OFFSET; //上抬模式
  @State bright: number = 0.0; //屏幕亮度值
  @State isKeepScreenOn: boolean = false; //屏幕是否为常亮状态
  @State privacyMode: boolean = false; //是否隐私模式
  @State statusBar: boolean = false;
  @State blGray: boolean = false; //置灰状态
  @State colorMode: ConfigurationConstant.ColorMode = ConfigurationConstant.ColorMode.COLOR_MODE_LIGHT; //深浅色模式
  @State blZhCn: boolean = false; //默认中文

  private applicationStateChangeCallback: ApplicationStateChangeCallback = {
    onApplicationForeground() {
      LogUtil.warn('applicationStateChangeCallback onApplicationForeground');
    },
    onApplicationBackground() {
      LogUtil.warn('applicationStateChangeCallback onApplicationBackground');
    }
  };
  @State callback1: number = -1;
  private environmentCallback: EnvironmentCallback = {
    onConfigurationUpdated(config) {
      LogUtil.warn(`onConfigurationUpdated config:\n${JSON.stringify(config, null)}`);
    },
    onMemoryLevel(level) {
      LogUtil.warn(`onMemoryLevel level: ${level}`);
    }
  };
  @State callback2: number = -1;
  private abilityLifecycleCallback: AbilityLifecycleCallback = {
    onAbilityCreate(ability) {
      LogUtil.info(`AbilityLifecycleCallback onAbilityCreate ability: ${ability}`);
    },
    onWindowStageCreate(ability, windowStage) {
      LogUtil.info(`AbilityLifecycleCallback onWindowStageCreate ability: ${ability}`);
      LogUtil.info(`AbilityLifecycleCallback onWindowStageCreate windowStage: ${windowStage}`);
    },
    onWindowStageActive(ability, windowStage) {
      LogUtil.info(`AbilityLifecycleCallback onWindowStageActive ability: ${ability}`);
      LogUtil.info(`AbilityLifecycleCallback onWindowStageActive windowStage: ${windowStage}`);
    },
    onWindowStageInactive(ability, windowStage) {
      LogUtil.info(`AbilityLifecycleCallback onWindowStageInactive ability: ${ability}`);
      LogUtil.info(`AbilityLifecycleCallback onWindowStageInactive windowStage: ${windowStage}`);
    },
    onWindowStageDestroy(ability, windowStage) {
      LogUtil.info(`AbilityLifecycleCallback onWindowStageDestroy ability: ${ability}`);
      LogUtil.info(`AbilityLifecycleCallback onWindowStageDestroy windowStage: ${windowStage}`);
    },
    onAbilityDestroy(ability) {
      LogUtil.info(`AbilityLifecycleCallback onAbilityDestroy ability: ${ability}`);
    },
    onAbilityForeground(ability) {
      LogUtil.info(`AbilityLifecycleCallback onAbilityForeground ability: ${ability}`);
    },
    onAbilityBackground(ability) {
      LogUtil.info(`AbilityLifecycleCallback onAbilityBackground ability: ${ability}`);
    },
    onAbilityContinue(ability) {
      LogUtil.info(`AbilityLifecycleCallback onAbilityContinue ability: ${ability}`);
    }
  };


  @MockSetup
  mock() {
    this.describe = new DescribeBean("AppUtil", "APP相关工具类");
  }

  build() {
    Column() {
      TitleBarView({ describe: this.describe })
      Divider()
      Scroll(this.scroller) {
        Column({ space: 5 }) {
          Button("isApiSupported()")
            .btnStyle()
            .onClick(async () => {
              let api12 = AppUtil.isApiSupported(12);
              let api15 = AppUtil.isApiSupported(15);
              let api17 = AppUtil.isApiSupported(17);
              let api20 = AppUtil.isApiSupported(20);
              let api22 = AppUtil.isApiSupported(22);
              let api31 = AppUtil.isApiSupported(31);
              let infoStr = `API12: ${api12}\nAPI15: ${api15}\nAPI17: ${api17}\nAPI20: ${api20}\nAPI22: ${api22}\nAPI31: ${api31}`;
              Utils.showSheetText(infoStr);
            })
          Button("getApplicationContext()")
            .btnStyle()
            .onClick(() => {
              let applicationContext = AppUtil.getApplicationContext();
              ToastUtil.showToast("成功获取applicationContext");
            })
          Button("getContext()")
            .btnStyle()
            .onClick(() => {
              let context = AppUtil.getContext();
              ToastUtil.showToast("成功获取上下文");
            })
          Button("getUIContext()")
            .btnStyle()
            .onClick(() => {
              let uiContext = AppUtil.getUIContext();
              ToastUtil.showToast("成功获取UIContext");
            })
          Button("getWindowStage()")
            .btnStyle()
            .onClick(() => {
              let windowStage = AppUtil.getWindowStage();
              LogUtil.error(JSON.stringify(windowStage, null, 2));
              ToastUtil.showToast("成功获取WindowStage");
            })
          Button("getMainWindow()")
            .btnStyle()
            .onClick(() => {
              let mainWindow = AppUtil.getMainWindow();
              LogUtil.error(JSON.stringify(mainWindow, null, 2));
              ToastUtil.showToast("成功获取主窗口");
            })
          Button("getConfiguration()")
            .btnStyle()
            .onClick(() => {
              let config = AppUtil.getConfiguration();
              Utils.showSheetText(JSON.stringify(config, null, 2));
            })
          Button("setGrayScale()")
            .btnStyle()
            .onClick(() => {
              if (!this.blGray) {
                this.blGray = true;
                AppUtil.setGrayScale(1);
                ToastUtil.showToast("一键置灰成功");
              } else {
                this.blGray = false;
                AppUtil.setGrayScale(0);
                ToastUtil.showToast("取消置灰成功");
              }
            })
          Button("setColorMode()")
            .btnStyle()
            .onClick(() => {
              if (this.colorMode !== ConfigurationConstant.ColorMode.COLOR_MODE_LIGHT) {
                this.colorMode = ConfigurationConstant.ColorMode.COLOR_MODE_LIGHT;
                AppUtil.setColorMode(ConfigurationConstant.ColorMode.COLOR_MODE_LIGHT);
              } else {
                this.colorMode = ConfigurationConstant.ColorMode.COLOR_MODE_DARK;
                AppUtil.setColorMode(ConfigurationConstant.ColorMode.COLOR_MODE_DARK);
              }
            })
          Button("getColorMode()")
            .btnStyle()
            .onClick(() => {
              let colorMode = AppUtil.getColorMode();
              ToastUtil.showToast(`应用的颜色模式:${colorMode}`);
            })
          Button("setFont()")
            .btnStyle()
            .onClick(() => {
              font.registerFont({ familyName: 'WCSF', familySrc: $rawfile('wcsf.ttf') });
              AppUtil.setFont('WCSF');
            })
          Button("setFontSizeScale()")
            .btnStyle()
            .onClick(() => {
              AppUtil.setFontSizeScale(2);
            })
          Button("getFontSizeScale()")
            .btnStyle()
            .onClick(() => {
              let fontSizeScale = AppUtil.getFontSizeScale();
              ToastUtil.showToast(`应用字体大小缩放比例:${fontSizeScale}`);
            })
          Button("setLanguage()")
            .btnStyle()
            .onClick(() => {
              if (this.blZhCn) {
                this.blZhCn = false;
                AppUtil.setLanguage('en-us');
              } else {
                this.blZhCn = true;
                AppUtil.setLanguage('zh-cn');
              }
              ToastUtil.showToast("设置成功！");
            })
          Button("getLanguage()")
            .btnStyle()
            .onClick(() => {
              let language = AppUtil.getLanguage();
              ToastUtil.showToast(`应用的语言:${language}`);
            })
          Button("setSupportedProcessCache()")
            .btnStyle()
            .onClick(() => {
              AppUtil.setSupportedProcessCache(true);
              ToastUtil.showToast("设置成功！");
            })
          Button("clearUpApplicationData()")
            .btnStyle()
            .onClick(() => {
              DialogHelper.showAlertDialog({
                content: '是否清理应用本身的数据？',
                primaryButton:'取消',
                secondaryButton:'清理',
                onAction: (action) => {
                  if (action === DialogAction.SURE) {
                    AppUtil.clearUpApplicationData();
                  }
                }
              });
            })
          Button("killAllProcesses()")
            .btnStyle()
            .onClick(() => {
              DialogHelper.showAlertDialog({
                content: '是否终止应用的所有进程？',
                primaryButton:'取消',
                secondaryButton:'终止',
                onAction: (action) => {
                  if (action === DialogAction.SURE) {
                    AppUtil.killAllProcesses();
                  }
                }
              });
            })
          Button("restartApp()")
            .btnStyle()
            .onClick(() => {
              DialogHelper.showAlertDialog({
                autoCancel: false,
                backCancel: false,
                content: '是否重启应用？',
                primaryButton:'取消',
                secondaryButton:'重启',
                onAction: (action) => {
                  if (action === DialogAction.SURE) {
                    AppUtil.restartApp();
                  }
                }
              });
            })
          Button("exit()")
            .btnStyle()
            .onClick(() => {
              DialogHelper.showAlertDialog({
                content: '是否重退出应用？',
                primaryButton:'取消',
                secondaryButton:'退出',
                onAction: (action) => {
                  if (action === DialogAction.SURE) {
                    AppUtil.exit();
                  }
                }
              });
            })
          Button("getRunningProcessInformation()")
            .btnStyle()
            .onClick(async () => {
              let processInformation = await AppUtil.getRunningProcessInformation();
              let jsonStr = JSON.stringify(processInformation, null, 2);
              Utils.showSheetText(jsonStr);
            })
          Button("onApplicationStateChange()")
            .btnStyle()
            .onClick(() => {
              AppUtil.onApplicationStateChange(this.applicationStateChangeCallback);
              DialogHelper.showToast('添加“applicationStateChange”监听成功！');
            })
          Button("offApplicationStateChange()")
            .btnStyle()
            .onClick(() => {
              AppUtil.offApplicationStateChange(this.applicationStateChangeCallback);
              DialogHelper.showToast('移除“applicationStateChange”监听成功！');
            })
          Button("onEnvironment()")
            .btnStyle()
            .onClick(() => {
              this.callback1 = AppUtil.onEnvironment(this.environmentCallback);
              DialogHelper.showToast('添加“environment”监听成功！');
            })
          Button("offEnvironment()")
            .btnStyle()
            .onClick(() => {
              if (this.callback1 !== -1) {
                AppUtil.offEnvironment(this.callback1);
                DialogHelper.showToast('移除“environment”监听成功！');
              }
            })
          Button("onAbilityLifecycle()")
            .btnStyle()
            .onClick(() => {
              this.callback2 = AppUtil.onAbilityLifecycle(this.abilityLifecycleCallback);
              DialogHelper.showToast('添加“abilityLifecycle”监听成功！');
            })
          Button("offAbilityLifecycle()")
            .btnStyle()
            .onClick(() => {
              if (this.callback2 !== -1) {
                AppUtil.offAbilityLifecycle(this.callback2);
                DialogHelper.showToast('移除“abilityLifecycle”监听成功！');
              }
            })
          Button("getKeyboardAvoidMode()")
            .btnStyle()
            .onClick(() => {
              this.mode = AppUtil.getKeyboardAvoidMode();
              ToastUtil.showToast(`当前模式为: ${StrUtil.equal(this.mode, KeyboardAvoidMode.OFFSET) ? "上抬模式" : "压缩模式"}`)
            })
          Button("setKeyboardAvoidMode()")
            .btnStyle()
            .onClick(() => {
              AppUtil.setKeyboardAvoidMode(StrUtil.equal(this.mode, KeyboardAvoidMode.OFFSET) ?
              KeyboardAvoidMode.RESIZE : KeyboardAvoidMode.OFFSET);
              this.mode = AppUtil.getKeyboardAvoidMode();
              ToastUtil.showToast(`设置模式为: ${StrUtil.equal(this.mode, KeyboardAvoidMode.OFFSET) ? "上抬模式" :
                "压缩模式"}`)
            })
          TextInput({ placeholder: '设置模式后点击输入框查看效果' })
            .width("95%")
            .margin({ bottom: 10 })

          Button("isPortrait()")
            .btnStyle()
            .onClick(() => {
              let isPortrait = AppUtil.isPortrait();
              ToastUtil.showToast(`当前是否竖屏: ${isPortrait}`);
            })
          Button("isLandscape()")
            .btnStyle()
            .onClick(() => {
              let isLandscape = AppUtil.isLandscape();
              ToastUtil.showToast(`当前是否横屏: ${isLandscape}`);
            })
          Button("getStatusBarHeight()")
            .btnStyle()
            .onClick(() => {
              let statusBarHeight = AppUtil.getStatusBarHeight();
              ToastUtil.showToast(`状态栏的高度为：${statusBarHeight}px`)
            })
          Button("getNavigationIndicatorHeight()")
            .btnStyle()
            .onClick(() => {
              let indicatorHeight = AppUtil.getNavigationIndicatorHeight();
              ToastUtil.showToast(`底部导航条的高度为：${indicatorHeight}px`)
            })
          Button("setStatusBar()")
            .btnStyle()
            .onClick(() => {
              this.statusBar = this.statusBar ? false : true;
              if (this.statusBar) {
                AppUtil.setStatusBar();
              } else {
                AppUtil.setStatusBar(false, true);
              }
            })
          Button("getBundleInfo()")
            .btnStyle()
            .onClick(async () => {
              let bundleInfo = await AppUtil.getBundleInfo();
              let infoStr = JSON.stringify(bundleInfo, null, 2);
              Utils.showSheetText(infoStr);
            })
          Button("getAppInfoSync()")
            .btnStyle()
            .onClick(() => {
              let appInfo = AppUtil.getAppInfoSync();
              let infoStr = JSON.stringify(appInfo, null, 2);
              Utils.showSheetText(infoStr);
            })
          Button("getSignatureInfo()")
            .btnStyle()
            .onClick(async () => {
              let signatureInfo = await AppUtil.getSignatureInfo();
              let infoStr = JSON.stringify(signatureInfo, null, 2);
              Utils.showSheetText(infoStr);
            })
          Button("getBundleName()\ngetVersionCode()\ngetVersionName()\ngetTargetVersion()\ngetInstallTime()\ngetUpdateTime()\ngetAppProvisionType()\ndebug()")
            .labelStyle({ maxLines: 10 })
            .type(ButtonType.Normal)
            .borderRadius(10)
            .padding({ top: 10, bottom: 10 })
            .btnStyle()
            .onClick(() => {
              let bundleName = AppUtil.getBundleName();
              let versionCode = AppUtil.getVersionCode();
              let versionName = AppUtil.getVersionName();
              let targetVersion = AppUtil.getTargetVersion();
              let infoStr = `bundleName: ${bundleName}\nversionCode: ${versionCode}\nversionName: ${versionName}\ntargetVersion: ${targetVersion}`;
              let installTime = AppUtil.getInstallTime();
              let updateTime = AppUtil.getUpdateTime();
              infoStr = infoStr + `\ninstallTime: ${installTime}\nupdateTime: ${updateTime}`;
              let appProvisionType = AppUtil.getAppProvisionType();
              let debug = AppUtil.debug();
              infoStr = infoStr + `\nappProvisionType: ${appProvisionType}\ndebug: ${debug}`;
              Utils.showSheetText(infoStr);
            })
        }
        .margin({ top: 5, bottom: 5 })
      }
      .layoutWeight(1)
    }
    .width('100%')
    .height('100%')
    .justifyContent(FlexAlign.Start)
    .backgroundColor($r('app.color.main_background'))
  }
}


@Styles
function btnStyle() {
  .width('90%')
  .margin({ top: 10, bottom: 5 })
}
```


## 🍎Contribution code and technology communication

Any problems found during use can be asked[Issue](https://gitee.com/tongyuyan/harmony-utils/issues)Give us;
Of course, we also welcome you to send us a message[PR](https://gitee.com/tongyuyan/harmony-utils/pulls) 。

[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[https://github.com/787107497](https://github.com/787107497)


## 🌏Open Source Protocol

This project is based on[Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0.html), when copying and borrowing codes, please be sure to indicate the source.
