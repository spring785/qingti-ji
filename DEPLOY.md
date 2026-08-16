# 轻体记 - Vercel 部署指南

## 一键部署到 Vercel

### 步骤 1：准备 GitHub 仓库

1. 将项目推送到 GitHub：
```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/你的用户名/轻体记.git
git push -u origin main
```

### 步骤 2：部署到 Vercel

1. 访问 [vercel.com](https://vercel.com) 并登录（推荐用 GitHub 登录）

2. 点击 "Add New Project"

3. 选择你的 GitHub 仓库

4. Vercel 会自动检测配置，确认以下设置：
   - **Framework Preset**: Expo
   - **Build Command**: `cd client && pnpm run build`
   - **Output Directory**: `client/dist`
   - **Install Command**: `pnpm install`

5. 点击 "Deploy"，等待部署完成

### 步骤 3：验证部署

部署完成后，Vercel 会给你一个域名，如：
- `https://qingti-ji.vercel.app`

访问该域名即可使用应用。

## 本地开发

```bash
# 安装依赖
pnpm install

# 启动开发服务器
coze dev

# 访问 http://localhost:5000
```

## 项目结构

```
├── api/                    # Vercel Serverless Functions
│   └── index.ts           # API 入口
├── client/                # Expo 前端
│   ├── app/              # 路由配置
│   ├── screens/          # 页面实现
│   └── components/       # 组件
├── server/               # Express 后端（本地开发用）
│   └── src/
├── vercel.json           # Vercel 配置
└── package.json
```

## 环境变量

部署时不需要设置环境变量，前后端同域自动处理。

如需本地开发连接远程后端，可设置：
```
EXPO_PUBLIC_BACKEND_BASE_URL=https://your-backend.vercel.app
```

## 常见问题

### Q: 为什么选择 Vercel？
- 免费额度充足（100GB 带宽/月）
- 自动 HTTPS
- 全球 CDN 加速
- 一键部署，自动 CI/CD

### Q: 数据会丢失吗？
当前版本使用内存存储，重启后数据会重置。如需持久化数据，建议接入 Supabase 或 Firebase。

### Q: 如何更新代码？
推送代码到 GitHub 后，Vercel 会自动重新部署。
