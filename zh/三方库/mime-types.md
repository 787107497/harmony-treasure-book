# mime-types (API12+)

## 🏆简介与推荐

[mime-types](https://ohpm.openharmony.cn/#/cn/detail/@nutpi%2Fmime-types)
主要用于处理和确定文件的 MIME 类型。

[harmony-utils](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)
一款功能丰富且极易上手的HarmonyOS工具库，借助众多实用工具类，致力于助力开发者迅速构建鸿蒙应用。

[harmony-dialog](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-dialog)
一款极为简单易用的零侵入弹窗，仅需一行代码即可轻松实现，无论在何处都能够轻松弹出。

## 🌞下载安装

`ohpm i @nutpi/mime-types`

OpenHarmony ohpm
环境配置等更多内容，请参考[如何安装 OpenHarmony ohpm 包](https://ohpm.openharmony.cn/#/cn/help/downloadandinstall)

## 📚API详解 [使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/plug/MimeTypesPage.ets)

| Mime方法名                          | 介绍                                       |
|:---------------------------------|:-----------------------------------------|
| lookup                           | 根据文件名获取MIME类型                            |
| contentType                      | 根据文件名的后缀名获取MIME类型                        |
| extension                        | 根据MIME类型获取文件扩展名                          |
| getFileExtention                 | 根据 文件名/文件path/文件uri/文件url，获取文件后缀名        |
| getIconFileByFileExtension       | 根据文件后缀名获取对应文件类型的图标                       |
| getIconFileByMIMEType            | 根据MIME类型获取对应文件类型的图标                      |
| getTypeDescriptorByFileExtension | 根据文件后缀名，获取TypeDescriptor（标准化数据类型的描述类）    |
| getTypeDescriptorByMIMEType      | 根据文件MIME类型，获取TypeDescriptor（标准化数据类型的描述类） |

## 📚示例代码

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

```
import { router } from '@kit.ArkUI';
import { StrUtil } from '@pura/harmony-utils';
import { Mime } from '@pura/mime-types';
import { TitleBarView } from '../../component/TitleBarView';
import { DescribeBean } from '../../model/DescribeBean';

/**
 * @nutpi/mime-types，使用案例 */
@Entry
@ComponentV2
export struct MimeTypesPage {
  private scroller: Scroller = new Scroller();
  @Local describe: DescribeBean = router.getParams() as DescribeBean;
  @Local txtStr: string = "";
  @Local iconFile1: string = "";
  @Local iconFile2: string = "";


  build() {
    Column() {
      TitleBarView({ describe: this.describe })
      Divider()
      Scroll(this.scroller) {
        Column({ space: 5 }) {
          Button("lookup()")
            .btnStyle()
            .onClick(() => {
              let mimeType1 = Mime.lookup("test.txt");
              let mimeType2 = Mime.lookup("测试文档.doc");
              let mimeType3 = Mime.lookup("应用.apk");
              let mimeType4 = Mime.lookup("一路向西.mp4");
              let mimeType5 = Mime.lookup("嗨歌.mp3");
              this.txtStr = `test.txt：${mimeType1}\n\n测试文档.doc：${mimeType2}\n\n应用.apk：${mimeType3}\n\n一路向西.mp4：${mimeType4}\n\n嗨歌.mp3：${mimeType5}`;
              this.iconFile1 = "";
              this.iconFile2 = "";
            })
          Button("contentType()")
            .btnStyle()
            .onClick(() => {
              let mimeType1 = Mime.contentType("html");
              let mimeType2 = Mime.contentType("jpeg");
              let mimeType3 = Mime.contentType(".ofd");
              let mimeType4 = Mime.contentType(".PDF");
              let mimeType5 = Mime.contentType(".png");
              this.txtStr = `html：${mimeType1}\n\njpeg：${mimeType2}\n\n.ofd：${mimeType3}\n\n.PDF：${mimeType4}\n\n.png：${mimeType5}`;
              this.iconFile1 = "";
              this.iconFile2 = "";
            })
          Button("extension()")
            .btnStyle()
            .onClick(() => {
              let mimeType1 = Mime.extension("image/jpeg");
              let mimeType2 = Mime.extension("image/gif");
              let mimeType3 = Mime.extension("audio/mp3");
              let mimeType4 = Mime.extension("application/pdf");
              let mimeType5 = Mime.extension("application/epub+zip");
              this.txtStr = `image/jpeg：${mimeType1}\n\nimage/gif：${mimeType2}\n\naudio/mp3：${mimeType3}\n\napplication/pdf：${mimeType4}\n\napplication/epub+zip：${mimeType5}`;
              this.iconFile1 = "";
              this.iconFile2 = "";
            })
          Button("getFileExtention()")
            .btnStyle()
            .onClick(() => {
              let mimeType1 = Mime.getFileExtention("test.txt");
              let mimeType2 = Mime.getFileExtention("/downnload/wps/测试文档.doc");
              let mimeType3 = Mime.getFileExtention("https://developer.demo/files/开发说明.PDF");
              this.txtStr = `${mimeType1}\n\n${mimeType2}\n\n${mimeType3}`;
              this.iconFile1 = "";
              this.iconFile2 = "";
            })
          Button("getIconFileByFileExtension()")
            .btnStyle()
            .onClick(() => {
              this.iconFile1 = Mime.getIconFileByFileExtension(".txt");
              this.iconFile2 = Mime.getIconFileByFileExtension("doc");
              this.txtStr = `${this.iconFile1}\n\n${this.iconFile2}`;
            })
          Button("getIconFileByMIMEType()")
            .btnStyle()
            .onClick(() => {
              this.iconFile1 = Mime.getIconFileByMIMEType("application/pdf");
              this.iconFile2 = Mime.getIconFileByMIMEType("image/gif");
              this.txtStr = `${this.iconFile1}\n\n${this.iconFile2}`;
            })

          Blank().layoutWeight(1)

          Image($r(this.iconFile1)).textStyle()
            .visibility(StrUtil.isNotEmpty(this.iconFile1) ? Visibility.Visible : Visibility.None)

          Image($r(this.iconFile2)).textStyle()
            .visibility(StrUtil.isNotEmpty(this.iconFile2) ? Visibility.Visible : Visibility.None)

          Text(this.txtStr)
            .visibility(StrUtil.isNotEmpty(this.txtStr) ? Visibility.Visible : Visibility.None)
            .textStyle()
        }
        .margin({ top: 5, bottom: 5 })
      }
      .layoutWeight(1)
    }
    .width('100%')
    .height('100%')
    .backgroundColor($r('app.color.main_background'))
  }
}


@Styles
function btnStyle() {
  .width('90%')
  .margin({ top: 10, bottom: 5 })
}

@Styles
function textStyle() {
  .width('95%')
  .padding(10)
  .shadow(ShadowStyle.OUTER_DEFAULT_XS)
  .margin({ top: 5, bottom: 10 })
  .border({
    width: 1,
    color: Color.Grey,
    radius: 10,
    style: BorderStyle.Dashed
  })
}
```


## 🍎沟通与交流🙏

使用过程中发现任何问题都可以提 [Issue](https://gitee.com/tongyuyan/harmony-utils/issues) 给我们；   
当然，我们也非常欢迎你给我们发 [PR](https://gitee.com/tongyuyan/harmony-utils/pulls) 。


## 🌏开源协议

本项目基于 [Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0.html) ，在拷贝和借鉴代码时，请大家务必注明出处。
