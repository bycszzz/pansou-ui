# PanSou 网盘资源搜索工具

一个基于 React + TypeScript + Vite 构建的现代化网盘资源搜索和API状态监控工具。支持搜索阿里云盘、百度网盘、夸克网盘等多种网盘资源，提供实时API状态监控功能。

![PanSou Tool](https://img.shields.io/badge/React-19-blue?style=for-the-badge&logo=react)
![TypeScript](https://img.shields.io/badge/TypeScript-5.0-blue?style=for-the-badge&logo=typescript)
![Vite](https://img.shields.io/badge/Vite-7.0-purple?style=for-the-badge&logo=vite)
![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-3.0-38B2AC?style=for-the-badge&logo=tailwind-css)

## ✨ 功能特性

### 🔍 智能网盘搜索
- **多网盘支持**: 阿里云盘、百度网盘、夸克网盘等主流网盘
- **实时搜索**: 快速响应，毫秒级搜索结果
- **智能筛选**: 支持按网盘类型筛选，快速定位目标资源
- **结果展示**: 美观的卡片式布局，清晰展示文件信息
- **一键复制**: 支持复制分享链接和提取密码

### 📊 API 状态监控
- **实时监控**: 每分钟自动检测API服务状态
- **性能指标**: 显示响应时间、在线率等关键数据
- **历史记录**: 追踪服务状态变化历史
- **自动刷新**: 支持手动刷新和自动定时刷新
- **状态可视化**: 直观的进度条和状态指示器

### 🎨 现代化界面
- **主题切换**: 支持亮色/暗色主题，Apple风格设计
- **响应式设计**: 完美适配桌面端和移动端
- **流畅动画**: 优雅的过渡效果和交互反馈
- **直观导航**: 简洁的导航栏和面包屑导航

### 🚀 性能优化
- **快速加载**: Vite构建，极速热重载
- **代码分割**: 按需加载，优化首屏性能
- **缓存策略**: 智能缓存，提升用户体验
- **错误处理**: 完善的错误边界和用户提示

## 🛠️ 技术栈

- **前端框架**: React 19 + TypeScript
- **构建工具**: Vite 7.0
- **样式框架**: Tailwind CSS 3.0
- **路由管理**: React Router DOM
- **HTTP客户端**: Axios
- **图标库**: Lucide React
- **状态管理**: React Context API
- **代码规范**: ESLint + Prettier

## 📦 安装和使用

### 环境要求
- Node.js 18.0 或更高版本
- npm 8.0+ 或 yarn 1.22+

### 快速开始

1. **克隆项目**
```bash
git clone https://github.com/bycszzz/pansou-ui.git
cd pansou-ui
```

2. **安装依赖**
```bash
npm install
# 或使用 yarn
yarn install
```

### 构建部署

**构建生产版本**
```bash
npm run build
```

**预览构建结果**
```bash
npm run preview
```

**代码检查**
```bash
npm run lint
```

## ⚙️ 配置说明

### API地址配置

#### 生产环境配置
在 `src/services/pansouApi.ts` 文件中修改API基础URL：

```typescript
// src/services/pansouApi.ts
const API_BASE_URL = ''

#### NGINX配置
# --- HTTP 到 HTTPS 的强制跳转 ---
server {
    listen 80;
    listen [::]:80;
    server_name your_domain ;
    return 301 https://$host$request_uri;
}

# --- HTTPS 服务配置 ---
server {
    listen 443 ssl http2;
    listen [::]:443 ssl http2;
    server_name your_domain ;

    ssl_certificate /etc/nginx/ssl/cert.pem;
    ssl_certificate_key /etc/nginx/ssl/key.pem;

    # ↓↓↓ 这是新增的反向代理配置块 ↓↓↓
    # 所有 /api/ 开头的请求都会被转发到后端API
    location /api/ {
        # proxy_pass 指向你后端服务的实际地址
        # 注意：这里用 127.0.0.1 (本地回环地址) 而不是公网IP，更安全高效
        proxy_pass http://127.0.0.1:8080;

        # --- 以下是推荐的代理头部设置 ---
        # 将原始请求的 Host 头部传递给后端
        proxy_set_header Host $host;
        # 将客户端的真实IP地址传递给后端
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }

    # --- 这是你原来的前端文件服务配置 ---
    # 所有不匹配 /api/ 的其他请求，都会由这里处理，返回你的网页
    location / {
        root /var/www/pansou-ui/dist;
        try_files $uri $uri/ /index.html;
    }
}
```

### 注意事项
- 可能需要配置selinux `sudo setsebool -P httpd_can_network_connect 1`

## 🎯 使用指南

### 搜索功能
1. 在搜索框中输入关键词（如：电影、软件、教程等）
2. 点击搜索按钮或按回车键开始搜索
3. 使用筛选按钮按网盘类型过滤结果
4. 点击结果卡片查看详细信息
5. 复制分享链接和提取密码

### 状态监控
1. 点击导航栏的"状态监控"进入监控页面
2. 查看API服务的实时状态和性能指标
3. 点击"刷新"按钮手动更新状态
4. 监控页面会自动每分钟更新一次

### 主题切换
- 点击导航栏右侧的月亮/太阳图标切换主题
- 主题偏好会自动保存到本地存储

## 📁 项目结构

```
src/
├── components/          # 可复用组件
│   ├── SearchBox.tsx    # 搜索框组件
│   ├── SearchResults.tsx # 搜索结果组件
│   ├── ResultCard.tsx   # 结果卡片组件
│   ├── ErrorMessage.tsx # 错误信息组件
│   ├── LoadingSpinner.tsx # 加载动画组件
│   └── LoadingState.tsx # 加载状态组件
├── pages/              # 页面组件
│   └── StatusPage.tsx  # 状态监控页面
├── services/           # API服务
│   ├── pansouApi.ts    # PanSou API接口
│   └── statusService.ts # 状态监控服务
├── contexts/           # React Context
│   └── ThemeContext.tsx # 主题管理
├── types/              # TypeScript类型定义
│   ├── api.ts          # API相关类型
│   └── status.ts       # 状态相关类型
├── utils/              # 工具函数
│   └── helpers.ts      # 通用工具函数
├── assets/             # 静态资源
├── App.tsx             # 主应用组件
├── main.tsx            # 应用入口
└── index.css           # 全局样式
```

## ⚙️ 配置说明


### 主题配置
支持亮色和暗色主题，用户偏好会保存在 localStorage 中。

**CSS变量配置**
```css
:root {
  /* 亮色主题变量 */
  --bg-primary: #ffffff;
  --text-primary: #1f2937;
  --accent-color: #3b82f6;
}

[data-theme="dark"] {
  /* 暗色主题变量 */
  --bg-primary: #1a1a1a;
  --text-primary: #ffffff;
  --accent-color: #60a5fa;
}
```

## 🚀 部署指南

### Vercel 部署
1. Fork 本项目到你的 GitHub 账户
2. 在 [Vercel](https://vercel.com) 中导入项目
3. 配置构建命令：`npm run build`
4. 配置输出目录：`dist`
5. 点击部署

### Netlify 部署
1. Fork 本项目到你的 GitHub 账户
2. 在 [Netlify](https://netlify.com) 中连接 GitHub 仓库
3. 配置构建命令：`npm run build`
4. 配置发布目录：`dist`
5. 点击部署

### 静态服务器部署
```bash
# 构建项目
npm run build

# 将 dist 目录上传到你的服务器
# 配置 Nginx 或其他 Web 服务器
```


### 开发规范
- 使用 TypeScript 编写代码
- 遵循 ESLint 和 Prettier 配置
- 添加适当的注释和文档
- 确保所有测试通过

## 📝 更新日志

### v1.0.0 (2024-07-12)
- ✨ 初始版本发布
- 🔍 实现网盘资源搜索功能
- 📊 添加API状态监控
- 🎨 支持亮色/暗色主题切换
- 📱 响应式设计优化

## 📄 许可证

本项目采用 MIT 许可证 - 查看 [LICENSE](LICENSE) 文件了解详情。

## 🙏 致谢
- [linuxdo](https://linux.do) 快来玩
- [PanSou API](https://pansou.252035.xyz) - 提供网盘搜索服务
- [React](https://reactjs.org) - 前端框架
- [Vite](https://vitejs.dev) - 构建工具
- [Tailwind CSS](https://tailwindcss.com) - CSS框架
- [Lucide React](https://lucide.dev) - 图标库

## 📞 联系我们

- gemini https://gemini.google.com/
- grok https://grok.com/

---

⭐ 如果这个项目对你有帮助，请给我们一个 Star！
