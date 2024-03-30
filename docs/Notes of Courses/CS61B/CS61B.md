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