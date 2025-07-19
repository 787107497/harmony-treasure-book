# SpinKit(API12)

--------------------------------------------------------------------------------

## 🏆Introduction and Recommendations

[SpinKit](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fspinkit)
is a loading animation library for OpenHarmony/HarmonyOS.

[harmony-utils](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)
A HarmonyOS tool library with rich features and extremely easy to use, with the help of many practical tools, is committed to helping developers quickly build Hongmeng applications.

[harmony-dialog](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-dialog)
An extremely simple and easy-to-use zero-invasion pop-up window, which can be easily implemented with just one line of code, and can be easily popped up no matter where you are.

## 📚Download and install

`ohpm i @pura/spinkit`

OpenHarmony ohpm
For more information, please refer to[如何安装 OpenHarmony ohpm 包](https://ohpm.openharmony.cn/#/cn/help/downloadandinstall)

## 📚Result Picture

The renderings are slightly stumbled, please run the source code or add dependencies to view the effect.
![SpinKit](https://wsrv.nl/?url=https://i-blog.csdnimg.cn/img_convert/9dbf847c21a14f327652c75a3a3ea3f4.png)

## 📚SpinKit Component

| Properties | Introduction |
|:----------|:-----------|
| spinType | Animation type |
| spinSize | Animation size, default 60 |
| spinColor | Animation color, default white |

 ```
  SpinKit()
  
  SpinKit({ spinType: SpinType.spinA })
  
  SpinKit({ spinType: SpinType.spinH })
  
  SpinKit({
     spinType: SpinType.spinA,
     spinColor: Color.Pink,
     spinSize: 70
  })
 ```

## Please move the loading box[harmony-dialog](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-dialog)


## Full Code Example

------

```
import { SpinKit, SpinType } from '@pura/spinkit';
import { ComposeTitleBar } from '@kit.ArkUI';

@Entry
@Component
struct Index {
  private scroller: Scroller = new Scroller();

  aboutToAppear(): void {

  }

  build() {
    Column() {
      ComposeTitleBar({
        title: $r('app.string.spin_kit'),
        subtitle: $r('app.string.spinKit_desc'),
      })
      Divider()
      Scroll(this.scroller) {
        Grid() {
          GridItem() {
            SpinKit({ spinType: SpinType.spinA })
          }.aspectRatio(1)
          .backgroundColor($r('app.color.color1'))

          GridItem() {
            SpinKit({ spinType: SpinType.spinB })
          }.aspectRatio(1)
          .backgroundColor($r('app.color.color2'))

          GridItem() {
            SpinKit({ spinType: SpinType.spinC })
          }.aspectRatio(1)
          .backgroundColor($r('app.color.color3'))

          GridItem() {
            SpinKit({ spinType: SpinType.spinD })
          }.aspectRatio(1)
          .backgroundColor($r('app.color.color4'))

          GridItem() {
            SpinKit({ spinType: SpinType.spinE })
          }.aspectRatio(1)
          .backgroundColor($r('app.color.color5'))

          GridItem() {
            SpinKit({ spinType: SpinType.spinF })
          }.aspectRatio(1)
          .backgroundColor($r('app.color.color6'))

          GridItem() {
            SpinKit({ spinType: SpinType.spinG })
          }.aspectRatio(1)
          .backgroundColor($r('app.color.color7'))

          GridItem() {
            SpinKit({ spinType: SpinType.spinH })
          }.aspectRatio(1)
          .backgroundColor($r('app.color.color8'))

          GridItem() {
            SpinKit({ spinType: SpinType.spinI })
          }.aspectRatio(1)
          .backgroundColor($r('app.color.color9'))

          GridItem() {
            SpinKit({ spinType: SpinType.spinJ })
          }.aspectRatio(1)
          .backgroundColor($r('app.color.color10'))

          GridItem() {
            SpinKit({ spinType: SpinType.spinK })
          }.aspectRatio(1)
          .backgroundColor($r('app.color.color11'))

          GridItem() {
            SpinKit({ spinType: SpinType.spinL })
          }.aspectRatio(1)
          .backgroundColor($r('app.color.color12'))

          GridItem() {
            SpinKit({ spinType: SpinType.spinM })
          }.aspectRatio(1)
          .backgroundColor($r('app.color.color13'))

          GridItem() {
            SpinKit({ spinType: SpinType.spinN })
          }.aspectRatio(1)
          .backgroundColor($r('app.color.color14'))

          GridItem() {
            SpinKit({ spinType: SpinType.spinO })
          }.aspectRatio(1)
          .backgroundColor($r('app.color.color15'))

          GridItem() {
            SpinKit({ spinType: SpinType.spinP })
          }.aspectRatio(1)
          .backgroundColor($r('app.color.color14'))

          GridItem() {
            SpinKit({ spinType: SpinType.spinQ })
          }.aspectRatio(1)
          .backgroundColor($r('app.color.color13'))

          GridItem() {
            SpinKit({ spinType: SpinType.spinR })
          }.aspectRatio(1)
          .backgroundColor($r('app.color.color12'))

          GridItem() {
            SpinKit({ spinType: SpinType.spinS })
          }.aspectRatio(1)
          .backgroundColor($r('app.color.color11'))

          GridItem() {
            SpinKit({ spinType: SpinType.spinT })
          }.aspectRatio(1)
          .backgroundColor($r('app.color.color10'))

          GridItem() {
            SpinKit({ spinType: SpinType.spinU })
          }.aspectRatio(1)
          .backgroundColor($r('app.color.color9'))

          GridItem() {
            SpinKit({ spinType: SpinType.spinV })
          }.aspectRatio(1)
          .backgroundColor($r('app.color.color8'))

          GridItem() {
            SpinKit({ spinType: SpinType.spinW })
          }.aspectRatio(1)
          .backgroundColor($r('app.color.color7'))

          GridItem() {
            SpinKit({ spinType: SpinType.spinX })
          }.aspectRatio(1)
          .backgroundColor($r('app.color.color6'))

          GridItem() {
            SpinKit({ spinType: SpinType.spinY })
          }.aspectRatio(1)
          .backgroundColor($r('app.color.color5'))

          GridItem() {
            SpinKit({ spinType: SpinType.spinZ })
          }.aspectRatio(1)
          .backgroundColor($r('app.color.color4'))
        }
        .rowsTemplate('1fr 1fr 1fr 1fr 1fr 1fr 1fr 1fr 1fr')
        .columnsTemplate('1fr 1fr 1fr')
        .columnsGap(0)
        .rowsGap(0)
        .width('100%')
        .aspectRatio(3 / 9)
      }
      .layoutWeight(1)
    }
    .width('100%')
    .height('100%')
    .backgroundColor(Color.White)
  }
}
```


## 💖 Communication and communication 🙏

Any problems found during use can be asked[Issue](https://gitee.com/tongyuyan/harmony-utils/issues)Give us;
Of course, we also welcome you to send us a message[PR](https://gitee.com/tongyuyan/harmony-utils/pulls) 。

[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)  
[https://github.com/787107497](https://github.com/787107497)


## 🌏Open Source Protocol

This project is based on[Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0.html), when copying and borrowing codes, please be sure to indicate the source.

