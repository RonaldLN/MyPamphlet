## 1

通过 `figure(num)` 方法创建多个窗口，并且可以通过参数 `figsize=(width, height)` 设置窗口的大小

且，设置图例( `legned()` )、坐标轴标签和标题( `title("text")` )的函数只对代码中最近的窗口有效

## 2

保存图像的方法

>   ```python
>   from matplotlib import pyplot as plt
>   ```

`plt.savefig()` 可以把图像保存成图片，但是会把之前添加过的数据都放在一个图里面

我就每次输出成文件后清除数据

```python
plt.savefig(path + '.png')
plt.clf()
```

---

??? example "chat log"

    **user**: 
    
    matplotlib怎么打印两张图？
    
    **chatgpt**: 
    
    要在 Matplotlib 中打印两张图，可以使用 `plt.subplot()` 函数或 `plt.subplots()` 函数来创建子图。下面是使用 `plt.subplot()` 函数打印两张图的示例代码：
    
    ```python
    import matplotlib.pyplot as plt
    import numpy as np
    
    # 创建数据
    x = np.linspace(0, 2 * np.pi, 100)
    y1 = np.sin(x)
    y2 = np.cos(x)
    
    # 绘制第一张图
    plt.subplot(2, 1, 1)
    plt.plot(x, y1)
    plt.title('Sin')
    
    # 绘制第二张图
    plt.subplot(2, 1, 2)
    plt.plot(x, y2)
    plt.title('Cos')
    
    # 显示图像
    plt.show()
    ```
    
    在上面的代码中，`plt.subplot(2, 1, 1)` 创建了一个 2 行 1 列的子图网格，并将当前的 Axes 对象设置为第一个子图。然后，我们使用 `plt.plot()` 函数绘制第一个图，并使用 `plt.title()` 函数添加标题。接下来，`plt.subplot(2, 1, 2)` 设置当前的 Axes 对象为第二个子图，并绘制第二个图。最后，我们调用 `plt.show()` 函数显示图像。
    
    如果你想要更灵活地控制子图的布局，可以使用 `plt.subplots()` 函数。下面是使用 `plt.subplots()` 函数打印两张图的示例代码：
    
    ```python
    import matplotlib.pyplot as plt
    import numpy as np
    
    # 创建数据
    x = np.linspace(0, 2 * np.pi, 100)
    y1 = np.sin(x)
    y2 = np.cos(x)
    
    # 创建子图
    fig, axs = plt.subplots(2, 1, figsize=(6, 6))
    
    # 绘制第一张图
    axs[0].plot(x, y1)
    axs[0].set_title('Sin')
    
    # 绘制第二张图
    axs[1].plot(x, y2)
    axs[1].set_title('Cos')
    
    # 调整子图之间的间距
    fig.tight_layout()
    
    # 显示图像
    plt.show()
    ```
    
    在上面的代码中，`plt.subplots(2, 1, figsize=(6, 6))` 创建了一个 2 行 1 列的子图网格，并将返回的 Figure 对象和 Axes 对象存储在变量 `fig` 和 `axs` 中。然后，我们使用 `axs[0].plot()` 和 `axs[1].plot()` 函数分别在第一个和第二个子图中绘制图像，并使用 `axs[0].set_title()` 和 `axs[1].set_title()` 函数添加标题。最后，我们使用 `fig.tight_layout()` 函数调整子图之间的间距，并调用 `plt.show()` 函数显示图像。
    
    **user**: 
    
    如何打开figure2?
    
    **chatgpt**: 
    
    如果你想要打开 Matplotlib 中的第二个 Figure 窗口，可以使用 `plt.figure()` 函数创建一个新的 Figure 对象，并在调用 `plt.show()` 函数之前调用 `plt.figure()` 函数。
    
    下面是一个简单的示例代码，演示如何打开第二个 Figure 窗口：
    
    ```python
    import matplotlib.pyplot as plt
    import numpy as np
    
    # 创建数据
    x = np.linspace(0, 2 * np.pi, 100)
    y1 = np.sin(x)
    y2 = np.cos(x)
    
    # 创建第一个图形窗口
    plt.figure(1)
    plt.plot(x, y1)
    plt.title('Sin')
    
    # 创建第二个图形窗口
    plt.figure(2)
    plt.plot(x, y2)
    plt.title('Cos')
    
    # 显示图像
    plt.show()
    ```
    
    在上面的代码中，我们首先在 `plt.figure(1)` 中创建第一个图形窗口，并在其中绘制了一个正弦函数图像。然后，我们在 `plt.figure(2)` 中创建了第二个图形窗口，并在其中绘制了余弦函数图像。最后，我们调用 `plt.show()` 函数来显示这两个图形窗口。
    
    需要注意的是，每次调用 `plt.figure()` 函数都会创建一个新的 Figure 对象，并将其设为当前 Figure 对象。因此，如果你需要在多个 Figure 窗口中绘制不同的图形，请确保在每个 Figure 窗口中使用不同的 Figure 对象。
    
    **user**: 
    
    如何设置图形窗口的大小，比如显示更长的x轴
    
    **chatgpt**: 
    
    要设置 Matplotlib 中图形窗口的大小，可以使用 `plt.figure()` 函数的 `figsize` 参数。`figsize` 参数接受一个元组，用于指定图形窗口的宽度和高度，单位为英寸。
    
    例如，如果你想要显示更长的 x 轴，可以通过增加图形窗口的宽度来实现。下面是一个示例代码，演示如何设置图形窗口的大小：
    
    ```python
    import matplotlib.pyplot as plt
    import numpy as np
    
    # 创建数据
    x = np.linspace(0, 2 * np.pi, 100)
    y = np.sin(x)
    
    # 创建图形窗口，并设置大小
    plt.figure(figsize=(8, 4))
    
    # 绘制图像
    plt.plot(x, y)
    plt.xlabel('X')
    plt.ylabel('Y')
    plt.title('Sin')
    
    # 显示图像
    plt.show()
    ```
    
    在上面的代码中，我们使用 `plt.figure(figsize=(8, 4))` 函数创建一个大小为 8x4 英寸的图形窗口，然后在其中绘制了一个正弦函数图像。通过增加图形窗口的宽度，x 轴的长度也随之增加。
    
    需要注意的是，图形窗口的大小可能因操作系统和显示器而异，因此你可能需要根据实际情况调整窗口大小。