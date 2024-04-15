# MediaPipe

## 1

一开始安装mediapipe时

```bash
pip install mediapipe
```

显示了如下报错

```bash
ERROR: Could not find a version that satisfies the requirement mediapipe (from versions: none)
ERROR: No matching distribution found for mediapipe
```

然后google搜索信息，在[github issues上的这个回答](https://github.com/google/mediapipe/issues/1325#issuecomment-847185114)上看到了官方文档中对这个情况的说明，

[mediapipe/docs/getting_started/troubleshooting.md at master · google/mediapipe (github.com)](https://github.com/google/mediapipe/blob/master/docs/getting_started/troubleshooting.md#python-pip-install-failure)

然后发现是由于最开始安装的python是32位的版本，所以重新去安装了64位的python (python-3.10.11-amd64.exe)

>   Please note that MediaPipe Python PyPI officially supports the **64-bit** version of Python 3.7 to 3.10 on the following OS:
>
>   -   x86_64 Linux
>   -   x86_64 macOS 10.15+
>   -   amd64 Windows

换成64位的python之后就可以正常 `pip install mediapipe` 了