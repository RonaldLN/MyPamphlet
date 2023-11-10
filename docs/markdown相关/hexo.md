# Hexo

## 1

>   ### 安装前提
>
>   安装 Hexo 相当简单，只需要先安装下列应用程序即可：
>
>   -   [Node.js](http://nodejs.org/) (Node.js 版本需不低于 10.13，建议使用 Node.js 12.0 及以上版本)
>   -   [Git](http://git-scm.com/)

[安装 `hexo`](https://hexo.io/zh-cn/docs/#安装-Hexo) 

```bash
npm install -g hexo-cli
```

[建站 | Hexo](https://hexo.io/zh-cn/docs/setup)

```bash
hexo init <folder>
cd <folder>
npm install
```

>   感觉跟 mkdocs 有点类似

预览

>   [指令 - server| Hexo](https://hexo.io/zh-cn/docs/commands#server)

```bash
hexo server
```

>   启动服务器。默认情况下，访问网址为： [`http://localhost:4000/`](http://localhost:4000/)。
>
>   | 选项             | 描述                           |
>   | :--------------- | :----------------------------- |
>   | `-p`, `--port`   | 重设端口                       |
>   | `-s`, `--static` | 只使用静态文件                 |
>   | `-l`, `--log`    | 启动日记记录，使用覆盖记录格式 |

```bash
E:\Github\hexotest2>hexo server
INFO  Validating config
INFO  Start processing
INFO  Hexo is running at http://localhost:4000/ . Press Ctrl+C to stop.
```

## 2

使用主题 `Hexo Aurora Theme` 

-   官方网站：

    [Hexo Aurora Docs | Hexo Aurora Docs (tridiamond.tech)](https://aurora.tridiamond.tech/)

-   官方 github 仓库：

    [auroral-ui/hexo-theme-aurora: 🏳️‍🌈 Futuristic auroral Hexo theme. (github.com)](https://github.com/auroral-ui/hexo-theme-aurora)

在使用 hexo 搭建好初始的网站后，就可以按照

[快速上手 | Hexo Aurora Docs (tridiamond.tech)](https://aurora.tridiamond.tech/cn/guide/getting-started.html)

中的指引来**将默认的主题换成 `Aurora`**

