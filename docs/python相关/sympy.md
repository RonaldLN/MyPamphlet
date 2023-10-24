# SymPy

## 1

[Quick examples · sympy/sympy Wiki (github.com)](https://github.com/sympy/sympy/wiki/Quick-examples)

## 2

`diff()`函数用来求导，用法 `diff(func, x, n)` ，func是要求导的函数，x是要对其求导的变量，n是可选的，表示求n阶导数，默认为1阶导数。(或 `diff(func, x, x, x, ...)`)

```python
from sympy import symbols, diff

# 定义二元函数
x, y = symbols('x y')
f = x**2 + 2*x*y + y**2

# 对x求偏导数
df_dx = diff(f, x)
print("对x求偏导数：", df_dx)

# 对y求偏导数
df_dy = diff(f, y)
print("对y求偏导数：", df_dy)
```

`.diff()`方法也可以用来求导，用法`func.diff(x, n)` (x为求导的变量，n为阶数)或`func.diff(x, x, x, ...)` (依次求导的变量)，则对 $f(x)$ 求三阶导为

```python
f(x).diff(x, 3)
```

或

```python
f(x).diff(x, x, x)
```

## 3

`Derivative`类构造方法与 `diff()`函数较为类似，使用方法也为 `Derivative(func, x, n)` 或 `Derivative(func, x, x, x, ...)`，但如果函数 `func` 为一个具体的函数时，前者不输出求导的结果，而输出求导的表达式，后者输出导函数，如

```python
g = x ** 2 + 2 * x + 1
write_latex_md(latex(Derivative(g, x, x)))
write_latex_md(latex(diff(g, x, x)))
```

结果分别为
$$
\frac{d^{2}}{d x^{2}} \left(x^{2} + 2 x + 1\right)
$$

和

$$
2
$$
而使用 `.doit()` 方法像后者一样可以输出导函数

## 4

使用 `Rational` 类可以表示分数，如

```python
Rational(3,2)*pi
```

输出为
$$
\frac{3 \pi}{2}
$$
若写成

```python
3 / 2 * pi
```

则输出为
$$
1.5\pi
$$

## 5

`symbols.()` 

```python
x, y, z = symbols('x,y,z')
a, b, c = symbols('a b c')

>>> symbols('x:10')
(x0, x1, x2, x3, x4, x5, x6, x7, x8, x9)

>>> symbols('x5:10')
(x5, x6, x7, x8, x9)
>>> symbols('x5(:2)')
(x50, x51)

>>> symbols('x5:10,y:5')
(x5, x6, x7, x8, x9, y0, y1, y2, y3, y4)

>>> symbols(('x5:10', 'y:5'))
((x5, x6, x7, x8, x9), (y0, y1, y2, y3, y4))
```

## 6

要让sympy显示图像，需要安装matplotlib包

```bash
pip install matplotlib
```

## 7

>   [2023数模国赛](https://ronaldln.github.io/MyPamphlet-Blog/2023/09/08/2023/)

如果需要在函数或方程中添加对数函数，需要使用sympy包里的 `log(x, y)` 函数(x为真数，y为底数)

(如果在导入sympy包时，使用 `from sympy import *` 则可能会使得 python 的 math 里的求对数的函数被覆盖)

---

??? example "chat log"

    **user**: 
    
    sympy怎么使用?
    
    **bing**: 
    
    [1]: https://zhuanlan.zhihu.com/p/609928549 "python的SymPy库如何使用 - 知乎 - 知乎专栏"
    [2]: https://zhuanlan.zhihu.com/p/60509430 "用Python学数学之Sympy代数符号运算 - 知乎 - 知乎专栏"
    [3]: https://geek-docs.com/python/python-tutorial/python-sympy.html "SymPy 教程|极客教程"
    [4]: https://zhuanlan.zhihu.com/p/96738286 "用 Python 来研究数学 --- SymPy 符号工具包介绍 - 知乎"
    [5]: https://zhuanlan.zhihu.com/p/111573239 "SymPy 符号计算基本教程 - 知乎"
    
    SymPy 是一款用于符号计算的 Python 库，可以进行符号计算、符号代数、微积分、方程式求解、数值计算等操作。以下是 SymPy 库的基本使用方法： 
    
    1. 安装 SymPy 库; 在命令行中输入 pip install sympy，即可安装 SymPy 库。如果已经安装了 Anaconda，可以直接使用 conda install sympy 命令安装。 
    2. 导入 SymPy 库; 在 Python 代码中导入 SymPy 库，如下所示：
    ```python
    from sympy import *
    ```
    3. 使用 SymPy 库; 例如，要求解方程式 x^2 + 2x + 1 = 0，可以使用以下代码：
    ```python
    from sympy import *
    x = symbols('x')
    solve(x**2 + 2*x + 1, x)
    ```
    这将返回 [-1]，即方程式的解为 -1。
    
    希望这能帮到你！


    **user**: 
    
    Rational函数有什么作用？
    
    **bing**: 
    
    [1]: https://zhuanlan.zhihu.com/p/31211594 "1.5.2 Rational functions - 知乎 - 知乎专栏"
    [2]: https://en.wikipedia.org/wiki/Rational_function "Rational function - Wikipedia"
    [3]: https://openstax.org/books/college-algebra-2e/pages/5-6-rational-functions "5.6 Rational Functions - College Algebra 2e | OpenStax"
    
    有理函数是任何可以由有理分式定义的函数，其中有理分式是一种代数分式，其分子和分母都是多项式。多项式的系数不必是有理数；它们可以在任何域K中取值[^1^][2]。
    
    有理函数在数学中有广泛的应用，例如在微积分中，有理函数是一类可以被积分的函数。在代数几何中，有理函数是一类可以被定义在代数簇上的函数。[^1^][2]
    
    希望这能回答你的问题！


    **user**: 
    
    sympy中的 rational有什么作用？
    
    **bing**: 
    
    [1]: https://bing.com/search?q=sympy%E4%B8%AD%E7%9A%84rational%E5%87%BD%E6%95%B0%E6%9C%89%E4%BB%80%E4%B9%88%E4%BD%9C%E7%94%A8%EF%BC%9F "SymPy 教程|极客教程"
    [2]: https://geek-docs.com/sympy/sympy-tutorial/python-sympy-is_rational-method.html "Python sympy.is_rational方法 - 极客教程"
    [3]: https://geek-docs.com/sympy/sympy-tutorial/python-sympy-rational-method.html "Python sympy.Rational()方法|极客教程"
    [4]: https://geek-docs.com/python/python-tutorial/python-sympy.html "SymPy 教程|极客教程"
    [5]: https://zhuanlan.zhihu.com/p/96738286 "用 Python 来研究数学 --- SymPy 符号工具包介绍 - 知乎"
    [6]: https://zhuanlan.zhihu.com/p/111573239 "SymPy 符号计算基本教程 - 知乎 - 知乎专栏"
    
    在SymPy中，Rational函数是用于处理有理数的函数。有理数是可以表示为两个整数（分子p和非零分母q）的商或分数p/q的任何数字。Rational函数可以将浮点数转换为有理数形式，也可以检查元素是否为有理数，返回布尔值True或False[^1^][1] [^2^][2] [^3^][3].
    
    希望这能回答你的问题！


    **user**: 
    
    如何在py文件中调用某个软件打开某个文件？
    
    **bing**: 
    
    [1]: https://blog.csdn.net/weixin_47702737/article/details/121721523 "Linux终端如何运行py文件【python代码文件】 - CSDN博客"
    [2]: https://www.zhihu.com/question/51290977 "在python交互模式中怎么运行py文件? - 知乎"
    [3]: https://blog.csdn.net/gsgbgxp/article/details/117042635 "python调用另一个.py文件中的类和函数或直接运行另一个.py文件_python引用其他py文件的函数_gsgbgxp的博客-CSDN博客"
    [4]: https://blog.csdn.net/qq_37235616/article/details/107576352 "python文件中执行另一个python文件教程 相当于直接run python文件_python执行另一个python文件_chestnut ..."
    
    你可以使用Python的subprocess模块来调用其他软件。例如，如果你想在Windows上使用记事本打开一个文件，你可以使用以下代码：
    
    ```python
    import subprocess
    subprocess.Popen(['notepad.exe', 'file.txt'])
    ```
    
    这将打开记事本并打开名为file.txt的文件。[^1^][1] [^2^][2] [^3^][3]
    
    希望这能回答你的问题！


    **user**: 
    
    如果我想使用其他软件呢，比如vs code
    
    **bing**: 
    
    [1]: https://blog.csdn.net/letianxf/article/details/121532945 "使用命令行打开vscode_一天一丢丢的博客-CSDN博客"
    [2]: https://www.py.cn/tools/anaconda/19889.html "怎么在vscode上使用anaconda - Python学习网"
    [3]: https://zhuanlan.zhihu.com/p/64994681 "Python in VS Code：环境配置 - 知乎 - 知乎专栏"
    [4]: https://zhuanlan.zhihu.com/p/142642410 "Python 使用VS Code进行调试 - 知乎 - 知乎专栏"
    [5]: https://code.visualstudio.com/docs/languages/python "Python in Visual Studio Code"
    [6]: https://zhuanlan.zhihu.com/p/258899307 "如何使用python打开及读写文件（基础篇） - 知乎专栏"
    
    你可以使用Python的subprocess模块来调用其他软件。例如，如果你想在Windows上使用VS Code打开一个文件，你可以使用以下代码：
    
    ```python
    import subprocess
    subprocess.Popen(['code', 'file.txt'])
    ```
    
    这将打开VS Code并打开名为file.txt的文件。[^1^][1] [^2^][2] [^3^][3]
    
    希望这能回答你的问题！


    **user**: 
    
    diff函数怎么用？
    
    **bing**: 
    
    [1]: https://www.runoob.com/python3/ref-set-difference.html "Python Set difference() 方法 | 菜鸟教程"
    [2]: https://blog.csdn.net/fanlily913/article/details/109297994 "python 中的求导和偏导——diff函数和symbols函数 - CSDN博客"
    [3]: https://www.jianshu.com/p/eef13cc2ca1e "pandas常用函数之diff - 简书"
    [4]: https://blog.csdn.net/ggdhs/article/details/89913421 "@ Python 学习随笔——利用sympy模块中的diff函数来实现对函数的求导_diff sympy_乖乖的函数的博客-CSDN博客"
    [5]: https://numpy.org/doc/stable/reference/generated/numpy.diff.html "numpy.diff — NumPy v1.25 Manual"
    
    在Python中，diff函数可以有不同的含义，具体取决于你使用的库。例如，如果你使用的是Python的set库，那么difference()方法可以用于返回集合的差集，即返回的集合元素包含在第一个集合中，但不包含在第二个集合中。
    
    **user**: 
    
    sympy的diff函数怎么用？
    
    **bing**: 
    
    [1]: https://bing.com/search?q=sympy%E7%9A%84diff%E5%87%BD%E6%95%B0%E6%80%8E%E4%B9%88%E7%94%A8%EF%BC%9F "Python sympy.diff()用法及代码示例 - 纯净天空"
    [2]: https://geek-docs.com/sympy/sympy-method/python-sympy-diff-method.html "sympy.diff()方法|极客教程"
    [3]: https://www.zhihu.com/question/54619210 "python sympy库用于求导的函数是什么？ - 知乎"
    [4]: https://zhuanlan.zhihu.com/p/533559325 "python科学计算05-利用python的sympy进行导数和偏导数计算 - 知乎"
    [5]: https://blog.csdn.net/ggdhs/article/details/89913421 "@ Python 学习随笔——利用sympy模块中的diff函数来实现对函数的求导_diff sympy_乖乖的函数的博客-CSDN博客"
    [6]: https://zhuanlan.zhihu.com/p/96738286 "用 Python 来研究数学 --- SymPy 符号工具包介绍 - 知乎"
    
    在Python中，你可以使用sympy库中的diff()函数来求导数。diff()函数的基本用法是：diff(func,x,n)，其中，func是要求导的函数，x是要对其求导的变量，n是可选的，表示求n阶导数，默认为1阶导数。[^1^][1] [^2^][3] [^3^][4]
    
    例如，如果你想对一个二元函数求偏导数，你可以使用以下代码：[^4^][5]
    
    ```python
    from sympy import symbols, diff
    
    # 定义二元函数
    x, y = symbols('x y')
    f = x**2 + 2*x*y + y**2
    
    # 对x求偏导数
    df_dx = diff(f, x)
    print("对x求偏导数：", df_dx)
    
    # 对y求偏导数
    df_dy = diff(f, y)
    print("对y求偏导数：", df_dy)
    ```
    
    希望这能回答你的问题！


    **user**: 
    
    ```python
    from sympy import *
    f(x).diff(x, x)
    ```
    是什么意思
    
    **bing**: 
    
    这段代码的意思是：定义一个函数f(x)，然后对这个函数连续求两次导数。
    
    其中，f(x).diff(x, x)表示对f(x)这个函数进行两次求导，即求二阶导数。
    
    希望这能回答你的问题！


    **user**: 
    
    那么如果求f(x)三阶导，应该如何写？
    
    **bing**: 
    
    如果要求f(x)的三阶导数，你可以使用以下代码：
    
    ```python
    from sympy import *
    f(x).diff(x, 3)
    ```
    
    其中，diff()函数的第二个参数表示要求的导数阶数，这里是3，即求三阶导数。
    
    希望这能回答你的问题！


    **user**: 
    
    那么二阶导数为什么是f(x).diff(x,x)
    
    **bing**: 
    
    在Python中，你可以使用sympy库中的diff()函数来求导数。diff()函数的基本用法是：diff(func,x,n)，其中，func是要求导的函数，x是要对其求导的变量，n是可选的，表示求n阶导数，默认为1阶导数。
    
    因此，f(x).diff(x,x)表示对f(x)这个函数进行两次求导，即求二阶导数。
    
    希望这能回答你的问题！


    **user**: 
    
    那么 sympy Derivative函数是什么意思？
    
    **bing**: 
    
    [1]: https://www.demo2s.com/python/python-sympy-derivatives.html "Python SymPy Derivatives"
    [2]: https://www.tutorialspoint.com/sympy/sympy_derivative.htm "SymPy - Derivative - Online Tutorials Library"
    [3]: https://geek-docs.com/sympy/sympy-tutorial/python-sympy-derivative-method.html "Python sympy.Derivative()方法 - 极客教程"
    [4]: https://www.geeksforgeeks.org/python-sympy-derivative-method/ "Python | sympy.Derivative() method - GeeksforGeeks"
    [5]: https://docs.sympy.org/latest/tutorials/intro-tutorial/calculus.html "Calculus - SymPy 1.12 documentation"
    [6]: https://zhuanlan.zhihu.com/p/96738286 "用 Python 来研究数学 --- SymPy 符号工具包介绍 - 知乎"
    
    在Python中，你可以使用sympy库中的Derivative()函数来求导数。Derivative()函数的基本用法是：Derivative(func,x)，其中，func是要求导的函数，x是要对其求导的变量。
    
    与diff()函数不同的是，Derivative()函数返回一个未评估的导数，而不是已经计算出来的导数。如果要计算这个导数，你可以使用doit()方法。
    
    例如，如果你想对一个函数f(x)求一阶导数，你可以使用以下代码：[^1^][1]
    
    ```python
    from sympy import symbols, Derivative
    
    # 定义函数
    x = symbols('x')
    f = x**2 + 2*x + 1
    
    # 对x求一阶导数
    df_dx = Derivative(f, x).doit()
    print("对x求一阶导数：", df_dx)
    ```
    
    希望这能回答你的问题！


    **user**: 
    
    如何使用sympy求解微分方程组？
    
    **bing**: 
    
    [1]: https://blog.csdn.net/linshen1213/article/details/99433348 "Python解微分方程_python求解微分方程_林重言的博客-CSDN博客"
    [2]: https://www.cnblogs.com/zyg123/p/10549354.html "5.5Python数据处理篇之Sympy系列(五)---解方程 - 梦并不遥远 - 博客园"
    [3]: https://zhuanlan.zhihu.com/p/599865732 "「SymPy」符号运算(3) (非)线性方程(组)求解、数列求和、连乘、求极限 - 知乎"
    [4]: https://zhuanlan.zhihu.com/p/111573239 "SymPy 符号计算基本教程 - 知乎 - 知乎专栏"
    [5]: https://blog.csdn.net/Jarrodche/article/details/99546070 "Sympy符号计算（使用python求导，解方程组） - CSDN博客"
    
    在Python中，你可以使用sympy库中的dsolve()函数来求解微分方程组。dsolve()函数的基本用法是：dsolve(equations)，其中，equations是微分方程组。
    
    例如，如果你想求解一个二阶微分方程组y'' + y = 0，你可以使用以下代码：[^1^][1]
    
    ```python
    from sympy import symbols, Function, dsolve
    
    # 定义函数
    x = symbols('x')
    y = Function('y')(x)
    
    # 求解微分方程组
    dsolve(y.diff(x, x) + y, y)
    ```
    
    希望这能回答你的问题！


    **user**: 
    
    如何使用 sympy 求解 二元二阶线性微分方程组
    
    **bing**: 
    
    在Python中，你可以使用sympy库中的dsolve()函数来求解微分方程组。dsolve()函数的基本用法是：dsolve(equations)，其中，equations是微分方程组。
    
    例如，如果你想求解一个二元二阶线性微分方程组，你可以使用以下代码：
    
    ```python
    from sympy import symbols, Function, dsolve
    
    # 定义函数
    x = symbols('x')
    y1 = Function('y1')(x)
    y2 = Function('y2')(x)
    
    # 求解微分方程组
    dsolve((y1.diff(x, x) + y1 + y2.diff(x), y2.diff(x, x) + y2 - y1), (y1, y2))
    ```
    
    希望这能回答你的问题！

