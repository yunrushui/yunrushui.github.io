# yunrushui blog

博客地址：https://yunrushui.github.io/

## Ubuntu 打开项目

```bash
source /opt/blog/env.sh
cd /opt/blog/site
code .
```

在 VS Code 左侧打开 source/_posts 下的 Markdown 文件编辑。
按 Ctrl+Shift+V 查看 Markdown 预览；这是文章预览，不包含网站主题。
按 Ctrl+Shift+P，选择 Tasks: Run Task，再选择“预览博客”。
打开 http://localhost:4000 查看整站，保存文章后刷新浏览器。
若已有预览服务运行，无需再启动；在运行服务的终端按 Ctrl+C 停止。
修改 _config.yml 后需重启预览服务。

## 每次编辑前

先确认上次修改已提交，再拉取另一系统推送的修改：

```bash
git status
git pull --ff-only
```

首次上传并设置 upstream 后才能使用上述 pull。
如果拉取失败或提示本地修改冲突，停止并检查，不要强制覆盖。

## 新文章与图片

Ubuntu 终端先 source /opt/blog/env.sh，并 cd /opt/blog/site。
Windows 在博客目录使用 npm exec -- hexo 代替下方的 hexo。

```bash
hexo new "my-first-post"
```

编辑 source/_posts/my-first-post.md。保留顶部 --- 包围的配置，
可将 title 改为中文，正文写在第二个 --- 后面。例如：

```markdown
---
title: 我的第一篇博客
date: 2026-10-19 12:00:00
tags:
  - 学习记录
---

今天开始记录自己的学习过程。

## 学习内容

- 第一项
- 第二项
```

文件名一旦公开尽量不要改，文章网址与日期和文件名有关。
图片可放到 source/images/，文章用 ![说明](/images/example.png) 引用。

## 本地草稿

```bash
hexo new draft "unfinished-post"
hexo server --draft --ip 127.0.0.1
```

source/_drafts/ 已被 Git 忽略，留在当前系统，不同步到另一系统。
准备公开时执行 hexo publish "unfinished-post"，检查后再提交。
不要把密码、令牌、私钥写进文章或公开仓库。

## 发布修改

先保存编辑器文件，再检查生成和变更：

```bash
npm run build
git status
git diff
```

确认待上传的内容都可以公开，再执行：

```bash
git add .
git diff --cached --stat
git commit -m "Update blog"
git push
```

git add 暂存；git commit 保存本地版本；git push 上传 GitHub。
完成 GitHub Pages 设置后，每次推送 main 都会自动部署。
到仓库 Actions 页面检查发布是否成功，然后访问博客。
上传成功不等于部署成功；失败时查看 Actions 中的错误。

## 双系统

Windows 和 Ubuntu 各有一份源文件，通过同一 GitHub 仓库同步。
切换前提交并推送，切换后先 git pull --ff-only。
两边 node_modules 分别安装，不复制，不提交。保留 package-lock.json。
Windows 需单独安装 Git、Node.js，并配置自己的 SSH 身份。
Ubuntu 私钥和工具位于 /opt/blog/site 之外，不上传仓库。
