## One-click graying is usually used in the following scenarios

###### 1. Major memorial activities:

In special times such as major disasters, accidents or memorial days in the country, in order to express respect and condolences for the deceased, many APPs will put the interface in the dust. For example, after some earthquakes, air crashes and other disasters, as well as during national mourning days, a large number of APPs will respond to the call to put aside one-click dust. This is not only an emotional expression, but also a reflection of the social responsibility of enterprises and platforms.

###### 2. Special anniversary or themed event:

For certain anniversary events with special significance, the APP may choose a gray interface to create a specific atmosphere. For example, on days related to historical events such as the Victory Anniversary of the Anti-Fascist War, some historical and cultural apps or related topics may guide users to pay attention and remember these important moments by putting them in the dust.

###### 3. Simulate special visual effects or user experience scenarios:

In some specific application scenarios, in order to bring a unique visual experience to the user or simulate a specific situation, the APP will use the graying function. For example, in some movies and TV series promotional apps, in order to create a nostalgic, retro or specific plot atmosphere, the interface may be placed in one click, making the user feel like he is in a specific era background; or in some game apps, specific levels or scenes may need to be placed in gray to increase the mystery, tension or highlight specific elements of the game.

###### 4. System or APP maintenance and upgrade:

When the APP is maintained, upgraded or failed, in order to clearly prompt the user for unavailability of the APP, the interface may be grayed out and relevant maintenance prompts are displayed. This can prevent users from continuing to operate without knowing it, reduce users' confusion and dissatisfaction, and also facilitate the development team to carry out maintenance work.

## Implementation plan

### 1. Component common attribute grayscale

grayscale(value: number) Adds a grayscale effect to the component.
value, adds a grayscale effect to the current component. The value is defined as the ratio of grayscale conversion. If the parameter is 1.0, it will be completely converted to a grayscale image. If the parameter is 0.0, the image will not change. When the parameter is between 0.0 and 1.0, the effect will change linearly. (Percent); Default value: 0.0; Value range: [0.0, 1.0]; Description: When setting a value less than 0.0, it is processed as 0.0, and when setting a value greater than 1.0, it is processed as 1.0.

```js
Image($r('app.media.image')).width('90%').height(30).grayscale(0.7)
Image($r('app.media.image')).width('90%').height(30).grayscale(1)
 
Text('为组件添加灰度效果').fontSize(15).fontColor(0xFF0000).grayscale(1)
```

###### Encapsulate a common graying component, which is wrapped with all pages.

### 2. Window properties setWindowGrayScale

setWindowGrayScale(grayScale: number): Promise<void>
Set window grayscale and use Promise asynchronous callback. This interface needs to be called after calling loadContent() or setUIContent() to make the window load the page content.
grayScale, window grayscale. This parameter is a floating point number and takes the value range [0.0, 1.0]. 0.0 means that the window image has no change, 1.0 means that the window image is completely converted to a grayscale image, and the effect changes linearly from 0.0 to 1.0.

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

### 3. Use the tool library[harmony-utils](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)

Call the tool class method, AppUtil.setGrayScale(1);

```js
AppUtil.setGrayScale(0.7); //设置灰度0.7
AppUtil.setGrayScale(1); //设置全灰
AppUtil.setGrayScale(1, true); //只置灰主窗口

AppUtil.setGrayScale(0); //取消置灰
```


