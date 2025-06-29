# picker_utils (API12+)

## 🏆Introduction and Recommendations

[picker_utils](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fpicker_utils)
yes[harmony-utils](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)
A split sub-store includes PickerUtil, PhotoHelper, and ScanUtil.
Main solution: When using the harmony-utils three-party library and without using picker capabilities, there is no need to declare camera permissions and storage permissions in the privacy policy.

## 🌞Download and install

`ohpm i @pura/picker_utils`

OpenHarmony ohpm
For more information, please refer to[如何安装 OpenHarmony ohpm 包](https://ohpm.openharmony.cn/#/cn/help/downloadandinstall)
<br>

## 📚API detailed explanation[使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/plug/MimeTypesPage.ets)

## 📂Module Introduction

| Module | Introduction |
|:------------|:-------------------------|
| PickerUtil | Photos, files (files, pictures, videos) selection and saving, tools |
| PhotoHelper | Album related tools |
| ScanUtil | Code tool category (scan code, code image generation, picture identification) |

## PickerUtil (photographing, file selection and saving, tool class)[使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/utils/PickerUtilPage.ets)

| Methods | Introduction |
|:---------------------------------|:----------------------------------------------------|
| camera<br>cameraEasy | Call the system camera, take photos, record videos |
| selectPhoto | Pull up the photoPicker interface by selecting mode, users can select one or more pictures/videos |
| savePhoto | Pull up photoPicker in the save mode to save the file name of the picture or video resource. If there are no parameters, the user needs to enter it by default |
| selectDocument | Pull up the documentPicker interface by selecting mode, users can select one or more files |
| saveDocument<br>saveDocumentEasy | Pull up the documentPicker interface through the save mode, and the user can save one or more files |
| selectAudio | Pull up the audioPicker interface by selecting mode, users can select one or more audio files |
| saveAudio | Pull up the audioPicker interface through save mode, and users can save one or more audio files |

## PhotoHelper (album related, tool category)[使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/utils/PhotoHelperPage.ets)

| Methods | Introduction |
|:-----------------------------|:---------------------------------------|
| select<br>selectEasy | Pull up the photoPicker interface by selecting mode, users can select one or more pictures/videos |
| save | Apply for permission to save pictures or videos to the album.                     |
| showAssetsCreationDialog | Pop-up window authorization save, call the interface to pull up the save confirmation pop-up window.                   |
| showAssetsCreationDialogEasy | Pop-up window authorization save, call the interface to pull up the save confirmation pop-up window, and save.               |
| applyChanges | Save security controls, submit media change requests, insert pictures/videos.               |
| getPhotoAsset | Get the PhotoAsset object of the corresponding uri, used to read file information |

## ScanUtil (code tool class (scan code, code image generation, picture identification))[使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/utils/ScanUtilPage.ets)

| Methods | Introduction |
|:----------------------|:-------------------------------|
| startScanForResult | Call the default interface to scan the code and use the Promise method to asynchronously return the decoding result |
| generateBarcode | Code diagram generation, use Promise to return the generated code diagram asynchronously |
| decode | Call picture identification and use Promise to return the identification result asynchronously |
| decodeImage | Call image data identification capability, use Promise asynchronous callback to return code identification results |
| onPickerScanForResult | Pull up the gallery through picker and select the picture, and call the picture identification code |
| canIUseScan | Determine whether the current device supports code capabilities |

## 🍎Communication and communication 🙏

Any problems found during use can be asked[Issue](https://gitee.com/tongyuyan/harmony-utils/issues)Give us;
Of course, we also welcome you to send us a message[PR](https://gitee.com/tongyuyan/harmony-utils/pulls) 。


## 🌏Open Source Protocol

This project is based on[Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0.html), when copying and borrowing codes, please be sure to indicate the source.
