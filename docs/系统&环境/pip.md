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

