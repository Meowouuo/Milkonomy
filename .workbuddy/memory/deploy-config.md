# MilkyProfit 自动部署配置

## GitHub Actions CI/CD

**工作流文件**：`.github/workflows/deploy.yml`

### 触发条件

- 推送代码到 `main` 分支时自动触发
- 支持手动触发（workflow_dispatch）

### 部署流程

1. **Checkout** - 检出代码
2. **Setup Node.js** - 安装 Node.js 22
3. **Install dependencies** - `npm ci` 安装依赖
4. **Build** - `npm run build` 构建公开版本
   - 设置环境变量：
     - `VITE_PUBLIC_PATH: /MilkyProfit/`
     - `VITE_ROUTER_HISTORY: hash`
5. **Create .nojekyll** - 禁用 Jekyll 处理
6. **Deploy** - 使用 `github-pages-deploy-action` 部署到 `meowouuo.github.io` 仓库

### 部署目标

- **目标仓库**：`Meowouuo/meowouuo.github.io`
- **目标分支**：`main`
- **部署目录**：`dist/`
- **访问地址**：`https://meowouuo.github.io/MilkyProfit/`

### 注意事项

- 使用 hash 路由模式避免 GitHub Pages 刷新 404
- `clean: false` 保留目标仓库其他文件（如 data/）
