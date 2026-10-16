# CS-Learning

It's a Computer Science self-learning guideline for undergraduate level. Click [here](https://guotree.github.io/CS-Learning/).

一份本科级计算机科学自学指南，基于 [MkDocs Material](https://squidfunk.github.io/mkdocs-material/) 构建，线上地址：https://guotree.github.io/CS-Learning/

## 目录结构

```
CS-Learning/
├── mkdocs.yml                  # 站点配置：导航、主题、插件、扩展
├── overrides/                  # Material 主题自定义模板
├── .github/workflows/ci.yml    # CI：push 到 main 自动部署
├── .gitmodules                 # 笔记子模块声明
└── docs/
    ├── index.md                # 首页：11 个学习领域索引
    ├── links.md                # 外部链接汇总
    ├── resources/              # 各领域推荐资源（书籍 / 课程 / 视频）
    ├── notes/                  # 学习笔记（按领域分目录）
    │   ├── intro/CrashCourseCS/          # 子模块
    │   └── ai/Harvard-Data-Science/      # 子模块
    ├── assets/ javascripts/ stylesheets/ # favicon、MathJax、自定义 CSS
    └── templates.md
```

标记约定：⭐ + 加粗 = 推荐内容；✅ + 绿色 = 已完成内容。

## 本地运行

```bash
# 1. 克隆仓库（含子模块）
git clone --recursive https://github.com/guotree/CS-Learning.git
cd CS-Learning

# 2. 安装依赖（Python 3.x）
pip install mkdocs-material

# 3. 启动本地预览（http://127.0.0.1:8000/，修改文件自动热重载）
mkdocs serve

# 4. 构建静态站点（输出到 site/）
mkdocs build
```

如果你克隆时忘了加 `--recursive`，补拉子模块：

```bash
git submodule update --init --recursive
```

## 更新子模块

笔记是独立仓库，拉取最新内容：

```bash
git pull --recurse-submodules
# 或
git submodule update --remote --merge
git add docs/notes
git commit -m "update submodules"
```

## 添加内容

**新增推荐资源**：编辑 `docs/resources/<领域>.md`，沿用现有的 HTML 表格格式（Book / Course / Video 三列）。

**新增学习笔记**：

1. 在对应领域目录下创建 Markdown 文件，例如 `docs/notes/algorithms/my-notes.md`；
2. 在 `mkdocs.yml` 的 `nav` 中启用该领域并列出文件：

   ```yaml
   - Notes:
       - Algorithms and Data Structures:
           - "notes/algorithms/my-notes.md"
   ```

   目录中已有的注释块可以作为模板，取消注释并按需修改即可。

3. 笔记中可用 `[tags]` 标记主题（已启用 `tags` 插件），支持 `admonition`、代码块、MathJax 数学公式等 Markdown 扩展。

## 部署

推送到 `main` 分支后，GitHub Actions（`.github/workflows/ci.yml`）会自动执行 `mkdocs gh-deploy --force` 发布到 GitHub Pages，无需手动操作。注意：需要仓库 Settings → Pages 指向 `gh-pages` 分支。
