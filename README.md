# BWM-Forge

**Agentic World Programming for Embodied Intelligence**

Program geometry, motion and viewpoints. Generate high-fidelity robot videos through a collaborative agent workflow.

BWM-Forge 项目展示网站，介绍空间语义驱动、运动先验驱动与真实示范驱动三种输入模式，以及多智能体流程、案例视频、评估指标和 Harness 架构。支持中英文切换、日间与夜间主题；首次访问默认使用白底日间模式，之后记住用户的选择。

## 文件结构

```text
BWM-Forge/
├── index.html       # 完整页面，包含样式、交互逻辑和中英文文案
├── media/cases/     # 页面实际引用的案例视频、图片和海报
├── photos/          # 项目标志
├── vendor/          # 本地样式依赖、字体与图标字体
├── .nojekyll        # 直接发布静态文件
├── .gitattributes
├── .gitignore
└── README.md
```

这是可直接发布的静态站点，无需构建、npm 安装或后端服务。直接编辑 `index.html`，并保持资源相对路径有效。

## 本地预览

在仓库根目录运行：

```powershell
python -m http.server 8000 --bind 127.0.0.1
```

打开 <http://127.0.0.1:8000/>。按 `Ctrl+C` 停止服务。

## 发布到 GitHub Pages

1. 在 GitHub 创建名为 `BWM-Forge` 的空仓库。
2. 在本地仓库根目录执行下列命令，将 `YOUR_USERNAME` 替换成实际账号。提交时使用你自己的 Git 用户名和邮箱。

```powershell
git add .
git commit -m "Publish BWM-Forge website"
git remote add origin https://github.com/YOUR_USERNAME/BWM-Forge.git
git push -u origin main
```

3. 打开仓库 **Settings → Pages**，选择 **Deploy from a branch**，分支选择 **main**，目录选择 **/(root)**，保存。
4. 部署成功后，在 `https://YOUR_USERNAME.github.io/BWM-Forge/` 访问网站。

所有页面资源使用相对路径，可部署在 `/BWM-Forge/` 子路径；`.nojekyll` 使静态文件直接发布。如果要使用账号根域名 `https://YOUR_USERNAME.github.io/`，对应仓库应命名为 `YOUR_USERNAME.github.io`。参见 [GitHub Pages 官方部署说明](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site)。

## 更新文案、资源与链接

- **论文链接**：在 `index.html` 中查找 `id="technical-report-link"`，替换其 `href`。当前暂指向 `https://arxiv.org/`。
- **代码链接**：查找 `id="github-link"`，替换其 `href`。当前暂指向 `https://github.com/`。
- **中英文文案**：同步修改页面初始英文内容及 `const i18n` 内的 `en`、`zh` 文案，保留 `data-i18n` 键。
- **案例资源**：修改对应的 `src`、`poster`、`data-preview-src`；视频与缩略图引用需一起更新。建议使用浏览器可播放的 H.264 MP4。
- **输入示意图**：搜索 `bwm-evidence`，可编辑内联 SVG 图标、箭头和文字。
- **主题**：默认日间模式，主题开关会将用户选择保存到浏览器本地。

更新后检查桌面和移动端的中英文页面，以及 Agent 切换、案例切换和视频播放，再提交并推送即可更新站点。

## Cloudflare 临时共享

保持上述本地预览服务运行，在另一个终端使用已安装的 `cloudflared`：

```powershell
cloudflared tunnel --url http://127.0.0.1:8000
```

使用终端显示的 `https://…trycloudflare.com` 链接分享预览。保持两个终端运行，结束后按 `Ctrl+C` 关闭。该临时链接不影响 GitHub Pages 的正式地址。
