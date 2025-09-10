# Vue 3 + TypeScript + Vite + Pinia 逐帧动画项目

## 🎯 项目特性

- **Vue 3** - 最新版本的Vue框架
- **TypeScript** - 类型安全的JavaScript
- **Vite** - 快速的构建工具
- **Pinia** - 状态管理库
- **逐帧动画组件** - 鼠标滚轮控制的动画播放
- **原生HTML实现** - 纯原生实现的备用版本

## 🚀 在线演示

### GitHub Pages 部署
1. 将项目推送到GitHub仓库
2. 进入仓库设置 → Pages
3. 选择 "GitHub Actions" 作为源
4. 访问: `https://你的用户名.github.io/vue3-ts-pinia-app/`

### GitHub Codespaces
1. 点击仓库的 "Code" 按钮
2. 选择 "Open with Codespaces"
3. 在终端运行: `npm run dev`
4. 通过端口转发访问

### Netlify 部署 (备选)
1. 连接GitHub仓库到Netlify
2. 构建命令: `npm run build`
3. 发布目录: `dist`
4. 自动部署每次提交

## 📦 安装和运行

```bash
# 安装依赖
npm install

# 开发模式
npm run dev

# 构建生产版本
npm run build

# 预览生产版本
npm run preview
```

## 🎮 使用说明

### 逐帧动画组件
- 使用鼠标滚轮控制动画播放
- 键盘方向键 ↑/↓ 精确控制
- 实时进度指示器
- 支持触摸设备

### 原生HTML版本
位于 `src/html/frame-animation.html`
- 纯原生实现，无需框架
- 直接浏览器打开即可运行

## 📁 项目结构

```
├── public/
│   └── images/frames/     # 本地图片资源
├── src/
│   ├── components/        # Vue组件
│   │   └── FrameAnimation.vue
│   ├── html/             # 原生HTML实现
│   │   └── frame-animation.html
│   └── main.ts           # 应用入口
├── .github/workflows/     # GitHub Actions配置
└── vite.config.ts        # Vite配置
```

## 🌐 浏览器支持

- Chrome 90+
- Firefox 88+
- Safari 14+
- Edge 90+

## 📄 许可证

MIT License
