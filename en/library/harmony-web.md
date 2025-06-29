# harmony-web (API12)

## 🏆Introduction and Recommendations

[harmony-web](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-web)It is a WebView based on Hongmeng
The powerful and extremely easy-to-use library is not only lightweight, flexible and flexible, but also provides a series of problem solutions for Hongmeng WebView, helping developers to easily deal with various development challenges.

[harmony-utils](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)
A HarmonyOS tool library with rich features and extremely easy to use, with the help of many practical tools, is committed to helping developers quickly build Hongmeng applications.

[harmony-dialog](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-dialog)
An extremely simple and easy-to-use zero-invasion pop-up window, which can be easily implemented with just one line of code, and can be easily popped up no matter where you are.

## 🌞Download and install

`ohpm i @pura/harmony-web`

OpenHarmony ohpm
For more information, please refer to[如何安装 OpenHarmony ohpm 包](https://ohpm.openharmony.cn/#/cn/help/downloadandinstall)
<br>


## 📚 ***ArkWeb*** Component, Parameter Description

| Name | Type | Description | Required |
|:------------|:----------------------------|:-------------|:-----|
| controller | webview.WebviewController | Controller | Y |
| src | ResourceStr | Web Resource Address | Y |
| options | ArkWebOptions | ArkWeb property parameters | N |
| webClient | ArkWebClient | ArkWeb Lifecycle Events | N |
| arkJsObject | ArkJsObject or ArkJsObject[] | Interface object that needs to be registered | N |

## 📚 ArkWebHelper, method description

| Method name | Introduction |
|:-------------------|:----------------------|
| init | Initialization |
| prepareForPageLoad | Pre-connect url, call this API before loading the url |

## 📚Sample code

```
@Entry
@ComponentV2
struct Index {
  private controller: webview.WebviewController = new webview.WebviewController();
  @Local webUrl: string = "";
  @Local options: ArkWebOptions = new ArkWebOptions();
  @Local webClient: MyWebClient = new MyWebClient();
  @Local jsObject: MyJsObject = new MyJsObject();

  onBackPress(): boolean {
    if (this.controller?.accessBackward()) {
      this.controller?.backward();
      return true;
    }
    return false;
  }

  aboutToAppear(): void {
    let params: Params = router.getParams() as Params;
    this.webUrl = params.webUrl;
  }

  build() {
    Column() {
      ArkWeb({
        controller: this.controller,
        src: this.webUrl,
        options: this.options,
        webClient: this.webClient,
        arkJsObject: this.jsObject
      })
    }
    .height('100%')
    .width('100%')
  }

}
```

## 🍎Communication and communication 🙏

Any problems found during use can be asked[Issue](https://gitee.com/tongyuyan/harmony-utils/issues)Give us;
Of course, we also welcome you to send us a message[PR](https://gitee.com/tongyuyan/harmony-utils/pulls) 。

[https://gitee.com/tongyuyan/harmony-utils](https://gitee.com/tongyuyan/harmony-utils)   
[https://github.com/787107497](https://github.com/787107497)


## 🌏Open Source Protocol

This project is based on[Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0.html), when copying and borrowing codes, please be sure to indicate the source.
