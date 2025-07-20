# SpinKit(API12)

--------------------------------------------------------------------------------

## 🏆简介与推荐

[SpinKit](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fspinkit)
是一个适用于OpenHarmony/HarmonyOS的加载动画库。

[harmony-utils](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)
一款功能丰富且极易上手的HarmonyOS工具库，借助众多实用工具类，致力于助力开发者迅速构建鸿蒙应用。

[harmony-dialog](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-dialog)
一款极为简单易用的零侵入弹窗，仅需一行代码即可轻松实现，无论在何处都能够轻松弹出。

## 📚下载安装

`ohpm i @pura/spinkit`

OpenHarmony ohpm  
环境配置等更多内容，请参考[如何安装 OpenHarmony ohpm 包](https://ohpm.openharmony.cn/#/cn/help/downloadandinstall)

## 📚效果图

效果图略有卡顿，请运行源码或添加依赖，查看效果。      
![SpinKit](https://wsrv.nl/?url=https://i-blog.csdnimg.cn/img_convert/9dbf847c21a14f327652c75a3a3ea3f4.png)

## 📚SpinKit组件

| 属性        | 介绍         |
|:----------|:-----------|
| spinType  | 动画的类型      |
| spinSize  | 动画的大小，默认60 |
| spinColor | 动画的颜色，默认白色 |

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

## 加载弹框请移步 [harmony-dialog](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-dialog)


## 示例代码

------

```
import { SpinKit, SpinType } from '@pura/spinkit';
import { ComposeTitleBar } from '@kit.ArkUI';
import { ClickUtil, ToastUtil } from '@pura/harmony-utils';
import { DialogHelper } from '@pura/harmony-dialog';

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
        Column({ space: 15 }) {
          Button('加载框样式配置1')
            .fontFamily('MyFont')
            .width('100%')
            .backgroundColor(Color.Grey)
            .shadow(ShadowStyle.OUTER_DEFAULT_MD)
            .onClick(() => {
              DialogHelper.setDefaultConfig((config) => {
                config.loading_loadType = SpinType.spinZ; //动画类型
                config.loading_loadSize = 60; //加载动画或进度条的大小
                config.loading_loadColor = "#0A51E0"; //加载动画或进度条的颜色
                config.loading_content = ''; //加载动画的提示文字
                config.loading_fontSize = 16; //文字大小
                config.loading_fontColor = Color.White; //文字颜色
                config.loading_backgroundColor = '#CC000000'; //背景颜色，八位色值前两位为透明度
                config.loading_borderRadius = 10; //背景圆角
                config.loading_marginTop = 20; //文字与动画的间距
                config.loading_padding = 30; //padding
              })
              ToastUtil.showToast("样式配置成功！");
            })
          Button('加载框样式配置2')
            .fontFamily('MyFont')
            .width('100%')
            .backgroundColor(Color.Grey)
            .shadow(ShadowStyle.OUTER_DEFAULT_MD)
            .onClick(() => {
              DialogHelper.setDefaultConfig((config) => {
                config.loading_loadType = SpinType.spinH; //动画类型
                config.loading_loadSize = 70; //加载动画或进度条的大小
                config.loading_loadColor = Color.Brown; //加载动画或进度条的颜色
                config.loading_content = '努力加载中'; //加载动画的提示文字
                config.loading_fontSize = 16; //文字大小
                config.loading_fontColor = Color.White; //文字颜色
                config.loading_backgroundColor = '#EE000000'; //背景颜色，八位色值前两位为透明度
                config.loading_borderRadius = 12; //背景圆角
                config.loading_marginTop = 20; //文字与动画的间距
                config.loading_padding = { top: 35, right: 45, bottom: 30, left: 45 }; //padding
              })
              ToastUtil.showToast("样式配置成功！");
            })
          Button('加载框，样式一')
            .fontFamily('MyFont')
            .width('100%')
            .fontColor($r('app.color.color_main'))
            .backgroundColor($r('app.color.card_background'))
            .shadow(ShadowStyle.OUTER_DEFAULT_MD)
            .onClick(() => {
              ClickUtil.throttle(() => {
                let dialogId = DialogHelper.showLoadingDialog({ autoCancel: false })
                let timeoutID = setTimeout(() => {
                  DialogHelper.closeDialog(dialogId);
                  clearTimeout(timeoutID);
                }, 15000)
              })
            })
          Button('加载框，样式二')
            .fontFamily('MyFont')
            .width('100%')
            .fontColor($r('app.color.color_main'))
            .backgroundColor($r('app.color.card_background'))
            .shadow(ShadowStyle.OUTER_DEFAULT_MD)
            .onClick(() => {
              ClickUtil.throttle(() => {
                let dialogId = DialogHelper.showLoadingDialog({
                  loadType: SpinType.spinH,
                  autoCancel: false,
                  onDidDisappear: () => {
                    ToastUtil.showToast("加载框关闭了")
                  }
                })
                let timeoutID = setTimeout(() => {
                  DialogHelper.closeDialog(dialogId);
                  clearTimeout(timeoutID);
                }, 15000)
              })
            })
          Button('加载框，样式三')
            .fontFamily('MyFont')
            .width('100%')
            .fontColor($r('app.color.color_main'))
            .backgroundColor($r('app.color.card_background'))
            .shadow(ShadowStyle.OUTER_DEFAULT_MD)
            .onClick(() => {
              ClickUtil.throttle(() => {
                DialogHelper.showLoadingDialog({
                  loadType: SpinType.spinK,
                  loadColor: '#0A66F9',
                  backgroundColor: '#CC000000',
                  maskColor: '#10000000'
                })
              })
            })
          Button('加载框，样式四')
            .fontFamily('MyFont')
            .width('100%')
            .fontColor($r('app.color.color_main'))
            .backgroundColor($r('app.color.card_background'))
            .shadow(ShadowStyle.OUTER_DEFAULT_MD)
            .onClick(() => {
              ClickUtil.throttle(() => {
                DialogHelper.showLoadingDialog({
                  loadType: SpinType.spinB,
                  loadColor: Color.White,
                  autoCancel: true
                })
              })
            })
          Button('加载框，样式五')
            .fontFamily('MyFont')
            .width('100%')
            .fontColor($r('app.color.color_main'))
            .backgroundColor($r('app.color.card_background'))
            .shadow(ShadowStyle.OUTER_DEFAULT_MD)
            .onClick(() => {
              ClickUtil.throttle(() => {
                DialogHelper.showLoadingDialog({
                  loadType: SpinType.spinP,
                  loadColor: Color.White,
                  loadSize: 70,
                  content: '加载中...',
                  fontSize: 18,
                  fontColor: Color.White,
                  backgroundColor: '#BB000000',
                  maskColor: '#33000000',
                  padding: { top: 30, right: 50, bottom: 30, left: 50 },
                  marginTop: 20,
                  autoCancel: true
                })
              })
            })
          Button('加载框，样式六')
            .fontFamily('MyFont')
            .width('100%')
            .fontColor($r('app.color.color_main'))
            .backgroundColor($r('app.color.card_background'))
            .shadow(ShadowStyle.OUTER_DEFAULT_MD)
            .onClick(() => {
              ClickUtil.throttle(() => {
                //自定义文字和加载动画的颜色
                DialogHelper.showLoadingDialog({
                  loadType: SpinType.spinD,
                  content: "努力加载中",
                  loadColor: Color.Red,
                  backgroundColor: '#990000FF',
                  fontColor: Color.Red,
                  fontSize: 18,
                  padding: 30,
                  borderRadius: 10
                })
              })
            })
          Blank().layoutWeight(1)
        }
        .padding({ left: 15, right: 15 })
        Divider()
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


## 💖沟通与交流🙏

使用过程中发现任何问题都可以提 [Issue](https://gitee.com/tongyuyan/harmony-utils/issues)给我们；   
当然，我们也非常欢迎你给我们发 [PR](https://gitee.com/tongyuyan/harmony-utils/pulls) 。

[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)  
[https://github.com/787107497](https://github.com/787107497)


## 🌏开源协议

本项目基于 [Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0.html) ，在拷贝和借鉴代码时，请大家务必注明出处。   

