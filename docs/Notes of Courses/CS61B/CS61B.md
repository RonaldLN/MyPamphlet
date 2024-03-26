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