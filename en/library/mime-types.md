# mime-types (API12+)

## 🏆Introduction and Recommendations

[mime-types](https://ohpm.openharmony.cn/#/cn/detail/@nutpi%2Fmime-types)
Mainly used to process and determine the MIME type of files.

[harmony-utils](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)
A HarmonyOS tool library with rich features and extremely easy to use, with the help of many practical tools, is committed to helping developers quickly build Hongmeng applications.

[harmony-dialog](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-dialog)
An extremely simple and easy-to-use zero-invasion pop-up window, which can be easily implemented with just one line of code, and can be easily popped up no matter where you are.

## 🌞Download and install

`ohpm i @nutpi/mime-types`

OpenHarmony ohpm
For more information, please refer to[如何安装 OpenHarmony ohpm 包](https://ohpm.openharmony.cn/#/cn/help/downloadandinstall)

## 📚API detailed explanation[使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/plug/MimeTypesPage.ets)

| Mime method name | Introduction |
|:---------------------------------|:-----------------------------------------|
| lookup | Get MIME type by file name |
| contentType | Get MIME type based on the suffix name of the file name |
| extension | Get file extension based on MIME type |
| getFileExtention | Get file suffix name based on file name/file path/file uri/file url |
| getIconFileByFileExtension | Get the icon of the corresponding file type based on the file suffix name |
| getIconFileByMIMEType | Get the icon of the corresponding file type according to the MIME type |
| getTypeDescriptorByFileExtension | Get TypeDescriptor (a description class for standardized data type) based on file suffix name |
| getTypeDescriptorByMIMEType | Get TypeDescriptor (a description class for standardized data type) according to file MIME type |

## 📚Sample code

```
//根据文件名获取MIME类型
let mimeType1 = Mime.lookup("test.txt");
let mimeType2 = Mime.lookup("测试文档.doc");
let mimeType3 = Mime.lookup("应用.apk");
let mimeType4 = Mime.lookup("一路向西.mp4");
let mimeType5 = Mime.lookup("嗨歌.mp3");


//根据文件名的后缀名获取MIME类型
let mimeType1 = Mime.contentType("html");
let mimeType2 = Mime.contentType("jpeg");
let mimeType3 = Mime.contentType(".ofd");
let mimeType4 = Mime.contentType(".PDF");
let mimeType5 = Mime.contentType(".png");


//根据MIME类型获取文件扩展名
let mimeType1 = Mime.extension("image/jpeg");
let mimeType2 = Mime.extension("image/gif");
let mimeType3 = Mime.extension("audio/mp3");


//根据 文件名/文件path/文件uri/文件url，获取文件后缀名
let mimeType1 = Mime.getFileExtention("test.txt");
let mimeType2 = Mime.getFileExtention("/downnload/wps/测试文档.doc");
let mimeType3 = Mime.getFileExtention("https://developer.demo/files/开发说明.PDF");


//根据文件后缀名获取对应文件类型的图标
let iconFile1 = Mime.getIconFileByFileExtension(".txt");
let iconFile2 = Mime.getIconFileByFileExtension("doc");


//根据MIME类型获取对应文件类型的图标
let iconFile1 = Mime.getIconFileByMIMEType("application/pdf");
let iconFile2 = Mime.getIconFileByMIMEType("image/gif");
```


## 🍎Communication and communication 🙏

Any problems found during use can be asked[Issue](https://gitee.com/tongyuyan/harmony-utils/issues)Give us;
Of course, we also welcome you to send us a message[PR](https://gitee.com/tongyuyan/harmony-utils/pulls) 。


## 🌏Open Source Protocol

This project is based on[Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0.html), when copying and borrowing codes, please be sure to indicate the source.
