# EventBus

## 🏆Introduction and Recommendations

[EventBus](https://ohpm.openharmony.cn/#/cn/detail/@nutpi%2Feventbus) Message bus, supports Sticky, supports cross-APP broadcasting.

[harmony-utils](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils) A HarmonyOS tool library with rich features and extremely easy to use, with the help of many practical tools, is committed to helping developers quickly build Hongmeng applications.


## 🌞Download and install

`ohpm i @nutpi/eventbus`
OpenHarmony ohpm
For more information, please refer to[如何安装 OpenHarmony ohpm 包](https://ohpm.openharmony.cn/#/cn/help/downloadandinstall)

## 📚API detailed explanation

| EventBus method | Introduction |
|:-------------|:---------|
| on | Register Event Listening |
| once | Register a single event listening |
| off | Logout event listening |
| offAll | Log out all event listening |
| post | Post regular news |
| postSticky | Post sticky news |
| postApp | Publish cross-app messages |
| getSticky | Get sticky event data |
| removeSticky | Remove sticky events |

## 📚Sample code

```
//注册事件监听
EventBus.on('id', (id: string) => {
  ToastUtil.showToast(`ID: ${id}`);
});

//注册单次事件监听
EventBus.once('id', (id: string) => {
  ToastUtil.showToast(`单次ID: ${id}`);
});


//发布普通消息
EventBus.post('id', '100001200');

//发布粘性消息
EventBus.postSticky('id', '100001201');

//发布跨App消息
EventBus.postApp('id', '100001202');


//获取粘性事件数据
let sticky = EventBus.getSticky('id');
ToastUtil.showToast(`粘性事件数据：${sticky}`);

//移除粘性事件
EventBus.removeSticky('id');
ToastUtil.showToast(`移除粘性事件成功！`);


//注销事件监听
EventBus.off('id');

//注销所有事件监听
EventBus.offAll();
```

## Full Code Example

------

```
import { router } from '@kit.ArkUI';
import { TitleBarView } from '../../component/TitleBarView';
import { DescribeBean } from '../../model/DescribeBean';
import { EventBus } from '@nutpi/eventbus';
import { ToastUtil } from '@pura/harmony-utils';
import { DialogHelper } from '@pura/harmony-dialog';

/**
 * @nutpi/eventbus，使用案例
 */
@Entry
@ComponentV2
export struct EventBusPage {
  private scroller: Scroller = new Scroller();
  @Local describe: DescribeBean = router.getParams() as DescribeBean;
  @Local txtStr: string = "";

  build() {
    Column() {
      TitleBarView({ describe: this.describe })
      Divider()
      Scroll(this.scroller) {
        Column({ space: 5 }) {
          Button("on()")
            .btnStyle()
            .onClick(() => {
              //注册事件监听
              EventBus.on('id', (id: string) => {
                DialogHelper.showAlertDialog({
                  autoCancel: false,
                  backCancel: false,
                  content: `ID: ${id}`,
                  primaryButton: '已收到',
                  onAction: (action, id) => {
                    DialogHelper.closeDialog(id);
                  }
                });
              });
              ToastUtil.showToast(`注册事件监听成功！`);
            })
          Button("once()")
            .btnStyle()
            .onClick(() => {
              //注册单次事件监听
              EventBus.once('id', (id: string) => {
                DialogHelper.showAlertDialog({
                  autoCancel: false,
                  backCancel: false,
                  content: `单次ID: ${id}`,
                  primaryButton: '已收到',
                  onAction: (action, id) => {
                    DialogHelper.closeDialog(id);
                  }
                });
              });
              ToastUtil.showToast(`注册单次事件监听成功！`);
            })
          Button("post()")
            .btnStyle()
            .onClick(() => {
              EventBus.post('id', '100001200');
              ToastUtil.showToast(`发布普通消息！`);
            })
          Button("postSticky()")
            .btnStyle()
            .onClick(() => {
              EventBus.postSticky('id', '100001201');
              ToastUtil.showToast(`发布粘性消息！`);
            })
          Button("getSticky()")
            .btnStyle()
            .onClick(() => {
              let sticky = EventBus.getSticky('id');
              ToastUtil.showToast(`粘性事件数据：${sticky}`);
            })
          Button("removeSticky()")
            .btnStyle()
            .onClick(() => {
              EventBus.removeSticky('id');
              ToastUtil.showToast(`移除粘性事件成功！`);
            })
          Button("postApp()")
            .btnStyle()
            .onClick(() => {
              EventBus.postApp('id', '100001202');
              ToastUtil.showToast(`发布跨App消息！`);
            })
          Button("off()")
            .btnStyle()
            .onClick(() => {
              //注销事件监听
              EventBus.off('id');
              ToastUtil.showToast(`注销事件监听！`);
            })
          Button("offAll()")
            .btnStyle()
            .onClick(() => {
              //注销所有事件监听
              EventBus.offAll();
              ToastUtil.showToast(`注销所有事件监听！`);
            })

          Blank().layoutWeight(1)
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
```


## 🍎Communication and communication 🙏

Any problems found during use can be asked[Issue](https://gitee.com/tongyuyan/harmony-utils/issues)Give us;
Of course, we also welcome you to send us a message[PR](https://gitee.com/tongyuyan/harmony-utils/pulls) 。

## 🌏Open Source Protocol

This project is based on[Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0.html), when copying and borrowing codes, please be sure to indicate the source.
