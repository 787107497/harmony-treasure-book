## 一键置灰通常应用于如下场景

###### 1. 重大悼念活动：

在国家发生重大灾难、事故或举行悼念日等特殊时期，为了表达对逝者的尊重和哀悼，许多 APP 会将界面置灰。例如，在一些地震、空难等灾难事件发生后，以及全国性的哀悼日期间，大量 APP 会响应号召进行一键置灰。这不仅是一种情感上的表达，也是企业和平台社会责任感的体现。

###### 2. 特殊纪念日或主题活动：

某些具有特殊意义的纪念日活动，APP 可能会选择置灰界面来营造特定的氛围。比如在反法西斯战争胜利纪念日等与历史事件相关的日子，一些历史文化类或相关主题的 APP 可能会通过置灰来引导用户关注和铭记这些重要时刻。

###### 3. 模拟特殊视觉效果或用户体验场景：

在一些特定的应用场景中，为了给用户带来独特的视觉感受或模拟特定的情境，APP 会使用置灰功能。例如，在一些电影、电视剧的宣传 APP 中，为了营造出怀旧、复古或特定的剧情氛围，可能会将界面一键置灰，让用户仿佛置身于特定的时代背景中；或者在一些游戏 APP 中，特定的关卡或场景可能需要将界面置灰，以增加游戏的神秘感、紧张感或突出特定的元素。

###### 4. 系统或 APP 维护升级：

当 APP 进行维护、升级或出现故障需要暂停使用时，为了向用户明确提示当前 APP 的不可用状态，可能会将界面置灰，并显示相关的维护提示信息。这样可以避免用户在不知情的情况下继续操作，减少用户的困惑和不满，同时也方便开发团队进行维护工作。

## 实现方案

### 1. 组件通用属性 grayscale

grayscale(value: number) 为组件添加灰度效果。
value，为当前组件添加灰度效果。值定义为灰度转换的比例，入参1.0则完全转为灰度图像，入参0.0则图像无变化，入参在0.0和1.0之间时，效果呈线性变化。（百分比)；默认值：0.0；取值范围：[0.0, 1.0]；说明：设置小于0.0的值时，按值为0.0处理，设置大于1.0的值时，按值为1.0处理。

```js
Image($r('app.media.image')).width('90%').height(30).grayscale(0.7)
Image($r('app.media.image')).width('90%').height(30).grayscale(1)
 
Text('为组件添加灰度效果').fontSize(15).fontColor(0xFF0000).grayscale(1)
```

###### 封装一个通用的置灰组件，所有页面使用该组件包裹。

### 2、窗口属性 setWindowGrayScale

setWindowGrayScale(grayScale: number): Promise<void>
设置窗口灰阶，使用Promise异步回调。该接口需要在调用loadContent()或setUIContent()使窗口加载页面内容后调用。
grayScale，窗口灰阶。该参数为浮点数，取值范围为[0.0, 1.0]。0.0表示窗口图像无变化，1.0表示窗口图像完全转为灰度图像，0.0至1.0之间时效果呈线性变化。

```js
import { BusinessError } from '@kit.BasicServicesKit';

windowClass?.setUIContent('pages/Index', (error: BusinessError) => {
  if (error.code) {
    console.error(`Failed to set the content. Cause code: ${error.code}`);
    return;
  }
  console.info('Succeeded in setting the content.');
  let grayScale: number = 0.5;
  try {
    if (canIUse("SystemCapability.Window.SessionManager")) {
      let promise = windowClass?.setWindowGrayScale(grayScale);
      promise?.then(() => {
        console.info('Succeeded in setting the grayScale.');
      }).catch((err: BusinessError) => {
        console.error(`Failed to set the grayScale. Cause code: ${err.code}, message: ${err.message}`);
      });
    }
  } catch (exception) {
    console.error(`Failed to set the grayScale. Cause code: ${exception.code}, message: ${exception.message}`);
  }
});  
```

### 3、使用工具库[harmony-utils](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)

调用工具类方法，  AppUtil.setGrayScale(1);

```js
AppUtil.setGrayScale(0.7); //设置灰度0.7
AppUtil.setGrayScale(1); //设置全灰
AppUtil.setGrayScale(1, true); //只置灰主窗口

AppUtil.setGrayScale(0); //取消置灰
```


