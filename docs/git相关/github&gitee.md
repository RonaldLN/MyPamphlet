# Github & Gitee

## 1

-   gitee SSH公钥设置

    [SSH 公钥设置 | Gitee 产品文档](https://help.gitee.com/base/account/SSH公钥设置)

-   github SSH key 设置

    账户添加SSH: [Adding a new SSH key to your GitHub account - GitHub Docs](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)

    生成SSH: [Generating a new SSH key and adding it to the ssh-agent - GitHub Docs](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

## 2

上传文件至仓库：

```bash
git add --all
git commit -m "..." # 会在仓库对应文件的处显示，应该是用于标记哪一次上传
git push -u origin [ master | main ]
```

## 3

gitee pages 更新需要手动点击更新，

github pages 可以自动更新

## 4

[Generating a new SSH key and adding it to the ssh-agent - GitHub Docs](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

![github_linux_ssh](../images/github_linux_ssh.png)

```bash
ssh-keygen -t ed25519 -C "xxx@example.com"
```

第二行填写文件要保存的位置（直接复制给的就好了），然后`passphrase`可以不设置，之后把`~/.ssh/id_ed25519.pub`中的全部复制粘贴到github设置ssh中就行了

## 5

更新本地的仓库：

```bash
git pull
```

## 6

github 仓库设置 *讨论* GitHub Discussions

[GitHub Discussions 文档 - GitHub 文档](https://docs.github.com/zh/discussions)

在 **Settings - General - Features - Discussions** 前面勾选上

就可以打开*讨论*功能了

## 7

git 代理相关问题

由于之前想在 git bash 终端中使用 clash 的代理所以在 `E:\Program Files\Git\etc\bash.bashrc` 最上方按网上说的添加了

```bash
# Clash
export http_proxy=https://127.0.0.1:7890;export https_proxy=https://127.0.0.1:7890
```

然后发现 `git clone` 在不打开 clash 的情况下会有报错

```bash
Collecting git+https://github.com/huggingface/peft.git (from -r requirements.txt (line 8))
  Cloning https://github.com/huggingface/peft.git to c:\users\administrator\appdata\local\temp\pip-req-build-t4u9g6h5
  Running command git clone --filter=blob:none --quiet https://github.com/huggingface/peft.git 'C:\Users\Administrator\AppData\Local\Temp\pip-req-build-t4u9g6h5'
  fatal: unable to access 'https://github.com/huggingface/peft.git/': Failed to connect to 127.0.0.1 port 7890 after 2032 ms: Couldn't connect to server
```

所以在网上查询相关信息，发现这篇文章

[解决git下载出现：Failed to connect to 127.0.0.1 port 1080: Connection refused拒绝连接错误-CSDN博客](https://blog.csdn.net/weixin_41010198/article/details/87929622)

可以通过(windows也可以)

```bash
git config --global http.proxy
git config --global https.proxy
```

查询 git http 和 htttps 有没有使用代理

>   文章还说到 linux 还可以使用
>
>   ```bash
>   env|grep -I proxy
>   ```
>
>   来查询系统环境有没有代理，不过windows下这个命令运行不了

**取消代理的方法**

我在 windows git bash 上使用

```bash
git config --global --unset http.proxy
git config --global --unset https.proxy
```

成功取消了代理

而文章中的另一种方法

```bash
unset http_proxy
unset ftp_proxy
unset all_proxy
unset https_proxy
unset no_proxy
```

我试了在 windows git bash 上不行，可能在linux上可以

最后我取消了代理之后 `git clone` 就不会有之前的 ` Failed to connect to 127.0.0.1 port 7890` 

>   但是没打开 clash 时，变成了
>
>   ```bash
>   fatal: unable to access 'https://github.com/huggingface/peft.git/': Failed to connect to github.com port 443 after 21065 ms: Couldn't connect to server
>   ```

## 8

git 设置代理

(因为有时可能会 git clone 不了)

[【git错误】Error: Failed to connect to github.com port 443 after 21074 ms: Timed out_Sheyami的博客-CSDN博客](https://blog.csdn.net/Sheyami/article/details/121631887)

```bash
git config --global http.proxy http://127.0.0.1:7890
git config --global https.proxy http://127.0.0.1:7890
```

## 9

>   [复现代码](https://ronaldln.github.io/MyPamphlet-Blog/2023/10/04/)

git bash 中在运行命令是，可以*环境变量(或者叫全局变量？)*，如

```bash
HF_DATASETS_OFFLINE=1 TRANSFORMERS_OFFLINE=1 \
python examples/pytorch/translation/run_translation.py --model_name_or_path t5-small --dataset_name wmt16 --dataset_config ro-en ...
```

或

```bash
# Make sure you have git-lfs installed (https://git-lfs.com)
git lfs install
git clone https://huggingface.co/decapoda-research/llama-7b-hf

# if you want to clone without large files – just their pointers
# prepend your git clone with the following env var:
GIT_LFS_SKIP_SMUDGE=1
```

## 10

可以使用 `--amend` 来修改上一次 `commit` 提交

```bash
usage: git commit [-a | --interactive | --patch] [-s] [-v] [-u<mode>] [--amend]
                  [--dry-run] [(-c | -C | --squash) <commit> | --fixup [(amend|reword):]<commit>)]
                  [-F <file> | -m <msg>] [--reset-author] [--allow-empty]
                  [--allow-empty-message] [--no-verify] [-e] [--author=<author>]
                  [--date=<date>] [--cleanup=<mode>] [--[no-]status]
                  [-i | -o] [--pathspec-from-file=<file> [--pathspec-file-nul]]
                  [(--trailer <token>[(=|:)<value>])...] [-S[<keyid>]]
                  [--] [<pathspec>...]
    ...
    --amend               amend previous commit
```

```bash
git commit --amend -m "..."
```

## 11

学习 git 的视频

[Git + GitHub 10分钟完全入门_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1KD4y1S7FL)

[Git + GitHub 10分钟完全入门 (进阶)_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1hA411v7qX)

[GitHub 到底怎么用？十分钟学会 GitHub 基础知识_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1yo4y1d7UK)

## 12

github 提交 *PR Pull requests* 的方法，

**需要先将别人的仓库 ==fork== 到自己的仓库中，然后进行修改**，

之后就可以在自己 fork 的仓库或者原本的仓库中提交 *PR Pull requests*

## 13

查看仓库关联的远程库的命令

```bash
git remote -v
```

将本地仓库关联多个远程库

**方法一** (不能同时推送)

[Gitee导入Github仓库并同步更新_gitee强制同步-CSDN博客](https://blog.csdn.net/m0_46157986/article/details/109530672)

关联的远程库名默认为 `origin` ，

添加新的远程库

```bash
git remote add github git@github.com:RonaldLN/Exam-for-Software-of-DRB-of-2023.git
```

`github` 处可以改成其他(自定义的)远程库名，最后是远程库的地址，

添加后，进行 `git remote -v` 查看会发现

```bash
github  git@github.com:RonaldLN/Exam-for-Software-of-DRB-of-2023.git (fetch)
github  git@github.com:RonaldLN/Exam-for-Software-of-DRB-of-2023.git (push)
origin  git@gitee.com:ronald-luo/test.git (fetch)
origin  git@gitee.com:ronald-luo/test.git (push)
```

因此在 `git push` 时需要选择要推送的远程库的库名进行推送

```bash
git push -u xxx branch
```

>   删除关联的远程库的命令
>
>   ```bash
>   git remote rm xxx
>   ```

**方法二** (可以同时推送)

[Git同时推送多个远程仓库 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/141941373)

由于默认关联的远程库名是 `origin` ，

所以通过

```bash
git remote set-url --add origin git@github.com:RonaldLN/Exam-for-Software-of-DRB-of-2023.git
```

来在 `origin` 库名下添加远程库，

然后 `git remote -v` 查看

```bash
origin  git@gitee.com:ronald-luo/test.git (fetch)
origin  git@gitee.com:ronald-luo/test.git (push)
origin  git@github.com:RonaldLN/Exam-for-Software-of-DRB-of-2023.git (push)
```

因此在推送 `origin` 时就会向 github 和 gitee 一起推送

## 14

修改本地分支名的命令

```bash
git branch -m oldName newName
```

## 15

将两个远程仓库克隆到一个本地仓库的两个分支，并且合并的方法

[如何合并两个不同的 Git 仓库？ - 知乎 (zhihu.com)](https://www.zhihu.com/question/633582071)

## 16

如果仓库中的某个文件夹，里面有 `.git/` 文件夹，即是另一个仓库，那么这个文件夹中的文件不会被git识别到

## 17

添加submodule

```bash
git submodule add xxx.git [路径]
```

## 18

在windows上安装 [`git-filter-repo`](https://github.com/newren/git-filter-repo) ，

参考 [python - `git filter-repo` commands output nothing on Windows - Stack Overflow](https://stackoverflow.com/questions/69355161/git-filter-repo-commands-output-nothing-on-windows) 中 [TTT的回答](https://stackoverflow.com/a/69356543)

1.   运行 `git --exec-path` 查看 `git.exe` 所在的路径
2.   下载 [`git-filter-repo`](https://github.com/newren/git-filter-repo/blob/main/git-filter-repo) 文件(注意不要有后缀，可能下载会自动添加 `.txt` 后缀)，并将 `git-filter-repo` 复制到 `git.exe` 所在的路径
3.   在需要运行 `git filter-repo` 命令的仓库/路径下，尝试运行命令
     -   如果命令能正常运行，会显示 `No arguments specified.` ，那么就不用执行下一步
4.   如果没有显示的信息，或者显示类似于 `/usr/bin/env: ‘python3’: No such file or directory` 的报错信息，那么将 `git-filter-repo` 文件第一行 `#!/usr/bin/env python3` 中的 `python3` 换成 `python`

## 19

[将子文件夹拆分成新仓库 - GitHub 文档](https://docs.github.com/zh/get-started/using-git/splitting-a-subfolder-out-into-a-new-repository)

需要安装 [`git-filter-repo`](https://github.com/newren/git-filter-repo) ，

有两种拆分的形式：

1.   只保留某个子文件夹到新仓库中，git的历史记录里也只会保留与这个文件夹相关的commit

     ```bash
     git filter-repo --path FOLDER-NAME/
     ```

     >   Filter the specified branch in your directory and remove empty commits

2.   将某个子文件夹作为新仓库的根目录，即把该子文件夹作为一个新的仓库，并只保留相关的commit(commit中文件的路径会自动进行更改)

     ```bash
     git filter-repo --subdirectory-filter FOLDER-NAME
     ```

     >   Filter the specific branch by using a single sub-directory as the root for the new repository

## 20

windows升级git

>   [How to upgrade Git on Windows to the latest version - Stack Overflow](https://stackoverflow.com/questions/13790592/how-to-upgrade-git-on-windows-to-the-latest-version)

[Dutch Glory的回答](https://stackoverflow.com/a/48924212)提到windows中可以使用以下命令升级git

```bash
git update-git-for-windows
```

## 21

如果clone下来的仓库中有submodule子模块，但对应路径只有一个空文件夹，那么可以使用 `--init` 参数来拉取对应的文件

>   `--recursive` 表示递归对所有嵌套子模块进行操作

```bash
git submodule update --init --recursive
```

---

如果submodule子模块中有*大文件*，那么可以使用这样的命令对所有submodule拉取大文件

```bash
git submodule foreach git lfs pull
```

## 22

如果想在clone的时候就顺便把submodule一并克隆好，添加一个 `--recurse-submodules` 参数

```bash
git clone --recurse-submodules
```

## 23

可以使用 `git archive` 命令来打包(某个分支的)代码

```bash
git archive main --format=tar.gz --output=/path/to/main.tar.gz
```

或者使用zip格式打包

```bash
git archive main --format=zip --output=main.zip
```

