## 1

[Installation - Material for MkDocs (squidfunk.github.io)](https://squidfunk.github.io/mkdocs-material/getting-started/)

## 2

```yaml
markdown_extensions:
  - pymdownx.superfences: # mermaid画图
      custom_fences:
        - name: mermaid
          class: mermaid
          format: !!python/name:pymdownx.superfences.fence_code_format
  - attr_list # 矩形按钮/按键
  - def_list # a 无序/有序/任务 列表
  - pymdownx.tasklist: # a
      custom_checkbox: true
  - pymdownx.critic # b Formatting 含 高亮/删除线/下划线/上下角标 [等]
  - pymdownx.caret # b
  - pymdownx.keys # b
  - pymdownx.mark # b
  - pymdownx.tilde # b
  - toc: # 目录相关
      permalink: true # 每个页面内，各标题会生成各自的链接
      # title: 目录 # 修改页面右侧 Table of contents 文字
  - footnotes # 脚注
  - pymdownx.highlight: # c 代码块配置
      anchor_linenums: true
      line_spans: __span
      pygments_lang_class: true
  - pymdownx.inlinehilite # c
  - pymdownx.snippets # c
  - pymdownx.superfences # c
  - admonition # d 标注
  - pymdownx.details # d
  - pymdownx.superfences # d
```

## 3

```yaml
theme:
  name: material # 固定
  # language: zh # 语言设置为中文(会改变搜索栏/最后修改 等文字)，默认为英文
  logo: assets/logo.jpg # 页面中顶部栏左侧图标
  favicon: assets/favicon.jpg # 浏览器页面标签图标
  features:
    - navigation.expand # 目录自动展开子目录
    # - toc.integrate # 右边的toc融合到左侧的目录中
    - toc.follow # 右侧toc随着页面滑动自动滑动
    - navigation.top # 有回到页面最上方top的按键
    - search.suggest # 搜索建议
    - navigation.footer # 页面底部有下一页的链接(按目录上的顺序)
    - navigation.tabs # 一级目录融合至顶栏，并且只展示二级目录
    - content.code.copy # 代码块复制按键
    - search.suggest # 搜索建议
    - search.highlight # 搜索结果高亮/突出显示
    - search.share # 搜索结果分享
```

## 4

昼夜模式切换按键

```yaml
theme:
  palette: 

    # Palette toggle for light mode
    - media: "(prefers-color-scheme: light)"
      scheme: default
      toggle:
        icon: material/weather-night # 图标(可改，下同)
        name: Switch to dark mode

    # Palette toggle for dark mode
    - media: "(prefers-color-scheme: dark)"
      scheme: slate
      toggle:
        icon: material/weather-sunny
        name: Switch to light mode
```

## 5

目录

```yaml
nav:
  - 一级目录a: "a.md"
  - 一级目录b: "b.md"
  - 一级目录c: # 有子目录不能包含链接
    - 二级目录aa: "aa.md"
    - 二级目录ab: 
      - 三级目录aaa: "aaa.md"
  - 一级目录d: "d.md"
  ...
```

## 6

```yaml
plugins:
  - i18n: # 语言切换 (需要放在 git-revision-date-localized 之前)
      default_language: en
      material_alternate: true
      languages:
        zh:
          name: 简体中文
          build: true
        en:
          name: English labels (英文标签)
          build: true
  - git-revision-date-localized: # 页面下方创建和修改时间
      enable_creation_date: true
      type: timeago
  - glightbox # 图片放大
  - search: # 搜索(支持中文、英文)
      lang: 
        - zh
        - en
```

-   [语言切换](#17)
-   [页面下方创建和修改时间](#13)
-   [图片放大](#14)

## 7

右上角github仓库

[Adding a git repository - Material for MkDocs (squidfunk.github.io)](https://squidfunk.github.io/mkdocs-material/setup/adding-a-git-repository/)

```yaml
repo_url: https://github.com/RonaldLN/Project-Application-Form-of-AIGC
repo_name: Project-Application-Form-of-AIGC
```

## 8

上传到`github`、`gitee`仓库：

```bash
mkdocs gh-deploy --force
```

(该命令只上传site文件夹至gh-pages分支，若是github仓库，会自动选择gh-pages分支生成github pages页面)

## 9

添加 KaTeX 公式书写

`docs/javascripts/katex.js`:

```js
document$.subscribe(({ body }) => { 
  renderMathInElement(body, {
    delimiters: [
      { left: "$$",  right: "$$",  display: true },
      { left: "$",   right: "$",   display: false },
      { left: "\\(", right: "\\)", display: false },
      { left: "\\[", right: "\\]", display: true }
    ],
  })
})
```

`mkdocs.yml`:

```yaml
extra_javascript:
  - javascripts/katex.js 
  - https://cdnjs.cloudflare.com/ajax/libs/KaTeX/0.16.7/katex.min.js  
  - https://cdnjs.cloudflare.com/ajax/libs/KaTeX/0.16.7/contrib/auto-render.min.js

extra_css:
  - https://cdnjs.cloudflare.com/ajax/libs/KaTeX/0.16.7/katex.min.css
```

## 10

放在 `/doc`内子文件夹里的md文件会根据该子文件夹名自动生成一级目录（如果没有自定义目录）

## 11

添加谷歌分析

```yaml
extra:
  analytics:
    provider: google
    property: G-xxxxxxxxxx
```

## 12

图像延迟加载

在每个图像后加上 `{ loading=lazy }` 

```markdown
![xxx](.../xxx.png){ loading=lazy }
```

## 13

设置每个文章底部显示创建和更新时间

[Adding a git repository - Material for MkDocs (squidfunk.github.io)](https://squidfunk.github.io/mkdocs-material/setup/adding-a-git-repository/?h=contributor#document-dates)

添加包：

```bash
pip install mkdocs-git-revision-date-localized-plugin
```

添加到 `mkdocs.yml`:

```yaml
plugins:
  - git-revision-date-localized:
      enable_creation_date: true
      type: timeago
```

## 14

图片缩放功能/点击放大

[Images - Material for MkDocs (squidfunk.github.io)](https://squidfunk.github.io/mkdocs-material/reference/images/#lightbox)

`pip`:

```bash
pip install mkdocs-glightbox
```

`mkdocs.yml`:

```yaml
plugins:
  - glightbox
```

>   插件官方使用文档：
>
>   [blueswen/mkdocs-glightbox: A MkDocs plugin supports image lightbox (zoom effect) with GLightbox. (github.com)](https://github.com/blueswen/mkdocs-glightbox#usage)

## 15

添加版权信息

```yaml
copyright: Copyright &copy; 2023 - 2023 Ronald Luo
```

## 16

搜索

```yaml
theme:
    ...
    features:
 	...
    - search.suggest # 搜索建议
    - search.highlight # 搜索结果高亮/突出显示
    - search.share # 搜索结果分享

plugins:
  ...
  - search: # 搜索(选择支持中文、英文)
      separator: '[\s\-,:!=\[\]()"/]+|(?!\b)(?=[A-Z][a-z])|\.(?!\d)|&[lg]t;'
      lang: 
        # - zh
        - ja
        - en
```

中文暂不支持，可以选择日文( `ja` )代替

>   中文支持(即将)
>
>   >   [Setting up site search - Material for MkDocs (squidfunk.github.io)](https://squidfunk.github.io/mkdocs-material/setup/setting-up-site-search/#chinese-language-support)
>
>   为了在[内置搜索插件](https://squidfunk.github.io/mkdocs-material/setup/setting-up-site-search/#built-in-search-plugin)中添加对中文的支持，请通过 `pip` 安装 [jieba](https://pypi.org/project/jieba/) 文本分割库，插件将通过分句器运行所有文本：
>
>   ```bash
>   pip install jieba
>   ```

搜索建议功能：

>   启用搜索建议后，搜索将显示最后一个单词的最可能完成情况，该单词可以通过 ++arrow-right++ 键填充

## 17

语言切换

>   参考
>
>   [cs-self-learning/mkdocs.yml at master · PKUFlyingPig/cs-self-learning (github.com)](https://github.com/PKUFlyingPig/cs-self-learning/blob/master/mkdocs.yml)

需要安装 `mkdocs-static-i18n` 包

```bash
pip install mkdocs-static-i18n
```

并且在 `mkdocs.yml` 中 `plugins:` 里 `- i18n:` 需要写在 `git-revision-date-localized` 之前

>   报错信息：
>
>   ```bash
>   Error: [git-revision-date-localized] should be defined after the i18n plugin in your mkdocs.yml file. This is because i18n adds a 'locale' variable to markdown pages that this plugin supports.
>   ```

并且添加了i18n需要注释掉 `theme:` 中的 `language:` 

此外，

若想添加对应语言版本的文档，比如 `index.md` 的中文版，则在相同路径下创建 `index.zh.md` 进行编写

>   参考
>
>   [cs-self-learning/docs at master · PKUFlyingPig/cs-self-learning (github.com)](https://github.com/PKUFlyingPig/cs-self-learning/tree/master/docs)
>
>   ---
>
>   [ultrabug/mkdocs-static-i18n: MkDocs i18n plugin using static translation markdown files (github.com)](https://github.com/ultrabug/mkdocs-static-i18n/)
