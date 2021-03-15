![](https://socialify.git.ci/taseikyo/bili-danmaku-ass/image?forks=1&issues=1&language=1&owner=1&pattern=Brick%20Wall&pulls=1&stargazers=1&theme=Light "将 bilibili 的弹幕转化为 ass 字幕")

<h2 align="center"><img src="https://www.bilibili.com/favicon.ico">将 bilibili 的弹幕转化为 ass 字幕</h2>

## 起因

今天在网页上看视频，老是看一会就卡住了，然后半天不动，于是就把视频下载下来看，但是没弹幕又缺点味道，用 [BiliLocal](https://github.com/AncientLysine/BiliLocal) 看又不能加速，总是不能满足要求。

于是阴差阳错看到这篇博客：[借用 potplayer 播放器，在本地播放 b 站视频也能看弹幕了](https://blog.csdn.net/sushengbuhuo/article/details/108138488)

于是将 xml 格式的弹幕转化为 ass 格式字幕，然后用 potplayer 看视频，还不错，比较 potplayer 可以各种加速减速，就很棒。

问题是通过 [](https://tiansh.github.io/us-danmaku/bilibili/) 转化的字幕用 potplayer 打开有两个问题，一个字体太大，另一个是字幕滑动速度有问题，渲染出来弹幕抖动看不清：

<details>
  <summary>点我看图（36.1M）</summary>

![](bilibili/origin.gif)
</details>

于是自己拿源码来修改，主要就是对 js 文件的 config 对象进行修改，我改动的参数如下：

```JavaScript
var config = {
  'playResX': 1920,        // 屏幕分辨率宽（像素）
  'playResY': 1080,        // 屏幕分辨率高（像素）
  'font_size': 2,          // 字号（比例）
  'r2ltime': 25,           // 右到左弹幕持续时间（秒）
  'fixtime': 8,            // 固定弹幕持续时间（秒）
  'opacity': 0.8,          // 不透明度（比例）
};
```

字体大小是直接修改 `generateASS`  函数中的注释，我将其从 25 改为 35。

改完之后食用就很顺滑了：

<details>
  <summary>点我看图（29.4M）</summary>

![](bilibili/modify.gif)
</details>

## 使用

1.  在线
	- https://taseikyo.github.io/bili-danmaku-ass
1. 离线
	- 下载 zip 解压
	- 双击 "bilibili/index.html"
	- 需要修改的话，修改 "bilibili/bilibili_ASS_Danmaku_Downloader.user.js" 中 `config` 对应的属性即可
