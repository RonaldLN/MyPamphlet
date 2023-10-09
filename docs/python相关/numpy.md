## 1

[一个10分钟的numpy入门教程_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1Wy4y1h7ii)

## 2

>   [先进视觉](https://ronaldln.github.io/MyPamphlet-Blog/2023/09/29/2023/)

[numpy教程07---ndarray的保存与加载_ndarray保存-CSDN博客](https://blog.csdn.net/qq_38727995/article/details/124085766)

`ndarray` 类的输出和读取，可以用 `np` 类的方法输出和加载，有两种输出形式

-   二进制格式(输出成 `.npy` 文件)

    使用 `np.save("file", array)` 方法， `"file"` 是目标文件名，如果不加后缀，会自动添加 `.npy` 后缀，`array` 是 `ndarray` 实例

-   文本格式

    使用 `np.savetxt("fname", array)` 方法，`"fname"` 需要填写完整的文件名，`array` 是 `ndarray` 实例