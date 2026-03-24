---
layout: post
title: "Lottie 使用指南"
date: 2026-03-24
categories: 前端 可视化
toc: true
toc_sticky: true
---

## 1. 概述

&ensp;&ensp;Lottie 是一个由 Airbnb 开发的库，它可以在 Web、iOS、Android 和 React Native 上渲染 Adobe After Effects 动画。简单来说，设计师可以在 After Effects 中创建精美的动画，然后通过 Bodymovin 插件导出为 JSON 格式，开发者再通过 Lottie 库将这些 JSON 文件渲染成高质量的动画。
<br/>
![lottie效果图](/assets/images/lottie-1.png)

## 2. 为什么使用 Lottie

在传统的 Web 开发中，如果我们想要在网页中展示动画，通常有以下几种方式：
<br/>
●GIF 图片：文件较大，质量较低，无法交互
<br/>
●CSS 动画：适合简单动画，复杂动画难以实现
<br/>
●JavaScript 动画库：如 GSAP，需要手动编写动画代码
<br/>
●视频：文件大，加载慢，不够灵活
<br/>
而 Lottie 提供了一种全新的方式，它具有以下优势：
<br/>
![lottie效果图](/assets/images/lottie-10.png)

## 3. 快速开始

#### 3.1 安装lottie-web

```javascript
# 使用pnpm(推荐)
pnpm add lottie-web
# 使用npm
npm install lottie-web
# 使用yarn
yarn add lottie-web

```

#### 3.2 获取lottie动画文件（JSON格式）

●UI设计师提供
<br/>
●使用在线资源，如[LottieFiles](https://lottiefiles.com/)
<br/>
![lottie效果图](/assets/images/lottie-9.png)
![lottie效果图](/assets/images/lottie-8.png)
![lottie效果图](/assets/images/lottie-7.png)
![lottie效果图](/assets/images/lottie-6.png)
![lottie效果图](/assets/images/lottie-5.png)

#### 3.3 在vue中使用——一个简单的例子

i 准备好一个容器
<br/>
![lottie效果图](/assets/images/lottie-4.png)

ii 引入

```javascript
//全量引入
import lottie from "lottie-web";
//按需引入（推荐）
import { loadAnimation } from "lottie-web/build/player/lottie_svg.min.js";
```

iii 在准备好的容器中使用lottie渲染动画（以按需引入为例）
<br/>
![lottie效果图](/assets/images/lottie-3.png)
<br/>
iv 打开浏览器我们可以看到已经渲染好的动画
<br/>
v 可以动态的控制动画的行为
<br/>
![lottie效果图](/assets/images/lottie-2.png)

## 4. API参考

#### 4.1 属性

| 属性名           | 说明                                                                                        | 类型                | 默认值 |
| ---------------- | ------------------------------------------------------------------------------------------- | ------------------- | ------ |
| animationData    | 非必填，默认密码或者文本                                                                    | `object`            | 必填   |
| loop             | 是否循环播放动画                                                                            | `boolean`           | `true` |
| autoplay         | 是否自动播放动画                                                                            | `Boolean`           | `true` |
| width            | 动画容器宽度                                                                                | `String` / `Number` | `300`  |
| height           | 动画容器高度                                                                                | `String` / `Number` | `300`  |
| speed            | 动画播放速度，`1` 表示正常速度                                                              | `Number`            | `1`    |
| direction        | 动画播放方向，`1` 表示正向，`-1` 表示反向                                                   | `Number`            | `1`    |
| segments         | 播放特定片段，格式为 `[开始帧, 结束帧]`                                                     | `Array`             | `null` |
| initialSegment   | 初始播放片段，格式为 `[开始帧, 结束帧]`                                                     | `Array`             | `null` |
| renderer         | 渲染器类型，可选值：`svg`、`canvas`、`html`                                                 | `String`            | `svg`  |
| rendererSettings | 渲染器设置，详见 [lottie-web](https://airbnb.io/lottie/#/web?id=other-loading-options) 文档 | `Object`            | `{}`   |

#### 4.2 事件

| 事件名        | 参数                               | 说明                                  |
| ------------- | ---------------------------------- | ------------------------------------- |
| complete      | 无                                 | 动画播放完成时触发，当loop为`false`   |
| loopComplete  | 无                                 | 动画循环播放完成时触发,当loop为`true` |
| enterFrame    | `{currentTime,totalTime,...}`      | 进入新帧时触发                        |
| segmentStart  | `{ firstFrame, totalFrames, ... }` | 片段开始播放时触发,当设置帧片段时     |
| loaded_images | 无                                 | 图像加载完成时触发                    |
| DOMLoaded     | 无                                 | DOM加载完成时触发                     |
| destroy       | 无                                 | 动画实例销毁时触发                    |
| error         | `error`                            | 发生错误时触发                        |

#### 4.3 方法

| 方法名         | 参数                                 | 返回值 | 说明                                                                                                                                                                           |
| -------------- | ------------------------------------ | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| play           | 无                                   | 无     | 播放动画                                                                                                                                                                       |
| pause          | 无                                   | 无     | 暂停动画                                                                                                                                                                       |
| stop           | 无                                   | 无     | 停止动画并回到第一帧                                                                                                                                                           |
| goToAndPlay    | `value:Number，isFrame:Boolean`      | 无     | 跳转到指定帧或时间并播放，isFrame为`true`表示帧，为`false`表示时间                                                                                                             |
| goToAndStop    | `value:Number，isFrame:Boolean`      | 无     | 跳转到指定帧或时间并停止，isFrame为`true`表示帧，为`false`表示时间                                                                                                             |
| setSegment     | `startFrame:Number，endFrame:Number` | 无     | 设置播放片段                                                                                                                                                                   |
| playSegments   | `segments:Array,forceFlag:Boolean`   | 无     | 播放指定片段，`segments`可以包含两个数字或者两个数字组成的数组，`forceFlag`表示是否立即强制播放该片段，例：`anim.playSegments([[0,10],[30,45]],true)`//立即播放0-10帧和30-45帧 |
| getDuration    | `inFrames:Boolean=true`              | Number | 获取动画持续时间，inFrames为`true`表示帧，为`false`表示时间                                                                                                                    |
| resetSegments  | 无                                   | 无     | 还原帧段设置                                                                                                                                                                   |
| lottieInstance | 无                                   | 无     | lottie实例                                                                                                                                                                     |
