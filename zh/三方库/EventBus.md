# EventBus

## 🏆简介与推荐

[EventBus](https://ohpm.openharmony.cn/#/cn/detail/@nutpi%2Feventbus) 消息总线，支持Sticky，支持跨APP广播。

[harmony-utils](https://ohpm.openharmony.cn/#/cn/detail/@pura%2Fharmony-utils)
一款功能丰富且极易上手的HarmonyOS工具库，借助众多实用工具类，致力于助力开发者迅速构建鸿蒙应用。


## 🌞下载安装

`ohpm i @nutpi/eventbus`
OpenHarmony ohpm
环境配置等更多内容，请参考[如何安装 OpenHarmony ohpm 包](https://ohpm.openharmony.cn/#/cn/help/downloadandinstall)

## 📚API详解

| EventBus方法   | 介绍       |
|:-------------|:---------|
| on           | 注册事件监听   |
| once         | 注册单次事件监听 |
| off          | 注销事件监听   |
| offAll       | 注销所有事件监听 |
| post         | 发布普通消息   |
| postSticky   | 发布粘性消息   |
| postApp      | 发布跨App消息 |
| getSticky    | 获取粘性事件数据 |
| removeSticky | 移除粘性事件   |

## 📚示例代码

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

## 🍎沟通与交流🙏

使用过程中发现任何问题都可以提 [Issue](https://gitee.com/tongyuyan/harmony-utils/issues)给我们；   
当然，我们也非常欢迎你给我们发 [PR](https://gitee.com/tongyuyan/harmony-utils/pulls) 。

## 🌏开源协议

本项目基于 [Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0.html) ，在拷贝和借鉴代码时，请大家务必注明出处。
