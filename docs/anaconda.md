## 1

Anaconda 换源

换源北外

-   Windows 在用户主目录执行 `conda config --set show_channel_urls yes` 生成 `.condarc` 文件

-   linux 主目录下已有 `.condarc` 文件

修改 `.condarc` 文件：

```yaml
channels:
  - defaults
show_channel_urls: true
default_channels:
  - https://mirrors.bfsu.edu.cn/anaconda/pkgs/main
  - https://mirrors.bfsu.edu.cn/anaconda/pkgs/r
  - https://mirrors.bfsu.edu.cn/anaconda/pkgs/msys2
custom_channels:
  conda-forge: https://mirrors.bfsu.edu.cn/anaconda/cloud
  msys2: https://mirrors.bfsu.edu.cn/anaconda/cloud
  bioconda: https://mirrors.bfsu.edu.cn/anaconda/cloud
  menpo: https://mirrors.bfsu.edu.cn/anaconda/cloud
  pytorch: https://mirrors.bfsu.edu.cn/anaconda/cloud
  pytorch-lts: https://mirrors.bfsu.edu.cn/anaconda/cloud
  simpleitk: https://mirrors.bfsu.edu.cn/anaconda/cloud
  deepmodeling: https://mirrors.bfsu.edu.cn/anaconda/cloud/
```

>   [anaconda | 镜像站使用帮助 | 北京外国语大学开源软件镜像站 | BFSU Open Source Mirror](https://mirrors.bfsu.edu.cn/help/anaconda/)

## 2

查看已有环境

```bash
conda info -e
```

或

```bash
conda env list
```

## 3

[Conda使用指南 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/44398592)

创建conda环境，`python=3.x`指定python版本

```bash
conda create [ -n / --name ] xxx python=3.x
```

从已有环境克隆一个新的环境

```bash
conda create -n xxx --clone env
```



```bash
activate env # 激活env环境

conda deactivate # 退出env环境
```

删除已有环境

```bash
conda remove -n env --all
```

## 4

pycharm 找不到 conda 可执行文件：

1.   Conda 可执行文件：`...\Anaconda3\Scripts\conda.exe`
2.   加载环境