# AGENTS.md

## 项目概览
- 这是一个 **Hexo 5** 个人博客仓库，站点配置在 [`_config.yml`](/Users/fazzie/code/Fazziekey.github.io/_config.yml)。
- 当前主题是 `butterfly`，主题配置在 [`themes/butterfly/_config.yml`](/Users/fazzie/code/Fazziekey.github.io/themes/butterfly/_config.yml)。
- 仓库同时保存了 Hexo 源文件和已生成的静态站点产物；默认应优先修改源文件，再通过 Hexo 重新生成。

## 内容与目录约定
- 博客文章主要位于 [`source/_posts`](/Users/fazzie/code/Fazziekey.github.io/source/_posts)。
- 标签页、分类页、友链页等入口页面位于 [`source/tags`](/Users/fazzie/code/Fazziekey.github.io/source/tags)、[`source/categories`](/Users/fazzie/code/Fazziekey.github.io/source/categories)、[`source/link`](/Users/fazzie/code/Fazziekey.github.io/source/link)。
- `about`、`aboutEN`、`CV` 相关页面包含静态 HTML，并且在 Hexo `skip_render` 中被排除；这类页面可以直接改源 HTML，但不要把它们迁移成普通 Hexo 页面，除非用户明确要求。
- `source/_data/link.yml` 存放友链数据。
- `source/nn` 看起来是一个独立页面入口，修改前先检查它是否依赖本地静态资源或自定义脚本。

## 生成产物
- [`public`](/Users/fazzie/code/Fazziekey.github.io/public)、根目录下的 [`index.html`](/Users/fazzie/code/Fazziekey.github.io/index.html)、[`archives`](/Users/fazzie/code/Fazziekey.github.io/archives)、[`tags`](/Users/fazzie/code/Fazziekey.github.io/tags)、[`categories`](/Users/fazzie/code/Fazziekey.github.io/categories)、[`page`](/Users/fazzie/code/Fazziekey.github.io/page) 等大多是生成后的静态文件。
- 如果任务是“修改博客内容/样式/配置”，优先改 `source/`、`themes/butterfly/` 或根配置；不要把对生成目录的直接修改当成长期方案。
- 只有在用户明确要求“直接修线上静态文件”或仓库工作流本身就是提交产物时，才直接编辑这些生成文件。

## 常用命令
- 安装依赖：`npm install`
- 本地预览：`npm run server`
- 生成静态文件：`npm run build`
- 清理缓存与产物：`npm run clean`
- 部署：`npm run deploy`

## 编辑规范
- 文章 front matter 现有格式通常包含 `title`、`date`、`tags`、`categories`，保持 YAML 缩进风格一致。
- 仓库内同时存在中文和英文文件名，新增文章时优先沿用现有命名习惯，不要为了“统一”而批量重命名旧文章。
- 数学公式由 `hexo-math`/MathJax 支持；涉及公式渲染的问题时，先检查文章 front matter 和主题 math 配置。
- 主题菜单、社交链接、搜索、封面图等优先在 [`themes/butterfly/_config.yml`](/Users/fazzie/code/Fazziekey.github.io/themes/butterfly/_config.yml) 中调整，而不是直接改编译后的 HTML。
- 若需修改站点 URL、部署分支、skip_render 或插件行为，改 [`_config.yml`](/Users/fazzie/code/Fazziekey.github.io/_config.yml)。

## 工作方式建议
- 开始修改前，先确认目标是“源文件”还是“生成产物”，这在本仓库里很关键。
- 做完内容或主题修改后，至少运行一次 `npm run build` 验证 Hexo 能正常生成。
- 若任务涉及部署，先注意仓库里存在两套历史信息：[`deploy.sh`](/Users/fazzie/code/Fazziekey.github.io/deploy.sh) 使用 `git push origin hexo`，而 [`_config.yml`](/Users/fazzie/code/Fazziekey.github.io/_config.yml) 的 Hexo deploy 分支配置为 `master`。除非用户明确要求，不要擅自统一这两处配置。
