## 1

pip换源北外

[pypi | 镜像站使用帮助 | 北京外国语大学开源软件镜像站 | BFSU Open Source Mirror](https://mirrors.bfsu.edu.cn/help/pypi/)

**临时使用**

```
pip install -i https://mirrors.bfsu.edu.cn/pypi/web/simple some-package
```

注意，`simple` 不能少, 是 `https` 而不是 `http`

**设为默认**

升级 pip 到最新的版本 (>=10.0.0) 后进行配置：

```bash
python -m pip install --upgrade pip
pip config set global.index-url https://mirrors.bfsu.edu.cn/pypi/web/simple
```

## 2

pip 升级某个包

```bash
pip install [-U / --updrade] xxx
```

## 3

安装某个版本的包

```bash
pip install xxx==x.x.x
```

## 4

pip 安装某个本地的 包 / `.whl` 文件，直接 `pip install xxx.whl` 即可

```bash
pip install xxx.whl
```

## 5

[Python查看第三方库、包的所有可用版本，历史版本_python 2.7 pip查询可用库版本-CSDN博客](https://blog.csdn.net/u011519550/article/details/88890382)

如果想查询要安装的包所有可以安装的版本

可以这样

```bash
pip install xxx==
```

或者等号后可以写任何不是对应版本号的东西，然后就会返回类似于这样的信息

```bash
>pip install numpy==tst
Looking in indexes: https://mirrors.bfsu.edu.cn/pypi/web/simple/
ERROR: Could not find a version that satisfies the requirement numpy==tst (from versions: 1.3.0, 1.4.1, 1.5.0, 1.5.1, 1.6.0, 1.6.1, 1.6.2, 1.7.0, 1.7.1, 1.7.2, 1.8.0, 1.8.1, 1.8.2, 1.9.0, 1.9.1, 1.9.2, 1.9.3, 1.10.0.post2, 1.10.1, 1.10.2, 1.10.4, 1.11.0, 1.11.1, 1.11.2, 1.11.3, 1.12.0, 1.12.1, 1.13.0, 1.13.1, 1.13.3, 1.14.0, 1.14.1, 1.14.2, 1.14.3, 1.14.4, 1.14.5, 1.14.6, 1.15.0, 1.15.1, 1.15.2, 1.15.3, 1.15.4, 1.16.0, 1.16.1, 1.16.2, 1.16.3, 1.16.4, 1.16.5, 1.16.6, 1.17.0, 1.17.1, 1.17.2, 1.17.3, 1.17.4, 1.17.5, 1.18.0, 1.18.1, 1.18.2, 1.18.3, 1.18.4, 1.18.5, 1.19.0, 1.19.1, 1.19.2, 1.19.3, 1.19.4, 1.19.5, 1.20.0, 1.20.1, 1.20.2, 1.20.3, 1.21.0, 1.21.1, 1.21.2, 1.21.3, 1.21.4, 1.21.5, 1.21.6, 1.22.0, 1.22.1, 1.22.2, 1.22.3, 1.22.4, 1.23.0rc1, 1.23.0rc2, 1.23.0rc3, 1.23.0, 1.23.1, 1.23.2, 1.23.3, 1.23.4, 1.23.5, 1.24.0rc1, 1.24.0rc2, 1.24.0, 1.24.1, 1.24.2, 1.24.3, 1.24.4, 1.25.0rc1, 1.25.0, 1.25.1, 1.25.2, 1.26.0b1, 1.26.0rc1, 1.26.0)
ERROR: No matching distribution found for numpy==tst
```

