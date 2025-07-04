<div align="center">

<img width="200" src="https://s3-eu-west-1.amazonaws.com/static.playcanvas.com/platform/images/logo/playcanvas-logo-medium.png"/>

# PlayCanvas WebGL 游戏引擎

[API 参考文档](https://api.playcanvas.com/engine/) | [用户手册](https://developer.playcanvas.com) | [示例](https://playcanvas.github.io) | [论坛](https://forum.playcanvas.com) | [博客](https://blog.playcanvas.com)

PlayCanvas 是一款开源游戏引擎。它使用 HTML5 和 WebGL 技术，可在任何移动设备或桌面浏览器中运行游戏及其他交互式 3D 内容。

[![NPM 版本][npm-badge]][npm-url]
[![最小压缩包大小][minzip-badge]][minzip-url]
[![问题平均解决时间][resolution-badge]][isitmaintained-url]
[![未解决问题比例][open-issues-badge]][isitmaintained-url]
[![Twitter][twitter-badge]][twitter-url]

[English](https://github.com/playcanvas/engine/blob/dev/README.md)
[中文](https://github.com/playcanvas/engine/blob/dev/README-zh.md)
[日本語](https://github.com/playcanvas/engine/blob/dev/README-ja.md)
[한글](https://github.com/playcanvas/engine/blob/dev/README-kr.md)

## 项目展示

已有[众多游戏和应用](https://github.com/playcanvas/awesome-playcanvas)基于 PlayCanvas 引擎发布。以下是部分精选案例：

[![Seemore](https://s3-eu-west-1.amazonaws.com/images.playcanvas.com/projects/14705/319531/O4J4VU-image-25.jpg)](https://playcanv.as/p/MflWvdTW/) [![洪水之后](https://s3-eu-west-1.amazonaws.com/images.playcanvas.com/projects/14928/440410/98554E-image-25.jpg)](https://playcanv.as/p/44MRmJRU/) [![赌场](https://s3-eu-west-1.amazonaws.com/images.playcanvas.com/projects/14928/349824/U88HJQ-image-25.jpg)](https://playcanv.as/p/LpmXGUe6/)  
[![Swooop](https://s3-eu-west-1.amazonaws.com/images.playcanvas.com/projects/12/4763/TKYXB8-image-25.jpg)](https://playcanv.as/p/JtL2iqIH/) [![开发弓箭手](https://s3-eu-west-1.amazonaws.com/images.playcanvas.com/projects/12/415995/10A5A9-image-25.jpg)](https://playcanv.as/p/JERg21J8/) [![飞扬的小鸟](https://s3-eu-west-1.amazonaws.com/images.playcanvas.com/projects/8/375389/23PRTL-image-25.jpg)](https://playcanv.as/p/2OlkUaxF/)  
[![汽车](https://s3-eu-west-1.amazonaws.com/images.playcanvas.com/projects/12/347824/7ULQ3Y-image-25.jpg)](https://playcanv.as/p/RqJJ9oU9/) [![星爵](https://s3-eu-west-1.amazonaws.com/images.playcanvas.com/projects/12/333626/BGQN9H-image-25.jpg)](https://playcanv.as/p/SA7hVBLt/) [![全局光照](https://s3-eu-west-1.amazonaws.com/images.playcanvas.com/projects/4373/625081/6AB32D-image-25.jpg)](https://playcanv.as/p/ZV4PW6wr/ )

你可以在 [PlayCanvas 官网](https://playcanvas.com/explore) 查看更多游戏。

</div>

## 用户群体

PlayCanvas 被游戏、广告和可视化领域的领先企业所采用，包括：  
**Animech、Arm、宝马、迪士尼、Facebook、Famobi、Funday Factory、IGT、King、Miniclip、Leapfrog、Mojiworks、Mozilla、尼克国际儿童频道、Nordeus、NOWWA、PikPok、PlaySide Studios、Polaris、Product Madness、三星、Snap、Spry Fox、Zeptolab、Zynga**

## 功能特性

PlayCanvas 是一款功能完备的游戏引擎，具备以下特性：

* 🧊 **图形渲染** - 基于 WebGL2 与 WebGPU 构建的高级 2D + 3D 图形引擎。
* 🏃 **动画系统** - 支持角色和任意场景属性的强大状态驱动动画。
* ⚛️ **物理引擎** - 与 3D 刚体物理引擎 [ammo.js](https://github.com/kripken/ammo.js) 完全集成。
* 🎮 **输入系统** - 支持鼠标、键盘、触摸、游戏手柄和 VR 控制器的 API。
* 🔊 **声音系统** - 基于 Web Audio API 构建的 3D 位置音效。
* 📦 **资源管理** - 基于 [glTF 2.0](https://www.khronos.org/gltf/)、[Draco](https://google.github.io/draco/) 和 [Basis](https://github.com/BinomialLLC/basis_universal) 压缩技术的异步流加载系统。
* 📜 **脚本系统** - 支持使用 TypeScript 或 JavaScript 编写游戏行为逻辑。

## 使用示例

以下是一个超级简单的"你好世界"示例 - 一个旋转的立方体！

```js
import * as pc from 'playcanvas';

const canvas = document.createElement('canvas');
document.body.appendChild(canvas);

const app = new pc.Application(canvas);

// 设置画布填充模式为充满窗口
app.setCanvasFillMode(pc.FILLMODE_FILL_WINDOW);
app.setCanvasResolution(pc.RESOLUTION_AUTO);

// 监听窗口大小变化并调整画布尺寸
window.addEventListener('resize', () => app.resizeCanvas());

// 创建立方体实体
const box = new pc.Entity('cube');
box.addComponent('model', {
  type: 'box'
});
app.root.addChild(box);

// 创建相机实体
const camera = new pc.Entity('camera');
camera.addComponent('camera', {
  clearColor: new pc.Color(0.1, 0.2, 0.3)
});
app.root.addChild(camera);
camera.setPosition(0, 0, 3);

// 创建方向光实体
const light = new pc.Entity('light');
light.addComponent('light');
app.root.addChild(light);
light.setEulerAngles(45, 0, 0);

// 根据帧间隔时间旋转立方体
app.on('update', dt => box.rotate(10 * dt, 20 * dt, 30 * dt));

app.start();
```

想亲自尝试这段代码吗？可以在 [CodePen](https://codepen.io/playcanvas/pen/NPbxMj) 上编辑它。

关于如何基于 PlayCanvas 引擎搭建本地开发环境的完整指南，可查看 [这里](https://developer.playcanvas.com/user-manual/engine/standalone/)。

## 构建方法

请确保已安装 [Node.js 18+](https://nodejs.org)。然后安装所有必需的 Node.js 依赖：

```sh
npm install
```

现在你可以运行各种构建选项：

| 命令            | 描述                                   | 输出位置 |
| --------------- | -------------------------------------- | -------- |
| `npm run build` | 构建所有引擎版本和类型声明            | `build`  |
| `npm run docs`  | 构建引擎 [API 参考文档][docs]          | `docs`   |

## PlayCanvas 编辑器

PlayCanvas 引擎是一款开源引擎，可用于创建 HTML5 应用/游戏。除引擎外，我们还提供 [PlayCanvas 编辑器](https://playcanvas.com/):

[![编辑器](https://github.com/playcanvas/editor/blob/main/images/editor.png?raw=true)](https://github.com/playcanvas/editor)

关于编辑器相关的 bug 和问题，请参考 [编辑器仓库](https://github.com/playcanvas/editor)。

[npm-badge]: https://img.shields.io/npm/v/playcanvas
[npm-url]: https://www.npmjs.com/package/playcanvas
[minzip-badge]: https://img.shields.io/bundlephobia/minzip/playcanvas
[minzip-url]: https://bundlephobia.com/result?p=playcanvas
[resolution-badge]: https://isitmaintained.com/badge/resolution/playcanvas/engine.svg
[open-issues-badge]: https://isitmaintained.com/badge/open/playcanvas/engine.svg
[isitmaintained-url]: https://isitmaintained.com/project/playcanvas/engine
[twitter-badge]: https://img.shields.io/twitter/follow/playcanvas.svg?style=social&label=关注
[twitter-url]: https://twitter.com/intent/follow?screen_name=playcanvas
[docs]: https://api.playcanvas.com/modules/Engine.html
