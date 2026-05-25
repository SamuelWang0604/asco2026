# ASCO 2026 平台 — GitHub Pages 部署指南

## 前置条件
- 已有 GitHub 账号
- 已安装 Git（macOS 自带）
- 本地已有完整 Git 提交记录（4个commit）

## 方式一：gh CLI（推荐，如已安装）

```bash
# 1. 安装 gh CLI（如未安装）
brew install gh

# 2. 登录 GitHub
gh auth login

# 3. 创建公开仓库并推送（一条命令搞定）
cd "/Users/why/Documents/Journal Universe/2026ASCO"
gh repo create asco2026 --public --source=. --remote=origin --push

# 4. 启用 GitHub Pages
gh api repos/{owner}/asco2026/pages -X POST -f source.branch=main -f source.path=/
```

## 方式二：手动创建仓库（当前可用）

### 第一步：在 GitHub 网站创建仓库
1. 打开 https://github.com/new
2. Repository name: `asco2026`
3. 选择 **Public**（公开仓库）
4. **不要**勾选 Initialize with README
5. 点击 Create repository

### 第二步：推送本地代码
```bash
cd "/Users/why/Documents/Journal Universe/2026ASCO"

# 添加远程仓库（替换 YOUR_USERNAME 为你的 GitHub 用户名）
git remote add origin https://github.com/YOUR_USERNAME/asco2026.git

# 推送到 GitHub
git push -u origin main
```

### 第三步：启用 GitHub Pages
1. 打开 https://github.com/YOUR_USERNAME/asco2026/settings/pages
2. Source 选择 **Deploy from a branch**
3. Branch 选择 **main**，路径选 **/ (root)**
4. 点击 Save

### 第四步：访问网站
- 等待 1-2 分钟部署完成
- 访问地址：`https://YOUR_USERNAME.github.io/asco2026/asco2026.html`

## 文件清单（已提交的4个commit）

| 文件 | 大小 | 说明 |
|------|------|------|
| .gitignore | 555B | Git忽略规则 |
| ASCO2026_data_cleaning.xlsx | 725KB | Excel清洗文件 |
| all_abstracts_asco2026.json | 11.4MB | 全量摘要JSON |
| asco2026.html | 90KB | 主看板（4页SPA） |
| embedded_data.js | 10.8MB | 嵌入式全文数据 |
| ASCO2026_report.html | 26KB | 分析报告 |
| ASCO2026_全景概览报告.html | 53KB | 全景概览报告 |
| analysis_for_report.json | 97KB | 中间分析数据 |
| charts_data.json | 7KB | 图表数据 |

## 注意事项
- embedded_data.js 约 10.8MB，GitHub 单文件限制 100MB，没问题
- 总仓库大小约 23MB，远低于 GitHub 1GB 建议上限
- GitHub Pages 限制：单文件 ≤ 100MB，总仓库 ≤ 1GB，带宽 100GB/月
