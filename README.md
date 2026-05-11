# Pioneer Corn Revolutionized - 交互式 WebGL 体验项目

## 📖 项目概述
本项目是一个基于 WebGL 的交互式 3D 体验应用（基于 Pioneer 品牌宣传项目："Corn Revolutionized"）。它通过高质量的 3D 模型、纹理和前端交互动画，向用户展示玉米的生长过程及农业科技（包含玉米粒、秸秆、土壤等细节场景的渲染）。该代码库包含了该线上活动的前端静态资源与 3D 资产的完整存档。

## 🛠 技术栈
- **核心图形技术**: WebGL / 3D 渲染（通常配合 Three.js，通过 `vendors~main.js` 提供底层支持）
- **3D 资产格式**: `.gltf` / `.bin` (模型), `.ktx` (ASTC 压缩纹理用于 GPU 优化), `.png` PBR 材质
- **构建工具**: Webpack (打包出 `main`, `vendors`, `loader` 等 bundle)
- **字体与排版**: 自定义 Web 字体 (Gilroy, Manifold)、原生 CSS 响应式设计、以及针对不同设备（桌面/平板/手机）的布局适配
- **第三方分析与追踪**: 
  - Google Analytics / Google Tag Manager
  - Facebook Pixel
  - Snapchat Event Tracking
  - Eloqua (营销自动化工具)
  - TrustArc (Cookie / 隐私声明组件)

## 📂 核心目录结构
由于是对线上站点的归档，项目文件按其原始 CDN 域名进行了物理文件夹拆分：

```text
/
├── index.html                           # 核心入口文件，包含骨架屏样式与预加载逻辑
├── d1hl9u9k5hiqxp.cloudfront.net/       # 核心静态资源目录 (主 CDN 归档)
│   ├── loader.[hash].js                 # 资源预加载脚本
│   ├── main.[hash].js                   # 核心交互与业务逻辑代码
│   ├── vendors~main.[hash].js           # 第三方库依赖 (WebGL引擎、动画库等)
│   ├── models/                          # 3D 几何模型 (.gltf, .bin)
│   │   ├── kernel/                      # 玉米粒组件
│   │   └── landing/                     # 着陆页动画元素等
│   ├── textures/                        # 高清纹理与法线贴图
│   ├── compressed/                      # KTX 格式压缩纹理 (针对不同 GPU 硬件的显存优化)
│   ├── fonts/                           # Web 字体资源
│   ├── images/                          # UI 界面图像与图标
│   └── svg/                             # 矢量图形
├── www.googletagmanager.com/            # GTM 追踪脚本目录
├── connect.facebook.net/                # FB 追踪目录
├── consent.trustarc.com/                # TrustArc 合规组件
└── ...其他第三方静态追踪归档目录
```

## 🎨 核心 3D 场景解析
根据归档的 `assets` 和 `compressed` 目录，该交互体验涉及以下丰富的视觉维度：
- **Soil (土壤)**: 包含不同类型的营养成分（沙土、壤土、粘土）的置换贴图(Displacement)和法线贴图(Normal Map)。
- **Stalk (秸秆)**: 绑定骨骼的 `.gltf` 动画、不同阶段的颜色渐变、光照遮蔽贴图。
- **Kernel (玉米粒)**: 精细的玉米粒模型及屏幕后处理材质映射。
- **Environment (环境)**: 复杂的渲染环境，包含雨水纹理 (`rainTexture`)、镜头光晕 (`lens-flare`)、体积光噪音映射以及环境 HDR 反射贴图。

## 🚀 本地运行指南

由于项目包含大量的外部异步加载资源和 WebGL 模型，直接双击 `index.html` 用浏览器打开会导致跨域策略 (CORS) 拦截，从而导致 3D 模型或贴图加载失败呈现黑屏。建议通过本地 HTTP 服务器运行此项目。

### 运行步骤

1. **启动一个本地静态服务器** 
   你可以使用任何你熟悉的本地服务器工具，例如 Node.js 或 Python：
   
   ```bash
   # 如果你安装了 Node.js:
   npx http-server . -p 8080
   
   # 如果你安装了 Python 3:
   python3 -m http.server 8080
   ```

2. **访问应用**
   在浏览器中打开：`http://localhost:8080/index.html` （如果页面在跳转中受阻，请确保你拦截了可能重定向的分析脚本或在隔离环境中查看）。

> **⚠️ 注意**：此项目主要是构建后的生产环境打包产物（Minified JS）。如需深度研究其 3D 互动逻辑，需要通过浏览器的 Source 面板格式化 `main.js` 以作逆向参考。