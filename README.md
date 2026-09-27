# xxxxxthhh.github.io

根域名 **<https://xxxxxthhh.github.io/>** 的索引页 —— 把散落在各个 project site 上的手册与工具收在一处。

仓库名等于用户名加 `.github.io`,这是 GitHub 的用户站点约定:它独占根地址,不带路径前缀。其余仓库都是 project site,地址形如 `xxxxxthhh.github.io/<repo>/`。

## 内容

单文件 `index.html`,纯静态、无框架、无构建步骤。暗色为默认主题,另有日间主题,偏好存 cookie(`kx-theme`)。

收录 11 本 HTML 手册、3 个工具看板,以及一条指向旧博客的归档条目。每条的章节数、题量等规模数据取自各站自身的统计或实际文件数。

页面**不标注更新日期**:索引只回答「有什么」,日期会持续过期并误导读者以为站点已死。新增站点时手工加一张卡片即可。

## 分支布局

| 分支 | 内容 | 状态 |
|---|---|---|
| `main` | 当前索引页 | 默认分支 · GitHub Pages 发布源 |
| `Hexo` | 2017–2020 博客的 Hexo 源码与主题 | 停更,仅作存档 |
| `master` | 上述博客 `hexo generate` 的产物 | 停更,曾是旧的 Pages 发布源 |

旧博客共 13 篇,2020-01 最后更新,站点已下线。它的生成产物使用**根绝对路径**(`/css/main.css`、`/archives/`),因此无法整体挂到 `/blog/` 之类的子路径下继续服务 —— 要恢复那些文章的原 URL,只能把 `master` 的目录树(除 `index.html` 外)搬回 `main` 根目录。

> `Hexo` 分支根目录仍留有一个 `CNAME`(指向 `kylexu.cn`)。当前 Pages 源是 `main`,该文件不生效;但若把发布源切回 `Hexo`,这个域名会重新生效。

## 修改与发布

编辑 `index.html` 后推到 `main` 即可,GitHub Pages 会自动重新构建:

```bash
git push origin main
```

若构建长时间没有动静,可手动触发并查看结果:

```bash
gh api -X POST repos/xxxxxthhh/xxxxxthhh.github.io/pages/builds
```

```bash
gh api repos/xxxxxthhh/xxxxxthhh.github.io/pages/builds/latest --jq '{status,created_at,commit}'
```

发布后请以**页面内容**而非 HTTP 状态码判断是否生效 —— 旧版本同样返回 200:

```bash
curl -sL -H 'Cache-Control: no-cache' "https://xxxxxthhh.github.io/?v=$(date +%s)" | grep -o '<title>[^<]*</title>'
```

`.nojekyll` 用于跳过 Jekyll 处理,请勿删除。

## 关于自定义域名

目前未配置自定义域名。需要注意:给**用户站点**设置自定义域名会连带改变本账号下所有未单独配置 `CNAME` 的 project site 的地址(变为 `<域名>/<repo>/`)。已有独立域名的仓库不受影响。
