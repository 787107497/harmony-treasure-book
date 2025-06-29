# harmony-dialog(API12+)

## 🏆Introduction and Recommendations

[harmony-dialog](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-dialog)
An extremely simple and easy-to-use zero-invasion pop-up window, which can be easily implemented with just one line of code, and can be easily popped up no matter where you are. It covers
AlertDialog, TipsDialog, ConfirmDialog, SelectDialog, CustomContentDialog, TextInputDialog, TextAreaDialog, BottomSheetDialog, ActionSheetDialog, TextPickerDialog, DatePickerDialog, CustomDialog, BindSheet, LoadingDialog, LoadingProgress, Toast, ToastTip
Various types can meet various pop-up development needs.

[harmony-utils](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)
A HarmonyOS tool library with rich features and extremely easy to use, with the help of many practical tools, is committed to helping developers quickly build Hongmeng applications.


## 🌞Download and install

`ohpm i @pura/harmony-dialog`

OpenHarmony ohpm
For more information, please refer to[如何安装 OpenHarmony ohpm 包](https://ohpm.openharmony.cn/#/cn/help/downloadandinstall)
<br>

## 📚API detailed explanation[预览效果](https://blog.csdn.net/qq_32922545/article/details/144492075)🌞

| DialogHelper Method | Introduction |
|:------------------------|:------------------------------------------------------------------------------------------------------------------|
| setDefaultConfig | Set default uniform style |
| showAlertDialog | Display operation confirmation class pop-up box |
| showConfirmDialog | Display information confirmation class pop-up box |
| showTipsDialog | The display prompt pop-up box is a confirmation box with graphics |
| showSelectDialog | Show Select class pop-up box |
| showTextInputDialog | Show single line text input pop-up box |
| showTextAreaDialog | Show multi-line text input box |
| showCustomContentDialog | Display the pop-up box of the custom content area, and supports defining the button style of the operation area |
| showBottomSheetDialog | Show action panel |
| showActionSheetDialog | Show Action Panel (IOS Style) |
| showTextPickerDialog | Display selector pop-up box; refer to the TextPicker component; cooperate[china_area](https://ohpm.openharmony.cn/#/cn/detail/@nutpi%2Fchina_area)Data selection of provinces, cities and counties in China can be made. |
| showDatePickerDialog | Show date selector pop-up box, in conjunction[harmony-utils](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)The DateUtil tool class uses, formats the date.   |
| showCustomDialog | Show custom popups |
| update | Refresh custom pop-ups |
| isShowing | Is the current pop-up window displayed |
| closeDialog | Close pop-up box |
| showLoadingDialog | Show loading class pop-up box |
| showLoadingProgress | Show progress bar loading box |
| updateLoading | Refresh loading box |
| showBindSheet | Show custom semi-modal |
| updateBindSheet | Refresh custom semi-modal |
| closeBindSheet | Show toast with graphics |
| showToast | Show Toast |
| showToastLong | Show long toast |
| showToastShort | Show short toast |
| showToastTip | Show toast with graphics |
| generateId | GenerateBox ID |

<br/>

| AnimationHelper Method | Introduction |
|:------------------|:----------|
| transitionInUp | InUp animation |
| transitionInDown | InDown Animation |
| transitionInLeft | InLeft Animation |
| transitionInRight | InRight Animation |


## 📚Sample code[使用案例](https://gitee.com/tongyuyan/harmony-utils/blob/master/entry/src/main/ets/pages/index/DialogPage.ets)

```
    //简单初始化（1.0.8版本及以后）
    //必须在UIAbility的onCreate方法里初始化context。
    DialogHelper.setDefaultConfig((config) => {
      config.uiAbilityContext = this.context;
    })
    
    //设置默认的统一配置，在UIAbility的onCreate方法里初始化
    DialogHelper.setDefaultConfig((config) => {
      config.uiAbilityContext = this.context  //必须初始化上下文
      config.autoCancel = true; //点击遮障层时，是否关闭弹窗，true表示关闭弹窗。false表示不关闭弹窗。默认值：true
      config.backCancel = true; //点击返回键或手势返回时，是否关闭弹窗；实现onWillDismiss函数时，该参数不起作用。true表示关闭弹窗。false表示不关闭弹窗。默认值：true。
      config.actionCancel = true; //点击操作按钮时，是否关闭弹窗。false表示不关闭弹窗。默认值：true。
      config.alignment = DialogAlignment.Center; //弹窗的对齐方式。
      config.offset = { dx: 0, dy: 0 }; //弹窗相对alignment所在位置的偏移量。默认值：{ dx: 0, dy: 0 }
      config.maskColor = 0x33000000; //自定义蒙层颜色。默认值 0x33000000
      config.backgroundColor = Color.White; //弹窗背板颜色。默认值：Color.White
      config.backgroundBlurStyle = BlurStyle.COMPONENT_ULTRA_THICK; //弹窗背板模糊材质。默认值：BlurStyle.COMPONENT_ULTRA_THICK
      config.cornerRadius = 20; //设置背板的圆角半径。可分别设置4个圆角的半径。

      config.title = '温馨提示'; //弹框标题
      config.primaryButton = '取消'; //弹框左侧按钮。
      config.secondaryButton = '确定'; //弹框右侧按钮。
      config.imageRes = undefined; //TipsDialog用到，展示的图片。
      config.imageSize = { width: '64vp', height: '64vp' }; //TipsDialog用到，自定义图片尺寸。默认值：64*64vp

      config.loading_loadSize = 60; //加载动画或进度条的大小
      config.loading_loadColor = Color.White; //加载动画或进度条的颜色
      config.loading_content = ''; //加载动画的提示文字
      config.loading_fontSize = 16; //文字大小
      config.loading_fontColor = Color.White; //文字颜色
      config.loading_backgroundColor = '#CC000000'; //背景颜色，八位色值前两位为透明度
      config.loading_borderRadius = 10; //背景圆角
      
      config.picker_textStyle = ; //设置所有选项中除了最上、最下及选中项以外的文本颜色、字号、字体粗细。
      config.picker_selectedTextStylee = ; //设置选中项的文本颜色、字号、字体粗细。
      config.picker_disappearTextStylee = ; //设置所有选项中最上和最下两个选项的文本颜色、字号、字体粗细。
      config.picker_divider: DividerOptions = { strokeWidth: '2px', startMargin: 0, endMargin: 0, color: '#33000000' }; //设置分割线样式，不设置该属性则按“默认值”展示分割线。
      config.picker_canLoop: boolean = true; //设置是否可循环滚动。
      config.picker_titleFontColor = $r("sys.color.ohos_id_picker_title_text_color"); //弹框标题的字体颜色。
      config.picker_titleBackground = "#F9F9F9"; //头部背景颜色
      config.picker_buttonFontColor = $r("sys.color.ohos_id_picker_button_text_color"); //按钮颜色

      config.toast_duration = 2000; //显示时长(1500ms-10000ms)
      config.toast_durationLong = 10000; //显示时长(10000ms)
      config.toast_fontSize = 16; //文字大小
      config.toast_fontColor = Color.White; //文字颜色
      config.toast_backgroundColor = '#CC000000'; //背景颜色，建议八位色值前两位为透明度
      config.toast_borderRadius = 8; //背景圆角
      config.toast_padding = { left: 16, right: 16, top: 12, bottom: 12 }; //Padding
      config.toast_orientation = Orientation.VERTICAL; //吐司布局方向，默认垂直。设置该值时，请重新设置imageSize和margin。
      config.toast_imageSize = { width: 45, height: 45 }; //Tip图片尺寸。垂直默认值：45*45vp，水平建议值：24*24vp。
      config.toast_margin = 10; //吐司的图片与文字间距。
    });
 ```

 ```
    //在子窗口 使用弹框需要传入uiContext
    DialogHelper.showTipsDialog({
      uiContext:this.getUIContext(), //子窗口需要传入UIContext
      content: '想要卸载这个APP嘛?',
      onAction: (action) => {
        ToastUtil.showToast(`${action}`);
      }
    })
 ```

 ```
    //操作确认类弹出框
    DialogHelper.showAlertDialog({
      content: "确定保存该WPS文件吗？",
      onAction: (action) => {
        if (action == DialogAction.CANCEL) {
          ToastUtil.showToast(`您点击了取消按钮`);
        } else if (action == DialogAction.SURE) {
          ToastUtil.showToast(`您点击了确认按钮`);
        }
      }
    })
    

    //信息确认类弹出框
    DialogHelper.showConfirmDialog({
      checkTips: "是否记住密码？",
      content: "您是否退出当前应用",
      onCheckedChange: (check) => {
        ToastUtil.showToast(`${check}`);
      },
      onAction: (action) => {
        ToastUtil.showToast(`${action}`);
      }
    })
    
    
    //提示弹出框
    DialogHelper.showTipsDialog({
      content: '想要卸载这个APP嘛?',
      onAction: (action) => {
        ToastUtil.showToast(`${action}`);
      }
    })
    
    
    //选择类弹出框
    DialogHelper.showSelectDialog({
      radioContent: ["文本菜单选项一", "文本菜单选项二", "文本菜单选项三", "文本菜单选项四", "文本菜单选项五"],
      onCheckedChanged: (index) => {
        ToastUtil.showToast(`${index}`);
      },
      onAction: (action, dialogId, value) => {
        ToastUtil.showToast(`${action} --- ${value}`);
      }
    })
 ```

 ```
    //单行文本输入弹出框
    DialogHelper.showTextInputDialog({
      text: this.inputText,
      onChange: (text) => {
        console.error("onChange: " + text);
      },
      onAction: (action, dialogId, content) => {
        if (action == DialogAction.SURE) {
          this.inputText = content;
        }
      }
    })
    
    
    //多行文本输入弹出框
    DialogHelper.showTextAreaDialog({
      text: this.inputText,
      onChange: (text) => {
        console.error("onChange: " + text);
      },
      onAction: (action, dialogId, content) => {
        if (action == DialogAction.SURE) {
          this.inputText = content;
        }
      }
    })
    
    
    //自定义内容区弹出框
    DialogHelper.showCustomContentDialog({
      contentBuilder: () => {
        this.customTextBuilder("我是一个自定义弹框！")
      },
      onAction: (action) => {
        ToastUtil.showToast(`${action}`);
      }
    })
 ```

 ```
    //动作面板
    DialogHelper.showBottomSheetDialog({
      title: "请选择上传方式",
      sheets: ["相机", "相册", "文件管理器"],
      onAction: (index) => {
        ToastUtil.showToast(`您点击了，${this.menuArray[index]}`);
      }
    })
    
    
    //动作面板（IOS风格）
    DialogHelper.showActionSheetDialog({
      title: "请选择上传方式",
      sheets: ["相机", "相册", "文件管理器"],
      onAction: (index) => {
        ToastUtil.showToast(`您点击了，${this.menuArray[index]}`);
      }
    })
 ```

 ```
    //选择器弹框（TextPickerDialog）
    let areas = AreaHelper.getAreaSync();
    DialogHelper.showTextPickerDialog({
      title: "请选择收货地址",
      range: areas,
      onAction: (action: number, dialogId: string, value: string | string[]) => {
        if (action == DialogAction.SURE) {
          ToastUtil.showToast(`已选择：${value}`);
        }
      }
    })
 ```

 ```
    //日期选择器弹框（DatePickerDialog）
    DialogHelper.showDatePickerDialog({
      dateType: DateType.YmdHm,
      onAction: (action: number, dialogId: string, date: Date): void => {
        if (action == DialogAction.SURE) {
          let dateStr = DateUtil.getFormatDateStr(date, "yyyy-MM-dd HH:mm");
          ToastUtil.showToast(`选中日期：${dateStr}`);
          LogUtil.error(`选中日期：${dateStr}`);
        }
      }
    })
 ```

 ```
    //进度加载类弹出框
    DialogHelper.showLoadingDialog({
      loadType: SpinType.spinP,
      loadColor: Color.White,
      loadSize: 70,
      backgroundColor: '#BB000000',
      content: "加载中…",
      fontSize: 18,
      padding: { top: 30, right: 50, bottom: 30, left: 50 },
      autoCancel: true
     })

    
    //进度条加载弹框
    DialogHelper.showLoadingProgress({ progress: this.progress })
 ```

 ```  
    //吐司
    DialogHelper.showToast("这是一个自定义吐司")
    DialogHelper.showToastLong("这是一个自定义的长吐司呀")
    
    
    //吐司Tip
    DialogHelper.showToastTip({
      message: "操作成功",
      imageRes: $r('sys.media.ohos_ic_public_ok')
    })
 ```

 ```
   //自定义弹窗
    let drawer: DrawerOptions = {
      width: 260,
      msg: "这是一个自定义弹框，DrawerLayout",
      alignment: DialogAlignment.CenterStart,
      offset: { dx: 0, dy: 0 },
      transition: AnimationHelper.transitionInLeft(250)
    }
    DialogHelper.showCustomDialog(wrapBuilder(DrawerBuilder), drawer)
 ```

## 🍎Communication and communication 🙏

Any problems found during use can be asked[Issue](https://gitee.com/tongyuyan/harmony-utils/issues)Give us;
Of course, we also welcome you to send us a message[PR](https://gitee.com/tongyuyan/harmony-utils/pulls) 。

[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[https://github.com/787107497](https://github.com/787107497)


## 🌏Open Source Protocol

This project is based on[Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0.html), when copying and borrowing codes, please be sure to indicate the source.
