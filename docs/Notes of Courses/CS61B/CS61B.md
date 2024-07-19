## Lecture 0 Intro, Hello World Java

### 1

![cs61b_1](images/cs61b_1.png){ loading=lazy }

java中所有函数都应该存在于类中，因此java中所有的函数都是*方法 method*

## HW 0

### 1

java中数组的使用方法

```java
int[] numbers = new int[3];
numbers[0] = 4;
numbers[1] = 7;
numbers[2] = 10;
System.out.println(numbers[1]);
```

或者

```java
int[] numbers = new int[]{4, 7, 10};
System.out.println(numbers[1]);
```

可以使用 `.length` 来获取数组的长度，例如

```java
int[] numbers = new int[]{4, 7, 10};
System.out.println(numbers.length);
```

### 2

>   In Java, the [`for` keyword](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/for.html) has the syntax below:
>
>   ```java
>   for (initialization; termination; increment) {
>       statement(s)
>   }
>   ```
>
>   The initialization, termination, and increment must be semicolon separated. Each of these three can feature multiple comma-separated statements, e.g.
>
>   ```java
>   for (int i = 0, j = 10; i < j; i += 1) {
>       System.out.println(i + j);
>   }
>   ```
>
>   Comma separated `for` loops should be used sparingly.

java中 `for` 的使用方法(跟c中差不多)

### 3

Exercise 4

??? note "code"

    ```java
    public class BreakContinue {
        public static void windowPosSum(int[] a, int n) {
            /** your code here */ 
            for (int i = 0; i < a.length; i += 1) {
                if (a[i] < 0) {
                    continue;
                }
    
                int sum = 0;
                for (int j = 0; j <= n; j += 1) {
                    if (i + j >= a.length) {
                        break;
                    }
                    sum += a[i + j];
                }
    
                a[i] = sum;
            }
        }
    
        public static void main(String[] args) {
            int[] a = {1, 2, -3, 4, 5, 4};
            int n = 3;
            windowPosSum(a, n);
    
            // Should print 4, 8, -3, 13, 9, 4
            System.out.println(java.util.Arrays.toString(a));
        }
    }
    ```

### 4

`for` 循环语句的增强

java中 `for` 可以有相似于python中列表推导式的用法(把数组中的元素解压出来)

```java
public class EnhancedForBreakDemo {
    public static void main(String[] args) {
        String[] a = {"cat", "dog", "laser horse", "ketchup", "horse", "horbse"};

        for (String s : a) {
            for (int j = 0; j < 3; j += 1) {
                System.out.println(s);
                if (s.contains("horse")) {
                    break;
                }                
            }
        }
    }
}
```

>   注意到，java中，字符串String有 `contain` 方法，可以**判断是否包含某个子字符串**

## Lecture 2 Defining and Using Classes

### 1

![cs61b_2](images/cs61b_2.png){ loading=lazy }

Josh演示了在终端中运行java文件的方法，

需要先使用 `javac` 来编译java文件，然后会生成class文件，

再使用 `java` 文件来运行class文件(输入命令时可以忽略 `.class` 后缀)

>   `cat` 命令可以在终端中输出/显示文件的内容

---

Josh提到运行java程序的两步步骤

>   ```mermaid
>   flowchart LR
>   a(Hello.java) --> b[Compiler<br><code>javac</code>] --> c(Hello.class) --> d[Interpreter<br><code>java</code>] --> e([stuff<br>happens])
>   ```

但Josh也提到这不是唯一(运行java程序)的方法

### 2

Josh演示了调用其他java文件中的函数

=== "DogLauncher.java"

    ```java
    public class DogLauncher {
        public static void main(String[] args) {
            Dog.makeNoise();
        }
    }
    ```

=== "Dog.java"

    ```java
    public class Dog {
        public static void makeNoise() {
            System.out.println("Bark!");
        }
    }
    ```

然后发现，同一目录下的java文件之间可以(像Josh演示的一样)直接相互调用函数(而不需要 `import` ，不同目录下不能这样直接调用)

### 3

直接通过 `类名.方法` 的方法只能调用 `static` 属性的函数(感觉有点类似于python中的类属性和实例属性的区别)，没有 `static` 的函数只能通过实例去调用

>   ```java
>   public class Dog {
>       public int weightInPounds;
>   
>       public void makeNoise() {
>           if (weightInPounds < 10) {
>               System.out.println("yip!");
>           } else if (weightInPounds < 30) {
>               System.out.println("bark.");
>           } else {
>               System.out.println("woooof!");
>           }
>       }
>   }
>   ```
>
>   如果直接使用类名去调用，
>
>   ```java
>   public class DogLauncher {
>       public static void main(String[] args) {
>           Dog.makeNoise();
>       }
>   }
>   ```
>
>   会有如下报错
>
>   ```java
>   DogLauncher.java:3 error: non-static method makeNoise() cannot be referenced from a static context:
>           Dog.makeNoise();
>   1 error
>   ```
>
>   如果修改成
>
>   ```java
>   public class DogLauncher {
>       public static void main(String[] args) {
>           Dog d = new Dog();
>           d.weightInPounds = 20;
>           d.makeNoise();
>       }
>   }
>   ```
>
>   就能正常编译

### 4

定义一个类的大概代码结构

![cs61b_3](images/cs61b_3.png){ loading=lazy }

### 5

在使用自定义的类来创建数组时，数组在创建时并**不会创建**类的对象，即

```java
Dog[] dogs = new Dog[2];
```

只会创建一个数组，并不会创建两个Dog实例

### 6

`static` 的函数不能调用实例的变量

### 7

在不是 `static` 的函数中，可以使用 `this` 来获得自身这个实例(与c中的 `this` 略有不同，c中 `this` 是指针，java中 `this` 不是指针)

### 8

Josh建议，对于类中的 `static` 的属性，使用类名去获取这个属性，而不要使用实例去获取这个属性

### 9

`static` 的函数中如果想要访问 非 `static` 的属性(即实例属性)，需要传入实例并通过实例来访问

### 10

Josh在课上提到了一个网站，和cs61a中的python tutor类似的网站，但是是java语言

[Java Visualizer (uwaterloo.ca)](https://cscircles.cemc.uwaterloo.ca/java_visualize/)

### 11

Josh提到，使用helper函数来把大问题分解成小问题，

并且这样做有几点好处

-   more narratively clear
-   easier to get right when you write it
-   easier to debug

---

然后Josh通过一个具体例子演示，

![cs61b_4](images/cs61b_4.png){ loading=lazy }

Josh展示如果代码写在一个函数中，大概是这样

```java
public static Dog[] largerThanFourNeighbors(Dog[] dogs) {
    for (int i = 0; i < dogs.length; i += 1) {
        boolean largest = true;

        for (int j = -2; j <= 2; j += 1) {
            if (i + j < 0) {
                continue;
            }
            if (i + j >= dogs.length) {
                break;
            }
            if (j == 0) {
                continue;
            }

            Dog neighbor = dogs[i + j];
            if (neighbor.weightInPounds > dogs[i].weightInPounds) {
                largest = false;
            }
        }
        ...
    }
}
```

而分成不同的函数去编写，就会看起来结构更加清晰，debug也会更方便

```java
public static Dog[] largerThanFourNeighbors(Dog[] dogs) {
    Dog[] returnDogs = new Dog[dogs.length];
    int cnt = 0;

    for (int i = 0; i < dogs.length; i += 1) {
        if (isBiggestOfFour(dogs, i)) {
            returnDogs[cnt] = dogs[i];
            cnt = cnt + 1;
        }
    }

    returnDogs = arrayWithNoNulls(returnDogs, cnt);
    return returnDogs;
}

/** cnt is the number of non-null items */
public static Dog[] arrayWithNoNulls(Dog[] dogs, int cnt) {
    Dog[] noNullDogs = new Dog[cnt];
    for (int i = 0; i < cnt; i += 1) {
        noNullDogs[i] = dogs[i];
    }
    return noNullDogs;
}

/** Return true if dogs[i] is larger than its four neighbors */
public static boolean isBiggestOfFour(Dog[] dogs, int i) {
    boolean isBiggest = true;
    for (int j = -2; j <= 2; j += 1) {
        int compareIndex = i + j;

        /* avoid comparing ourself to ourself */
        if (j == 0) {
            continue;
        }

        if (validIndex(dogs, i + j)) {
            if (dogs[compareIndex].weightInPounds > dogs[i].weightInPounds) {
                isBiggest = false;
            }
        }
    }
    return isBiggest;
}

public static boolean validIndex(Dog[] dogs, int i) {
    if (i < 0) {
        return false;
    }
    if (i >= dogs.length) {
        return false;
    }
    return true;
}
```

>   ```java
>   public static void main(String[] args) {
>       Dog[] dogs = new Dog[] {
>           new Dog(10),
>           new Dog(15),
>           new Dog(20),
>           new Dog(15),
>           new Dog(10),
>           new Dog(5),
>           new Dog(10),
>           new Dog(15),
>           new Dog(22),
>           new Dog(15),
>           new Dog(20),
>       };
>       Dog[] bigDogs = largerThanFourNeighbors(dogs);
>   
>       for (int k = 0; k < bigDogs.length; k += 1) {
>           System.out.print(bigDogs[k].weightInPounds + " ");
>       }
>       System.out.println();
>   }
>   ```

## Lecture 2 Q&A

### 1

![cs61b_5](images/cs61b_5.png){ loading=lazy }

Josh在演示时，发现他的IDEA中装有[Java Visualizer](https://plugins.jetbrains.com/plugin/11512-java-visualizer)的插件，能直接在IDEA中在调试时看到可视化的*环境图 environment diagram*，

感觉挺有用，于是也安装了这个插件

---

Josh调试时还用了一下*step over 步过*的操作，之前不太清楚 *步过 step over* 、 *步入 step into* 、 *步出 step out* 的具体含义，于是就去查了一下，

[【pycharm调试】Pycharm 断点跳转及 Step Over/Step Into/Step Out 等的使用_pycharm中的step over和-CSDN博客](https://xhfei.blog.csdn.net/article/details/106206166)

从这篇文章上了解到，

-   *步过 step over* 是如果这一行有调用其他函数，那么会执行完调用的函数，然后走到下一行代码

-   *步入 step into* 是如果这一行有调用其他函数，那么就会走到被调用函数的第一行代码

    >   如果这一行没有调用其他函数，那么*步过step over*和*步入 step into*效果就是一样的(都是走到下一行代码)
    
-   *步出 step out* 是结合*步入 step into*来使用的，*步出 step out*会执行完当前整个函数，然后回到前一个函数调用这个函数的位置

## Project 0

### 1

由于在课程网站上没有找到能下载提供的初始代码的地方(课程网站上提供的方法是课程的学生从github上 `git pull` 自己对应学号的仓库)，

于是[在github上搜索 `cs61b sp21`](https://github.com/search?q=cs61b+sp21&type=repositories) 来搜索别人完成的作业仓库，看看能不能找到原始的代码，

然后点击最查看多star的仓库

[exuanbo/cs61b-sp21: CS 61B, Spring 2021 (github.com)](https://github.com/exuanbo/cs61b-sp21)

发现在 `README.md` 中有写着cs61b sp21的官方原始代码仓库

[Berkeley-CS61B/skeleton-sp21: starter code for spring 21 (github.com)](https://github.com/Berkeley-CS61B/skeleton-sp21)

于是就顺便发现了cs61b的[官方github账号](https://github.com/Berkeley-CS61B)

>   <h2>Public Access Resources</h2>
>
>   Previous course staff have made some iterations of this course available for auditors -- both Berkeley students and members of the public. While the assignment skeletons and specifications will be available for most years, some assignments have autograders that are not public. The most recent version with a public autograder is [Spring 2021](https://sp21.datastructur.es/about.html#auditing-cs61b).
>
>   Here's lints to the relevant materials:
>
>   -   [SP21 Course Website](https://sp21.datastructur.es/)
>   -   [Skeleton code](https://github.com/Berkeley-CS61B/skeleton-sp21)
>   -   [Java Libraries](https://github.com/Berkeley-CS61B/library-sp21)
>   -   [Lecture Code](https://github.com/Berkeley-CS61B/lectureCode-sp21)
>
>   <h2>Tooling</h2>
>
>   61B uses some tools to run its course. These are the open-source ones that we maintain for ourselves and actively use.
>
>   -   [IntelliJ Plugin](https://github.com/Berkeley-CS61B/intellij-plugin) - A style checker
>   -   [Java Visualizer](https://github.com/elipsitz/java-visualizer-intellij-plugin) - An IntelliJ plugin to visualize the data layout in Java applications. Externally maintained.
>   -   [jh61b](https://github.com/Berkeley-CS61B/jh61b) - A JUnit executor to output test results in [Gradescope's format](https://gradescope-autograders.readthedocs.io/en/latest/specs/#output-format)
>   -   [BSAG](https://github.com/Berkeley-CS61B/BSAG) - A Better SimpleAutograder for custom Gradescope logic
>       -   [bsag-jh61b](https://github.com/Berkeley-CS61B/bsag-jh61b) - BSAG steps for jh61b components

### 2

说明中提到，框架代码使用了一种叫做 *模型-视图-控制器模式 Model-View-Controller Pattern (MVC)* 的模式

>   The MVC pattern divides our problem into three parts:
>
>   -   The **model** represents the subject matter being represented and acted upon – in this case incorporating the state of a board game and the rules by which it may be modified. Our model resides in the `Model` , `Side` , `Board` , and `Tile` classes. The instance variables of `Model` fully determine what the state of the game is. Note: You’ll only be modifying the `Model` class.
>   -   A **view** of the model, which displays the game state to the user. Our view resides in the `GUI` and `BoardWidget` classes.
>   -   A **controller** for the game, which translates user actions into operations on the model. Our controller resides mainly in the `Game` class, although it also uses the GUI class to read keystrokes.

### 3

java中判断是否为 `null` 可以使用 `==`

### 4

在尝试完成 `tilt` 函数的过程中，一共进行了3次尝试，

前两次尝试大致思路都是，每一列只遍历一次，然后标记空的位置和上一个*瓷砖 tile*(第2次尝试与第1次的区别在于，将处理每一列写成了一个函数)，

但是两次都是只能通过 `TestUpOnly` 而不能通过 `TestModel` 。

第3次尝试打算放弃这个思路，而是将每一小步都写成一个函数，并且**由于留意到题目说明中提到 `board.move` 方法如果合并了*瓷砖*会返回 `true`** 于是打算利用这一点，最后写完并debug完后，没想到不仅通过了 `TestUpOnly` 也通过了 `TestModel` (😮很震惊，不知道为什么)

??? note "code"

    ```java
    public boolean tilt(Side side) {
        ...
    
        board.setViewingPerspective(side);
        for (int i = 0; i < board.size(); i++) {
            if (processCol(i)) {
                changed = true;
            }
        }
        board.setViewingPerspective(Side.NORTH);
    
        ...
    }
    
    public boolean processCol(int col) {
        boolean changed = false;
        int size = board.size();
    
        boolean[] isMerged = new boolean[size];
        for (int i = 0; i < size; i++) {
            int row = size - i - 1;
            isMerged[row] = false;
    
            if (needMove(col, row)) {
                int target = findTarget(col, row, isMerged);
                boolean doMerge = board.move(col, target, board.tile(col, row));
    
                if (doMerge) {
                    isMerged[target] = true;
                    score += board.tile(col, target).value();
                }
    
                changed = true;
            }
        }
        return changed;
    }
    
    public boolean needMove(int col, int row) {
        Tile tile = board.tile(col, row);
        if (tile == null) {
            return false;
        } else if (row == board.size() - 1) {
            return false;
        } else {
            Tile upTile = board.tile(col, row + 1);
            return upTile == null || upTile.value() == tile.value();
        }
    }
    
    public int findTarget(int col, int row, boolean[] isMerge) {
        int target = findEmptyTarget(col, row);
    
        if (target + 1 < board.size() && !isMerge[target + 1]
                && board.tile(col, row).value() == board.tile(col, target + 1).value()) {
            target += 1;
        }
        return target;
    }
    
    public int findEmptyTarget(int col, int row) {
        int target = row;
        for (int i = row + 1; i < board.size(); i++) {
            if (board.tile(col, i) != null) {
                break;
            }
            target = i;
        }
        return target;
    }
    ```

### 5

不知道是什么原因，在我的电脑上运行后按方向键没有反应，

于是启动调式模式查看问题，发现在 `Game.java:37` 中

```java
String cmnd = _source.getKey();
```

按压左键后的 `cmnd` 是 `"向左箭头"` ，于是继续追踪函数，发现源头在 `GUISource.java:36` 处，

![cs61b_6](images/cs61b_6.png){ loading=lazy }

所以就在 `switch` 中新加了几个 `case`

```java
switch (command) {
    ...
    case "向上箭头" :
        command = "Up";
        break;
    case "向右箭头" :
        command = "Right";
        break;
    case "向下箭头" :
        command = "Down";
        break;
    case "向左箭头" :
        command = "Left";
        break;
    default :
        break;
}
```

然后就能正常运行并玩游戏了😄

## Lecture 3 Testing

### 1

java中判断两个数组中的元素是否相等，可以使用

```java
java.util.Arrays.equals(a, b);
```

---

java中有用于测试的工具junit，

例如测试数组是否和预期值一样，并且如果不一样可以显示出错的元素

```java
String[] input = {"i", "have", "an", "egg"};
String[] expected = {"an", "egg", "have", "i"};

org.junit.Assert.assertArrayEquals(expected, input);
```

### 2

java中字符串不能直接比较大小，可以使用 `str1.compareTo(str2)` 的方法(使用字符串的 `compareTo` 方法)比较，

-   如果小于传入的字符串，会返回 `-1`
-   相等返回 `0`
-   大于返回 `1`

### 3

![cs61b_7](images/cs61b_7.png){ loading=lazy }

在Josh的演示中发现，idea(可能其他jetbrains的ide也差不多)中的断点右键**可以添加条件**

### 4

编写的测试的函数，可以在non-static函数声明上添加*装饰符* `@org.junit.Test` ，然后就可以不用在 `main` 中调用这个函数，可以直接运行文件就可以进行测试，例如

```java
@org.junit.Test
public void testSort() {
    String[] input = {"i", "have", "an", "egg"};
    String[] expected  = {"an", "egg", "have", "i"};
    
    Sort.sort(input);
    
    org.junit.Assert.assertArrayEquals(expected, input);
}
```

---

为了方便，还可以

```java
import org.junit.Test;
```

然后就可以直接 `@Test` 既可以了

---

为了方便，还可以导入 `Assert`

```java
import org.junit.Assert.*;
```

### 5

Josh提到了一个概念，*测试驱动开发 Test-Driven Development (TDD)*，

![cs61b_8](images/cs61b_8.png){ loading=lazy }

大概意思是，如果要实现一个功能，先确定特征，再根据这个特征编写测试例子，一开始运行无法通过测试，所以编写代码以通过测试，然后再改进代码，循环往复

## Lecture 3 Q&A

### 1

有人提问python中的 `is` 和 `==` 分别对应java中的什么，

Josh说，java中 `==` 类似于python中的 `is` (会检查对象的地址)，而java中类的 `.equals()` 方法类似于python中的 `==` (python中自定义类需要实现 `__eq__` 方法)

---

在java中，如果没有重写 `equals` 方法，那么默认的 `equals` 方法是检查地址

### 2

有人提问，Josh演示

```java
System.out.println(5 + 6 + "hi" + 5 + 6);
```

最后显示出来是 `11hi56` ，

于是发现java是从左往右进行运算，一开始 `5 + 6` 得到 `11` ，然后 `+ "hi"` 得到 `"11hi"` ，因此最后就会得到 `"11hi56"`

## Lecture 4 References, Recursion, and Lists

### 1

如果自定义对象实例赋值给一个新的变量，并使用新的变量来修改属性，那么修改的是原实例本身的属性，例如

```java
Walrus a = new Walrus(1000, 8.3);
Walrus b;
b = a;
b.weight = 5;
System.out.println(a);
System.out.println(b);
```

```txt
weight: 5, tusk size: 8.30
weight: 5, tusk size: 8.30
```

## Lecture 4 Q&A

### 1

java中的String字符串(创建后)不能被修改

### 2

java中可以使用三目运算符(和c中一样)

## Lab 2

### 1

在Lab 2 Setup的One-Time Setup中，需要在IDEA的主界面(没有打开项目的界面)中打开设置，

windows中可以使用 ++ctrl+alt+s++ 打开设置界面，也可以在 `自定义 > 所有设置...` 中打开设置界面

### 2

一开始我使用的jdk是之前安装的azul zulu的jdk，但是lab 2 setup一直无法配置好maven，

于是就去装了oracel的openjdk 17，最后就可以运行了

### 3

>   This is because JUnit tests are short-circuiting – as soon as one of the asserts in a method fails, it will output the failure and move on to the next test.

如果测试的函数(添加了 `@Test` 的函数)中，有一个 `assert` 错了，那么就会直接报错，然后进行下一个要测试的函数

### 4

从 `IntList.java` 的 `of` 函数中发现，java中在声明函数时，可以使用 `...` 来以数组的形式获取传入的多个参数(类似于python中的 `*args` )，例如

```java
public static int max(int ...argList) {
    int result = 0;
    for (int i = 0; i < argList.length; i++) {
        if (argList[i] > result) {
            result = argList[i];
        }
    }
    return result;
}
```

## Lecture 5 SLLists, Nested Classes, Sentinel Nodes

### 1

Josh说，如果嵌套的类，里面的类如果不需要访问外面类的属性，那么可以加上 `static` 关键字，好处是可以节省一些空间，例如

```java
public class SLList {
    private static class IntNode {
        public int item;
        public IntNode next;
        public IntNode(int i, IntNode n) {
            item = i;
            next = n;
        }
        ...
    }
}
```

个人理解是，如果是non-static，那么每次实例化外面的类时，都会给实例添加这个属性，如果是static，那么就不会这样

### 2

Josh提到，java代码中一个 `public` 的函数配一个 `private` 的同名helper函数很常见

### 3

如果需要创建空链表，可以给链表添加 *哨兵节点 sentinel node* (即空的头节点)，就可以在实现链表的其他功能时，避免处理空链表的特殊情况

## Lecture 5 Q&A

### 1

有人提问关于Josh课上说的，嵌套在内部定义的类，如果把类设置成了 `private` 的属性，那么类的成员设置成 `public` 还是 `private` 都差别不大，

Josh回答，因为类设置成 `private` 之后，里面的方法和属性(在外层的类之外)就都无法访问到了(应该是连构造方法也无法访问到)，所以成员的属性是 `public` 还是 `private` 都一样

## Lecture 6 DLLists, Arrays

### 1

介绍了*双向链表 doubly linked list (DLList)* (与之对应的是*单向链表 singly linked list (SLList)* )，为了避免*双向链表*的头和尾都指向同一个*哨兵节点*的情况，

>   ![cs61b_9](images/cs61b_9.png){ loading=lazy }

提到了两种解决方法，

-   设置两个*哨兵节点*

    ![cs61b_10](images/cs61b_10.png){ loading=lazy }

-   或者，设置成循环的双向链表

    ![cs61b_11](images/cs61b_11.png){ loading=lazy }

### 2

如果想要链表结构储存不同的数据类型(而不重复实现代码)，可以在定义类时，在类名后使用 `<...>` 添加自定义名称，之后在声明对应变量的数据类型时，都使用这个名称，例如

```java
public class SLList<LochNess> {
    private class StuffNode {
        public LochNess item;
        public StuffNode next;
        
        public StuffNode(LochNess i, StuffNode n) {
            item = i;
            next = n;
        }
    }
    
    private StuffNode first;
    private int size;
    
    public SLList(LochNess x) {
        first = new StuffNode(x, null);
        size = 1;
    }
    
    ...
}
```

使用这个类时，则需要在 `<>` 中添加数据类型

```java 
SLList<String> s1 = new SLList<String>("bone");
```

也可以将构造函数的 `String` 去除

```java
SLList<String> s1 = new SLList<>("bone");
```

### 3

java中创建数组的3种方法，

```java
y = new int[3];
```

```java
x = new int[] {1, 2, 3, 4, 5};
```

```java
int[] w = {9, 10, 11, 12, 13};
```

但需要注意第3种方法不能对**已经声明的变量**使用

### 4

`System.arraycopy` 的用法，

>   Takes 5 parameters:
>
>   -   Source array
>   -   Start position in source
>   -   Target array
>   -   Start position in target
>   -   Number to copy

以 `System.arraycopy(b, 0, x, 3, 2)` 为例，

-   `b` 是要复制的数组
-   `0` 是 `b` 中开始复制的下标
-   `x` 是要粘贴复制内容的数组
-   `3` 是 `x` 中开始粘贴的下标
-   `2` 是复制的元素个数

如果 `b` 是 `{9, 10, 11}` ，`x` 是 `{-1, 2, 5, 4, 99}` ，

那么复制后 `x` 就变成 `{-1, 2, 5, 9, 10}` 

### 5

java中，二维数组的每个元素是一维数组的地址，所以同一个二维数组中可以存储不同长度的一维数组

![cs61b_12](images/cs61b_12.png){ loading=lazy }

## Lecture 7 ALists, Resizing, vs. SLists

### 1

课上说到 *顺序表 (基于数组的列表) array based list (AList)* 由于在存储数据个数达到数组长度时需要更换一个更大的数组，但如果每次扩展都只增加固定的长度，那么数据量大时程序就会运行比较慢，所以提到每次扩展可以扩展成之前长度的2倍

### 2

在把*顺序表*改造成 泛型顺序表 时，在构造数组时，

```java
public class AList<Item> {
    private Item[] items;
    private int size;
    
    public AList() {
        items = new Item[100];
        size = 0;
    }
}
```

`new Item[100]` IDEA报错(会引起generic array creation的错误)，而需要改成

```java
items = (Item[]) new Object[100];
```

### 3

由于在java中，**==对象只有失去最后一个==*==指向 reference==*==时，才会被回收空间==**，所以在泛型顺序表的删除方法中，需要把数组中(需要删去的)最后一个元素指向 `null`

## Lab 3

### 1

异常断点的使用，

在 运行 --- 查看断点 中打开，或者使用 ++ctrl+shift+f8++ 打开，

![cs61a_14](images/cs61a_14.png){ loading=lazy }

选中(任何异常)断点，还可以在『条件』中添加判断的条件

>   如
>
>   ```java
>   this instanceof java.lang.ArrayIndexOutOfBoundsException
>   ```

## Lecture 8 Inheritance, Implements

### 1

*接口 interface* 的使用方法，例如

先实现一个*接口*(使用 `interface` 关键字)，

```java
public interface List61B<Item> {
    public void addFirst(Item x);
    public void addLast(Item y);
    public Item getFirst();
    public Item getLast();
    public Item removeLast();
    public Item get(int i);
    public void insert(Item x, int position);
    public in size();
}
```

然后之前的SLList和AList类就可以添加上 `implements List61B<...>`

```java
public class AList<Item> implements List61B<Item> {
    ...
}
```

```java
public class SLList<BLorp> implements List61B<Blorp> {
    ...
}
```

而再将函数传入的参数改成 `List61B<String> list` (原来是 `SLList` 或 `AList` )，那么在调用这个函数时，传入SLList或者AList实例都可以

---

![cs61b_13](images/cs61b_13.png){ loading=lazy }

继承*接口*的子类**必须**实现接口的所有方法

### 2

-   ***Override 覆写*** 指的是**子类**在类中重新重新实现父类或者接口中的方法
-   ***Overload 重载*** 指的是同一个**函数**被重复多次实现(可以是在不同的子类中)

### 3

`@Override` 注释，作用是只有函数是覆写父类或接口的函数时，才会被编译

>   Why use `@Override` ?
>
>   -   Main reason: Protects against typos.
>       -   If you say `@Override` , but it the method isn't actually overriding anything, you'll get a compile error.
>       -   e.g. `public void addLats(Item x)`
>   -   Reminds programmer that method definition came from somewhere higher up in the inheritance hierarchy.

### 4

***Implementation Inheritance 实现继承***，使用 `default` 关键字，可以在接口中实现函数，并且子类能继承已经实现好的函数(就可以不用*覆写*)，例如

```java
default public void print() {
    for (int i = 0; i < size(); i += 1) {
        System.out.print(get(i) + " ");
    }
    System.out.println();
}
```

>   由于是在接口中实现，所以只能使用接口中的方法

### 5

![cs61b_14](images/cs61b_14.png){ loading=lazy }

如果声明的是父类的变量，但指向的是子类的实例，在使用这个(父类类型的)变量调用覆写的方法时，由于 *动态方法选择 Dynamic Method Selection*，最终运行时运行的会是实际子类实例的方法

---

![cs61b_15](images/cs61b_15.png){ loading=lazy }

如果在子类中只是*重载*而没有*覆写*的方法，那么如果变量声明时是父类的类型，在调用*重载*的方法时，就会调用父类的方法，而如果是子类的类型就会调用子类的方法(如上图中，从父类和子类的方法中传入的参数不一致可以看出是*重载*，所以 `a.praise(d)` 调用的是 `Animal` 类的方法)

>   教授的解释：
>
>   this praise method, it's overloaded, not overriden. Notice that this is not the same method signature in the dog class, it's not praise animal in the dog class, it's praise dog in the dog class. This is actually a totally new method, so it's not overriding, it's overloading. The other praise method in this dog class

---

Josh说道，另一种*动态方法选择*的理解是，把它当成是一个两步的处理过程，第一步在编译时发生，第二步在运行时发生

>   -   At compile time: We determine the **signature S** of the method to be called.
>       -   S is decided using **ONLY static types**.
>   -   At runtime: The dynamic type of the **invoking object** uses its method with this exact signature S.

如上图中的例子

```java
Animal a = new Dog();
Dog d = new Dog();
a.greet(d);  // greet(Animal a)
a.sniff(d);  // sniff(Animal a)
d.praise(d); // praise(Dog a)
a.praise(d); // praise(Animal a)
```

在编译时，会变量的数据类型以及调用方法时传入的参数确定调用的函数，如 `a.praise(d)` 中 `a` 是 `Animal` ，所以会寻找 `Animal` 类中的方法，根据传入的参数 `d` 是 `Animal` (的子类)，所以确定调用的方法为 `praise(Animal a)` ，

在运行时，再根据具体变量指向的实例调用对应的方法，如 `a.sniff(d)` 在编译时确定方法为 `sniff(Animal a)` ，而实例 `a` ( `Dog` 类)中有对应的方法，所以调用的就是 `Dog` 类的 `sniff` 方法

---

### 6

```java
import java.util.List;
import java.util.ArrayList;
```

可以导入java已经实现好的链表类

## Lecture 8 Q&A

### 1

有人提问关于java中*类型转换 Casting*的问题

```java
Bird bird = new Falcon();
Falcon falcon = (Falcon) bird;
```

这两行代码(设置的变量)对应的*静态类型*和*动态类型*是这样，

|          | Static Type | Dynamic Type |
| -------- | ----------- | ------------ |
| `bird`   | Bird        | Falcon       |
| `falcon` | Falcon      | Falcon       |

然后Josh对代码稍加修改，

```java
Bird bird = (Bird) new Falcon();
Falcon falcon = (Falcon) bird;
```

然后说道第一行加上 `(Bird)` 也不会改变对应的*静态类型*和*动态类型*，

>   in fact, a cast doesn't change anything, it never changes anything. When I think about a cast as I'll say in lecture 9 is, it tells the compiler don't do your normal type checking, I know what I'm doing. It doesn't actually change anything, it just says for the purposes of type checking pretend this is a bird.

### 2

有人向Josh提问一题，要求只修改原方阵(不创建新矩阵)使矩阵旋转90°，答案的做法大概是，因为**方阵中的每个位置旋转4次就会回到原来的位置**，所以把每个元素替换到旋转后的位置，再把新位置的旧元素换到旋转后的位置，循环4次就能换好4个元素，可以参考Josh画的图

![cs61b_16](images/cs61b_16.png){ loading=lazy }

## Project 1

### 1

>   [Java instanceof - javatpoint](https://www.javatpoint.com/downcasting-with-instanceof-operator)
>
>   The **java instanceof operator** is used to test whether the object is an instance of the specified type (class or subclass or interface).

课程网站上说会用到 `instanceof` 关键字，然后根据课程网站上提供的链接，`instanceof` 关键字的解释如上

### 2

由于 `ArrayDeque` 没有测试的文件，如果要测试的话需要自己写一个测试的文件，课程网站上建议可以参考Lab 3中的测试，

>   So how do you verify correctness of your data structure? You use your skills that you got from Lab 3! You are encouraged to copy and paste those tests for `SList` and `AList` and adapt them for these data structures. The tests will look very similar and only require basic changes.

于是我cv了 `TestBuggyAList.java` ，然后改成了

??? example "code"

    ```java title="RandomizedComparisonTest.java" hl_lines="9-10 17-18 20 22 25-31"
    package deque;
    
    import ...;
    
    public class RandomizedComparisonTest {
        // YOUR TESTS HERE
        @Test
        public void testThreeAddThreeRemove() {
            LinkedListDeque<Integer> l1 = new LinkedListDeque<>();
            ArrayDeque<Integer> l2 = new ArrayDeque<>();
    
            ...
        }
    
        @Test
        public void randomizedTest() {
            LinkedListDeque<Integer> L = new LinkedListDeque<>();
            ArrayDeque<Integer> L2 = new ArrayDeque<>();
    
            int N = 100000;
            for (int i = 0; i < N; i += 1) {
                int operationNumber = StdRandom.uniform(0, 4);
                if (operationNumber == 0) {
                    ...
                } else if (operationNumber == 3) {
                    // addFirst
                    int randVal = StdRandom.uniform(0, 100);
                    L.addFirst(randVal);
                    L2.addFirst(randVal);
                    System.out.println("addFirst(" + randVal + ")");
                }
            }
        }
    }
    ```

### 3

java中生成随机数可以使用 `Math.random()` ，会返回 `[0, 1)` 的随机数

## Lecture 9 Extends, Casting, Higher Order Functions

### 1

`extends` 关键字，能继承另一个类的所有不是 `private` 的属性(包括方法)，然后可以添加新的方法

继承了之后，可以使用 `super` 来访问父类的非 `private` 的属性

---

子类的构造函数中，如果没有***显式*地**调用父类的构造函数(通过 `super([...]);` 调用)，那么会自动***隐式***地调用(调用 `super();` )

![cs61b_17](images/cs61b_17.png){ loading=lazy }

### 2

Java中的*高阶函数 Higher Order Functions*

Josh在课上展示了一个例子(使用*interface*)

=== "Java"

    ```java title="IntUnaryFunction"
    public interface IntUnaryFunction {
        int apply(int x);
    }
    ```
    
    ```java title="TenX"
    public class TenX implements IntUnaryFunction {
        public int apply(int x) {
            return 10 * x;
        }
    }
    ```
    
    ```java title="HoFDemo"
    public class HoFDemo {
        public static int do_twice(IntUnaryFunction f, int x) {
            return f.apply(f.apply(x));
        }
        public static void main(String[] args) {
            System.out.println(do_twice(new TenX(), 2));
        }
    }
    ```

=== "Python"

    ```python
    def tenX(x):
        return 10 * x
    
    def do_twice(f, x):
        return f(f(x))
    
    print(do_twice(tenX, 2))
    ```

## Lecture 10 Subtype Polymorphism vs. HoFs

### 1

Josh提到 `OurComparable` 的缺点

>   ```java
>   public interface OurComparable {
>       public int compareTo(Object o);
>   }
>   ```

即在运行时(如果类型不一致)会出现错误

>   ```java
>   public class Dog implements OurComparable {
>       public int compareTo(Object obj) {
>           /** Warning, cast can cause runtime error! */
>           Dog uddaDog = (Dog) obj;
>           return this.size - uddaDog.size;
>       }
>   }
>   ```

所以(为了避免这种情况)要换成使用 `Comparable<T>` (java内置的接口)

>   ```java
>   public interface Comparable<T> {
>       public int compareTo(T obj);
>   }
>   ```
>
>   ```java
>   public class Dog implements Comparable<Dog> {
>       public int compareTo(Dog uddaDog) {
>           return this.size - uddaDog.size;
>       }
>   }
>   ```

### 2

Josh提到，类似于python中传入 比较函数 进行不同的比较

```python title="python"
def print_larget(x, y, compare, stringify):
    if compare(x, y):
        return stringify(x)
    return stringify(y)
```

java中通常使用 `Comparator` ，他展示的示例如下

```java title="java"
import java.util.Comparator;

public class Dog {
    private String name;
    ...
    private static class NameComparator implements Comparator<Dog> {
        public int compare(Dog a, Dog b) {
            return a.name.compareTo(b.name);
        }
    }
    
    public static class Comparator<Dog> getNameComparator() {
        return new NameComparator();
    }
}
```

```java
Comparator<Dog> cd = Dog.getNameComparator();
if (cd.compare(d1, d3) > 0) {
    d1.bark();
} else {
    d3.bark();
}
```

## Lecture 10 Q&A

### 1

Josh根据下面这个Lecture 10课上提到的例子，对*类型转换 Casting*进行了进一步的解释

```java
Object o2 = new ShowDog("Mortimer", "Corgi", 25, 512.2);

ShowDog sdx = ((ShowDog) o2);
sdx.bark();

Dog dx = ((Dog) o2);
dx.bark();

((Dog) o2).bark();

Object o3 = (Dog) o2;
o3.bark();  // Compile error
```

类型转换**不会**改变原本变量的*静态类型*和*动态类型(即实际的类型)*，但是例如这一行代码中

```java
ShowDog sdx = ((ShowDog) o2);
```

`((ShowDog) o2)` 由于有*类型转换 Casting*，所以**这个表达式**(整体)会被认为静态类型是 `ShowDog` ，因而能赋值给静态类型同为 `ShowDog` 的 `sdx` ，而如果不加*类型转换*，

```java
ShowDog sdx = o2;
```

即使 `o2` 的*动态类型*(实际的类型)是 `ShowDog` ，但是因为 **`o2` *静态类型*是 `Object`** ， **`Object` 不能赋值给 `ShowDog`** (只有 `ShowDog` 类和 `ShowDog` 的子类才能赋值给 `ShowDog` )，所以会产生**编译错误**

## Lab 4

### 1

可以通过 `git checkout` 来变更文件到某个commit的状态

```bash
git checkout ... path/to/file
```

`...` 处可以是commit的编号(例如 `47bb0877` )，或者branch(例如 `main` )或者tag(例如 `origin/main` )
