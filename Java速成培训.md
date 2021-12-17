**Java速成培训**

[TOC]

# JDK下载和环境配置

## Java下载

JDK(Java Development Kit)：Java开发工具包

官网下载地址：https://www.oracle.com/java/technologies/javase-downloads.html

下载Java SE 11(LTS)：Java标准版本11(Long Term Support 长期支持)

![image-20210219101326453](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210219101326453.png)

点击**JDK Download**后，往下拉选择**jdk-11.0.10_windows-x64_bin.zip**压缩包（免安装版本）

![image-20210219101527466](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210219101527466.png)

将下载的文件放到D:\Java目录下，并解压到当前文件夹。

## 配置Java环境变量

1.在桌面上，右击【此电脑】->【属性】

![](C:\Users\Admin\Pictures\此电脑-属性.png)



2.点击【高级系统设置】

![image-20210219110526608](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210219110526608.png)



3.点击【环境变量】

![image-20210219110623227](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210219110623227.png)



4.点击【系统变量->新建】

![image-20210219110723044](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210219110723044.png)

5.然后输入固定的变量名JAVA_HOME，变量值选择jdk的目录，然后点击【确定】

![image-20210219110910845](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210219110910845.png)



6.在系统变量中，往下翻选中【Path】后，点【编辑】

![image-20210219111447988](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210219111447988.png)



7.点击【编辑】，输入%JAVA_HOME%\bin并【确定】，将所有的【确定】点击，即完成了Java配置。

![image-20210219111549292](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210219111549292.png)



8.验证Java配置，输入cmd回车

![image-20210219112011011](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210219112011011.png)

输入java -version后看到如下截图信息，即表示Java配置成功。

![image-20210219112113763](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210219112113763.png)



# 一、数据类型

![](F:\chengshuliang\个人输出文档\Java数据类型.png)



整型中的默认类型是int类型，如果想使用long类型，需要在数值后面加大写L

浮点型的默认类型是double，如果想使用float类型，需要在数值后面加大写F

```java
long a = 100L;
float b = 3.14F;
```



| 类型    | 字节 | 取值范围（二进制） | 取值范围（十进制）           |
| ------- | ---- | ------------------ | ---------------------------- |
| byte    | 1    | -2^7~2^7-1         | -128~127                     |
| short   | 2    | -2^15~2^15-1       | -32768~32767                 |
| int     | 4    | -2^31~2^31-1       | -2147483648<br />~2147483647 |
| long    | 8    | -2^63~2^63-1       |                              |
| float   | 4    |                    |                              |
| double  | 8    |                    |                              |
| boolean | 1    | true/false         | 默认值false                  |
| char    | 2    | 无符号，0~65535    | Unicode字符集（万国码）      |

转义字符\反斜杠：

| 符号       | 含义                   |
| ---------- | ---------------------- |
| \n         | 换行                   |
| \r         | 回车                   |
| \s         | 空格                   |
| \t         | 制表符                 |
| \\，\'，\" | 反斜杠，单引号，双引号 |

```java
public static void main(String[] args) {
    // 打印单引号
    System.out.println("\'");
    // 打印双引号
    System.out.println("\"");
    // 打印单斜杠
    System.out.println("\\");
    // 打印双斜杠
    System.out.println("\\\\");
}
```



以上8种基本数据类型对应的包装类型分别为：

Byte、Short、Integer、Long、Float、Double、Boolean、Character

一般原则：Java类的成员变量定义使用包装类型；在方法中的局部变量可以使用基本类型。



# 二、变量

Java是强类型语言，所有的变量必须要有类型。

变量的作用域：某个变量有效的范围称之为它的作用域范围，在这个作用域内，该变量可以随时使用以及重复赋值，但是不能再次声明，超过这个范围，变量会被垃圾回收器进行回收掉。

如何判断一个变量的作用域范围？

离变量声明的代码最近的左大括号所对应的范围就是它的作用域范围。

说明：for或者foreach循环情况变量作用域范围是大括号循环体。

```java 
for (int i = 0; i < 10; i++) {
    // 这是变量i的作用域范围
}

List<String> list = new ArrayList<String>();
for (String name : list) {
    // 这是变量name的作用域范围
}
```

变量的分类（根据作用域的范围）：

- 全局变量：定义在方法外部，类内部的变量，该变量的作用域是整个类（也叫成员变量）；
- 局部变量：定义在方法内部的变量，该变量的作用域是它所在的方法；
  说明：局部变量是可以跟全局变量同名的。
- 常量：定义在方法外部，并且由public static final修饰的变量它是一个固定不变的量（比如数学里的∏=3.14159265），它的作用域是整个项目都可以访问（注意：常量的名称我们使用全大写字母，若有多个单词，用下划线隔开）；
- 直接量（字面量）：直接写某个具体值；

代码中魔法值，即直接写的数字或字符串。调整到常量类或者枚举类中，便于维护管理。

# 三、标识符

什么是标识符：指在程序中，我们自定义的各种名字。比如类的名字、方法的名字和变量的名字等等，都是标识符。

标识符的命名规则（强制要求）

- 由大小写英文字母、数字、下划线和$组成；
- 不能以数字开头；
- 不能是关键字；

标识符的命名规范（建议要求）

- 类名规范：首字母大写，后面每个单词首字母大写（大驼峰式）；
- 方法名规范：首字母小写，后面每个单词首字母大写（小驼峰式）；

# 四、运算符

## 1.算术运算符

- 两个数的运算：

| 运算符 | 描述     |
| ------ | -------- |
| +      | 加、求和 |
| -      | 减、求差 |
| *      | 乘、求积 |
| /      | 除、求商 |
| %      | 模、求余 |

- 一个数的运算：

| 运算符 | 描述           |
| ------ | -------------- |
| ++     | 递增，变量值+1 |
| --     | 递减，变量值-1 |

Java中的不同数据类型之间进行算术运算的时候，结果会自动转成大的数据类型，整型中的默认类型是int。

```java
byte a = 10;
short b = 20;
int result = a + b;
```

整型的所有运算结果也是整型。

```java
// 结果c=2
int c = 10 / 4;
```

字符串和任意类型相加，结果等于字符串。

```java
// 打印结果：5+5=55
System.out.println("5+5=" + 5 + 5);
```

++和--若放在变量的前面，代表的是先加减再使用，若放在变量的后面，代表的是先使用再加减。

```java
int i = 0;
int j = 0;
int m = 0;
int n = 0;

int a = i++;
int b = j--;
int c = ++m;
int d = --n;
// a = 0; i = 1;
// b = 0; j = -1;
// c = 1; m = 1;
// d = -1; n = -1;
```

## 2.赋值运算符

把等号右边的值赋予给等号左边的变量

=、+=

```java
short a = 0;
// 会自动转型。
a += 5;
System.out.println(a);
short b = 0;
// 不会自动转型，需要强转。
b = (short)(b + 5);
System.out.println(b);
```

## 3.比较运算符

比较运算符，是两个数据之间进行比较的运算，运算结果都是布尔值true或者false

大于：>

小于：<

大于等于：>=

小于等于：<=

等于：==

不等于：!=

- 放在if或者while判断条件中
- ==一般用来判断基本数据类型的值是否相同
- 若使用==来判断对象是否相同的话，那么它判断的是对象的地址值是否相同
- 如何判断对象的内容是否相等：equals()

```java
    public static void main(String[] args) {
        String s1 = "Runoob";
        String s2 = "Runoob";
        String s3 = s1;
        String s4 = new String("Runoob");
        String s5 = new String("Runoob");

        System.out.println(s1 == s2);
        System.out.println(s2 == s3);
        System.out.println(s3 == s4);
        System.out.println(s4 == s5);
    }
```

![img](https://www.runoob.com/wp-content/uploads/2013/12/java-string-1-2020-12-01.png)



当Integer和Integer进行比较时，必须使用equals()方法。

```java
public static void main(String[] args) {
    Map<String, Integer> map = new HashMap<>();
    map.put("A", 66);
    map.put("B", Integer.valueOf(66));
    map.put("C", new Integer(66));
    map.put("D", 200);
    map.put("E", 200);

    System.out.println(map.get("A") == map.get("B"));
    System.out.println(map.get("B") == map.get("C"));
    System.out.println(map.get("D") == map.get("E"));
}
```



## 4.逻辑、三目运算符

逻辑运算符：用来连接两个布尔类型结果的运算符，运算结果还是布尔值true或者false

| 运算符 | 语义       | 描述                 |
| ------ | ---------- | -------------------- |
| &&     | 与（并且） | 一假必假，全真为真。 |
| \|\|   | 或（或者） | 一真必真，全假为假。 |
| !      | 非（取反） | 真即是假，假即是真。 |

逻辑运算符具有短路功能，若只使用一个&或者|结果一样，只是不再具有短路功能。

短路功能解释：若已经能判断出结果，则后续布尔表达式不会被执行。

布尔表达式1 && 布尔表达式2，若布尔表达式1为假，则直接返回结果假，不会执行布尔表达式2.

布尔表达式3 || 布尔表达式4，若布尔表达式3为真，则直接返回结果真，不会执行布尔表达式4.



三目运算符（三元运算符）：简化if...else的操作，先判断后处理，直接在一句话中完成。

| 运算符 | 语义                       | 描述                                                         |
| ------ | -------------------------- | ------------------------------------------------------------ |
| ? :    | 布尔表达式 ? 结果1 : 结果2 | 当表达式结果为真，返回结果1；<br />当表达式结果为假，返回结果2； |

**注意三目运算符的空指针问题：**根据规定，三目运算符的第二、第三位操作数的返回值类型应该是一样的，这样才能把一个三目运算符的结果赋值给一个变量。那如果，三目运算符的第二位和第三位的操作数的类型分别是基本数据类型和包装类型时，就需要有一方进行自动拆装箱。

```java
public class Test {
    public static void main(String[] args) {
        Integer a = 1;
		Integer b = 2;
		Integer c = null;
		Boolean flag = false;
		Integer result = (flag ? a*b : c);
		System.out.println(result);
    }
}

// 反编译之后的代码
import java.io.PrintStream;

public class Test {
	public Test() {}

	public static void main(String args[]) {
		Integer integer = Integer.valueOf(1);
		Integer integer1 = Integer.valueOf(2);
		Integer integer2 = null;
		Boolean boolean1 = Boolean.valueOf(false);
		Integer integer3 = Integer.valueOf(
            boolean1.booleanValue() ? integer.intValue() * integer1.intValue() : integer2.intValue());
		System.out.println(integer3);
	}
}

public class Test {
    public static void main(String[] args) {
        Integer a = 1;
		Integer b = 2;
		Integer c = null;
		Boolean flag = false;
		// Integer result = (flag ? a * b : c);
        // 使用if...else改写三目运算符不会报空指针异常。
        Integer result = null;
        if (flag) {
            result = a * b;
        } else {
            result = c;
        }
		System.out.println(result);
    }
}
```



# 五、条件判断语句

```java
// 1.单个if语句
if (布尔表达式) {
    // 布尔表达式为true将执行的语句
}

// 2.if...else语句
if (布尔表达式) {
    // 布尔表达式为true将执行的语句 
} else {
    // 布尔表达式为false将执行的语句   
}

// 3.if...else if...else语句
if (布尔表达式1) {
    // 布尔表达式1为true将执行的语句 
} else if (布尔表达式2) {
    // 布尔表达式2为true将执行的语句
} else {
    // 以上布尔表达式都不为true将执行的语句   
}

// 嵌套，一般不建议嵌套过多，导致代码可读性较差。
```



# 六、循环控制语句

```java
// 普通for循环（循环次数确定的情况下）
for (int i = 0; i < 10; i++) {
    System.out.println(i);
}

// 增强for循环（foreach循环）
List<String> nameList = new ArrayList<String>();
for (String name : nameList) {
    System.out.println(name);
}

// while循环，只要布尔表达式为 true，循环就会一直执行下去。
while (布尔表达式) {
    // 循环内容
}

// do...while循环
do {
    // 循环内容
} while (布尔表达式);
/*
 *布尔表达式在循环体的后面，所以语句块在检测布尔表达式之前已经执行了。 
 *如果布尔表达式的值为 true，则语句块一直执行，直到布尔表达式的值为false。
 */
```

break关键字，跳出当前循环，并且继续执行该循环之后的语句。

```java
break;
```

continue关键字，立即跳转到下一次循环检查中。

```java
continue;
```

return关键字，退出当前循环所在的方法。

```java
return;
```

思考：若我们想做到当某个内层循环条件满足时，跳出整个循环，该如何进行操作？

a.锚点法：在循环的开始给该循环起一个名字，然后在适当的时候，通过continue或者break跳到指定的位置上去。（不建议使用!）

b.标记法：直接在外层循环之外定义一个boolean变量，当内层循环满足了某个条件的时候，我们修改该变量的值，然后使用break跳出内层循环，然后我们在外层循环中不断监控这个boolean变量，当该变量发生了变化就意味着内层循环已经满足了条件，那么此时在外层循环里break;跳出循环。



# 七、数组

## 1.一维数组

声明数组变量

```java
int[] numArray;
```

创建数组

```java
numArray = new int[3];
```

声明并创建数组

```java
int[] numArray = new int[3];

int[] numArray2 = {1, 2, 3};
```

数组的元素是通过索引访问的。数组索引从 0 开始，所以索引值从 0 到 arrayRefVar.length-1。

```java
numArray[0] = 1;
```

## 2.二维数组

```java
// 静态初始化
int[][] table = new int[][]{{1, 2, 3},{4, 5, 6},{7, 8, 9}};
int[][] table2 = {{1, 2, 3},{4, 5, 6},{7, 8, 9}};

// 动态初始化
int[][] arr = {};
int[][] arr1 = new int[][]{};
int[][] arr2 = new int[2][];
// 2行3列的二维数组
int[][] arr3 = new int[2][3];
```



# 八、Java封装

​    封装最主要的功能在于我们能修改自己的实现代码，而不用修改那些调用我们代码的程序片段。

适当的封装可以让代码更容易理解与维护，也加强了代码的安全性。

封装的优点

- 良好的封装能够减少耦合。
- 类内部的结构可以自由修改。
- 可以对成员变量进行更精确的控制。
- 隐藏信息，实现细节。

## 1.访问控制修饰符

Java中，可以使用访问控制符来保护对类、变量、方法和构造方法的访问。Java 支持 4 种不同的访问权限。

- **public** : 对所有类可见。使用对象：类、接口、变量、方法
- **protected** : 对同一包内的类和所有子类可见。使用对象：变量、方法。 **注意：不能修饰类（外部类）**。
- **default** (即默认，什么也不写）: 在同一包内可见，不使用任何修饰符。使用对象：类、接口、变量、方法。
- **private** : 在同一类内可见。使用对象：变量、方法。 **注意：不能修饰类（外部类）**

| 修饰符      | 当前类 | 同一包内 | 子孙类(同一包) | 子孙类(不同包)                                               | 其他包 |
| :---------- | :----- | :------- | :------------- | :----------------------------------------------------------- | :----- |
| `public`    | Y      | Y        | Y              | Y                                                            | Y      |
| `protected` | Y      | Y        | Y              | Y/N（[说明](https://www.runoob.com/java/java-modifier-types.html#protected-desc)） | N      |
| `default`   | Y      | Y        | Y              | N                                                            | N      |
| `private`   | Y      | N        | N              | N                                                            | N      |

**思考：JavaBean的属性为何用private而不是public？**

问题：为什么javaBean不直接使用public，而是用private再提供get-set方法来获取和修改属性呢？

看起来private-get-set增加了代码量，也就是为了能够获取和修改，直接用public不是也可以直接获取和修改么。 

然后就在网上查了下各家的说法，总结了一下，也是为了说服自己去理解和记住。

1、java的封装性规定 (属于规定,但是现在一直这样使用，肯定是有道理的)

2、安全性，使用private的话，就可以单独控制某一个属性是否供获取或是修改，而使用public的，便可以随意修改

3、扩展性。单独使用public的话，只是简单的对属性进行获取和修改。使用private的话，可以在get和set方法中，对属性的值再次进行操作。

可以控制属性为只读或只改。

4、如果属性类型改变后，只需要修改get、set方法去兼容之前的即可。

```java
public class User {
    private String code;
    
    public String getCode() {
        return this.code;
    }
    
    public void setCode(String code) {
        this.code = code
    }
}

public class Test {
    public static void main(String[] args) {
        User user = new User();
        user.setCode("100001");
        System.out.println(user.getCode());
    }
}

/**
 * code属性的类型需要修改成Integer，
 * 通过修改getter、setter方法兼容之前的类型。
 */
public class User {
    private Integer code;
    
    public String getCode() {
        return this.code != null ? this.code.toString() : null;
    }
    
    public void setCode(String code) {
        if (StringUtils.isNotBlank(code)) {
            this.code = Integer.valueOf(code);
        }
    }
}
```



# 九、Java继承

​    代码存在重复了，后果就是代码量大且臃肿，而且维护性不高(维护性主要是后期需要修改的时候，就需要修改很多的代码，容易出错)，所以要从根本上解决这两段代码的问题，就需要继承，将两段代码中相同的部分提取出来组成一个父类。

​    需要注意的是Java不支持多继承，但支持多重继承。

![java-extends-2020-12-08](C:\Users\Admin\Pictures\java-extends-2020-12-08.png)

继承关键字

继承可以使用 extends 和 implements 这两个关键字来实现继承，而且所有的类都是继承于 java.lang.Object，当一个类没有继承的两个关键字，则默认继承object（这个类在 **java.lang** 包中，所以不需要 **import**）祖先类。

在 Java 中，类的继承是单一继承，也就是说，一个子类只能拥有一个父类，所以 extends 只能继承一个类。

使用 implements 关键字可以变相的使java具有多继承的特性，使用范围为类继承接口的情况，可以同时继承多个接口（接口跟接口之间采用逗号分隔）。

接口的继承：

```java
public interface A {
}

public interface B {
}

public interface C extends A, B {
}
```



# 十、Java多态

多态就是同一个接口，使用不同的实例而执行不同的操作，如图所示：

![java-polymorphism-111](C:\Users\Admin\Pictures\java-polymorphism-111.png)

```java
public interface Printer {
    void print();
}

public class ColorPrinter implements Printer {
    @Override
    public void print() {
        System.out.println("使用彩色打印机");
    }
}

public class BlackWhitePrinter implements Printer {
    @Override
    public void print() {
        System.out.println("使用黑白打印机");
    }
}

public class Test {
    public static void show(Printer printer) {
        printer.print();
    }
    
    public static void main(String[] args) {
        show(new ColorPrinter());
        show(new BlackWhitePrinter());
    }
}
```



**多态的优点**

- 消除类型之间的耦合关系
- 可替换性
- 可扩充性
- 接口性
- 灵活性
- 简化性



Java 重写(Override)与重载(Overload)

重写是子类对父类的允许访问的方法的实现过程进行重新编写, 返回值和形参都不能改变。**即外壳不变，核心重写！**

实现类对接口中的方法也是重写。



重载(overloading) 是在一个类里面，方法名字相同，而参数不同。返回类型可以相同也可以不同。

每个重载的方法（或者构造函数）都必须有一个独一无二的参数类型列表。

最常用的地方就是构造器的重载。

**总结**

方法的重写(Overriding)和重载(Overloading)是Java多态性的不同表现，重写是父类与子类之间多态性的一种表现，重载可以理解成多态的具体表现形式。

- 方法重载是一个类中定义了多个方法名相同,而他们的参数的数量不同或数量相同而类型和次序不同,则称为方法的重载(Overloading)。
- 方法重写是在子类存在方法与父类的方法的名字相同,而且参数的个数与类型一样,返回值也一样的方法,就称为重写(Overriding)。
- 方法重载是一个类的多态性表现,而方法重写是子类与父类的一种多态性表现。



# 十一、Java枚举（enum）

Java 枚举是一个特殊的类，一般表示一组常量，比如一年的 4 个季节，一个年的 12 个月份，一个星期的 7 天，方向有东南西北等。

Java 枚举类使用 enum 关键字来定义，各个常量使用逗号 **,** 来分割。

枚举跟普通类一样可以用自己的变量、方法和构造函数，构造函数只能使用 private 访问修饰符，所以外部无法调用。

枚举既可以包含具体方法，也可以包含抽象方法。 如果枚举类具有抽象方法，则枚举类的每个实例都必须实现它。

```java
/**
 * 季节枚举
 * @description: 季节枚举类
 * @author: csl
 * @date: 2021/2/18
 */
public enum Season {

    /**
     * 春季
     */
    SPRING("春季", "3~5月"),

    /**
     * 夏季
     */
    SUMMER("夏季", "6~8月"),

    /**
     * 秋季
     */
    AUTUMN("秋季", "9~11月"),

    /**
     * 冬季
     */
    WINTER("冬季", "12~2月");

    /**
     * 名称
     */
    private String name;

    /**
     * 范围
     */
    private String range;

    Season(String name, String range) {
        this.name = name;
        this.range = range;
    }

    public String getName() {
        return name;
    }

    public String getRange() {
        return range;
    }

}
```

枚举类使用

```java
public static void main(String[] args) {
    System.out.println(Season.SPRING.getName());
    System.out.println(Season.SPRING.getRange());
}
```





# 十二、Java 抽象类

抽象类除了不能实例化对象之外，类的其它功能依然存在，成员变量、成员方法和构造方法的访问方式和普通类一样。

由于抽象类不能实例化对象，所以抽象类必须被继承，才能被使用。也是因为这个原因，通常在设计阶段决定要不要设计抽象类。

在Java中抽象类表示的是一种继承关系，一个类只能继承一个抽象类，而一个类却可以实现多个接口。

**抽象类总结规定**

- 抽象类不能被实例化(初学者很容易犯的错)，如果被实例化，就会报错，编译无法通过。只有抽象类的非抽象子类可以创建对象。
- 抽象类中不一定包含抽象方法，但是有抽象方法的类必定是抽象类。
- 抽象类中的抽象方法只是声明，不包含方法体，就是没有方法的具体实现代码。
- 构造方法，类方法（用 static 修饰的方法）不能声明为抽象方法。
- 抽象类的子类必须给出抽象类中的抽象方法的具体实现，除非该子类也是抽象类。



# 十三、Java接口

## 1.接口与类的区别：

- 接口不能用于实例化对象。
- 接口没有构造方法。
- 接口中所有的方法必须是抽象方法。
- 接口不能包含成员变量，除了 static 和 final 变量。
- 接口不是被类继承了，而是要被类实现。
- 接口支持多继承。

## 2.接口特性

- 接口中每一个方法也是隐式抽象的,接口中的方法会被隐式的指定为 **public abstract**（只能是 public abstract，其他修饰符都会报错）。
- 接口中可以含有变量，但是接口中的变量会被隐式的指定为 **public static final** 变量（并且只能是 public，用 private 修饰会报编译错误）。
- 接口中的方法是不能在接口中实现的，只能由实现接口的类来实现接口中的方法。

## 3.抽象类和接口的区别

-  抽象类中的方法可以有方法体，就是能实现方法的具体功能，但是接口中的方法不行。
- 抽象类中的成员变量可以是各种类型的，而接口中的成员变量只能是 **public static final** 类型的。
- 接口中不能含有静态代码块以及静态方法(用 static 修饰的方法)，而抽象类是可以有静态代码块和静态方法。
- 一个类只能继承一个抽象类，而一个类却可以实现多个接口。

```java
public interface UserService {
    /**
     * 根据用户ID获取用户信息
     */
    User getById(Long userId);

    /**
     * 将用户信息打印出来
     */
    void printUser(User user);
}
```

## 4.在Java8中，接口中能定义如下变量和方法

- 常量

```java
String MYSQL = "mysql";
```

- 抽象方法

```java
/**
 * 根据用户ID获取用户信息
 */
User getById(Long userId);
```

- 默认方法

```java
default void defaultMethod() {
    System.out.println("接口中定义默认方法！");
}
```

- 静态方法

```java
static void staticMethod() {
    System.out.println("接口中定义静态方法！");
}
```

在Java9中，还支持私有方法

- 私有方法

```java
private void test() {
    System.out.println("接口中定义私有方法！");
}
```

- 私有静态方法

```java
private static void print() {
    System.out.println("接口中定义私有静态方法！");
}
```



# 十四、Java集合

1.Collection接口

​    最基本的集合接口，存储一组不唯一，无序的对象。

​    唯一：object1.equals(object2)为true表示这两个对象相同。

​    有序：对象被添加进去，和被获取时的顺序相同。

2.Collection接口常用的子接口：

List接口：存储一组不唯一，有序的对象。（可以包含null对象）

特点：查找元素效率高，插入和删除效率低。

```java
List<String> list = new ArrayList<>();
list.add("1");
list.add("2");
list.add("3");
list.add(null);
list.add("1");

for (String str : list) {
    System.out.println(str);
}
```



Set接口：存储一组唯一，无序的对象。

特点：查找元素效率低，插入和删除效率高。

```java
Set<String> set = new HashSet<>();
set.add("1");
set.add("2");
set.add("3");
set.add(null);
set.add("1");

for (String str : set) {
    System.out.println(str);
}
```



SortedSet：继承于Set保存有序的集合，其实现类是TreeSet（不能存null对象）

3.List接口常用的实现类：

ArrayList：实现了可变大小的数组，随机访问和遍历元素时，提供更好的性能。

LinkedList：主要用于创建链表数据结构，查找效率低。

Vector：该类和ArrayList非常相似，但是该类是同步的，可以用在多线程的情况，该类允许设置默认的增长长度，默认扩容方式为原来的2倍。

Stack：栈是Vector的一个子类，它实现了一个标准的后进先出的栈。

4.Set接口常用的实现类：

HashSet：不允许出现重复元素，不保证集合中元素的顺序，允许包含值为null的元素，但最多只能一个。

放在HashSet中的对象需要重写equals方法。

TreeSet：不重复且有序的。（不能存null对象）



5.Map接口常用的实现类：

存储一组键值对象。

HashMap：根据键的HashCode值存储数据，具有很快的访问速度，最多允许一条记录的键为null，不支持线程同步。

ConcurrentHashMap：线程安全的。



# 十五、Java泛型
泛型的本质是为了参数化类型。

也就是说在泛型使用过程中，操作的数据类型被指定为一个参数，这种参数类型可以用在类、接口和方法中，分别被称为泛型类、泛型接口、泛型方法。

特性：只在编译阶段有效。在编译过程中，正确检验泛型结果后，会将泛型的相关信息擦出，泛型信息不会进入到运行时阶段。

```java
// 只有String类型才能被添加到list中
List<String> list = new ArrayList<String>();
```

**注意**：泛型的类型参数只能是类类型，不能是基本类型。

## 1.泛型类

常用的ArrayList<E>、HashMap<E>

常用T，E，K，V，R，U等单个大写字母表示泛型。

```java
/**
 * 定义同一的API接口返回实体类
 */
public class ResponseData<T> {
    /**
     * 响应代码
     */
    private Integer code;
    /**
     * 响应信息
     */
    private String message;
    /**
     * 返回数据
     */
    private T data;
}
```

## 2.泛型接口

泛型接口与泛型类的定义及使用基本相同。

一般用于重构代码中，比如Mybatis的Mapper接口都自带11个CRUD方法。

```java
public interface BaseMapper<R, K, E> {
    R selectByPrimaryKey(K id);
}

public interface UserMapper extends BaseMapper<User, Long, UserExample> {
}
```



```java
/**
 * 定义一个泛型接口
 */
public interface Generator<T> {
    T next();
}
```

当实现泛型接口的类，没有传入泛型实参时：

```java
public class FruitGenerator<T> implements Generator<T> {
    @Override
    public T next() {
        return null;
    }
}
```

当实现泛型接口的类，传入泛型实参时：

```java
public class FruitGenerator implements Generator<String> {
    private String[] fruits = new String[]{"苹果", "桔子", "凤梨"};
    
    @Override
    public String next() {
        int index = new Random().nextInt(3);
        return fruits[index];
    }
}
```

## 3.泛型通配符

```java
/**
 * 在实例化泛型类时，必须指定T的具体类型。
 */
public class Generic<T> {
    private T key;
    
    public Generic(T key) {
        this.key = key;
    }
    
    public T getKey() {
        return key;
    }
}
```

实例化泛型类

```java
public class Test {
    
    public static void printKey(Generic<Number> gen) {
        System.out.println(gen.getKey());
    }
    
    /**
     * 使用通配符?代替具体的类型实参
     */
    public static void showKey(Generic<?> gen) {
        System.out.println(gen.getKey());
    }
    
    public static void main(String[] args) {
        Generic<Integer> intNum = new Generic<Integer>(123);
        System.out.println(intNum.getKey());
        Generic<String> str = new Generic<String>("666");
        System.out.println(str.getKey());
        
        Generic<Number> genNum = new Generic<Number>(456);
        printKey(genNum);
        // 传入Generic<Integer>编译会报错
        // printKey(intNum);

        showKey(intNum);
        showKey(genNum);
    }
    
}
```

此处的？和Number、String、Integer一样都是一种实际的类型，可以把？看成所有类型的父类。是一种真实的类型。

可以解决当具体类型不确定的时候，这个通配符就是 ?

## 4.泛型方法

泛型类，是在实例化类的时候指明泛型的具体类型；泛型方法，是在调用方法的时候指明泛型的具体类型 。

public修饰符与返回值之间有泛型<T>，可以理解为声明此方法为泛型方法。

```java
public <T> T printKey(Generic<T> gen) {
    return gen.getKey();
}
```

静态方法需要注意：静态方法无法访问类上定义的泛型；

那么，静态方法要使用泛型的话，必须将静态方法也定义成泛型方法 。



## 5.泛型上下边界

在使用泛型的时候，我们还可以为传入的泛型类型实参进行上下边界的限制，如：类型实参只准传入某种类型的父类或某种类型的子类。

为泛型添加上边界，即传入的类型实参必须是指定类型的子类型。

<? extends 父类>

为泛型添加下边界，即传入的类型实参必须是指定类型的父类型。

<? super 子类>

```java
/**
 * 应用在泛型类上
 */
public class Generic<T extends Number> {
}

/**
 * 应用在普通方法的参数上
 */
public void showKey(Generic<? extends Number> obj) {
    System.out.println(obj.getKey());
}

/**
 * 应用在泛型方法上的正确写法
 */
public <T extends Number> T showKey(Generic<T> obj) {
    return obj.getKey();
}
```



# 十六、Java8新特性-Stream

- 数据源：流的来源。可以是集合，数组等。
- 聚合操作：类似SQL语句一样的操作效果，比如过滤、排序、分组、统计、查找、转换等。
- stream()：为集合创建串行流。
- parallelStream()：为集合创建并行流。

```java
List<String> strings = Arrays.asList("abc", "", "bc", "efg", "abcd","", "jkl");
// 获取空字符串的数量
long count = strings.parallelStream().filter(string -> string.isEmpty()).count();
```

**forEach**

Stream提供了新的方法forEach来迭代流中的每个数据。

```java
public static void main(String[] args) {
    List<Integer> nums = Arrays.asList(1, 2, 3, 4, 5, 6);
    // 遍历集合
    nums.stream().forEach(System.out::println);
    // 过滤处大于3的数字
    List<Integer> resultList = nums.stream().filter(n -> n > 3).collect(Collectors.toList());
    System.out.println("过滤之后的结果：");
    resultList.stream().forEach(System.out::println);
}
```

**map**

map方法用于映射每个元素到对应的结果。（理解为转换）

```java
List<Integer> numbers = Arrays.asList(3, 2, 7, 3, 5);
// 获取对应的平方数，并去重。
List<Integer> squaresList = numbers.stream().map(i -> i*i).distinct().collect(Collectors.toList());
```

**limit**

limit方法用于获取指定数量的流。

```java
List<Integer> nums = Arrays.asList(7, 8, 1, 2, 3, 4, 5, 6);
// 显示前3个元素
nums.stream().limit(3).forEach(System.out::println);
```

**sorted**

sorted方法用于对流进行排序。默认升序

```java
List<Integer> nums = Arrays.asList(7, 8, 1, 2, 3, 4, 5, 6);
// 排序后输出
nums.stream().sorted().forEach(System.out::println);
```

**Collectors**

属于工具类，功能：将流转换成集合、分组、过滤、统计等等。

C#linq与Java8 Stream比较

| C# linq             | Java Stream                 | 说明 |
| ------------------- | --------------------------- | ---- |
| Foreach             | forEach                     |      |
| Select              | map                         |      |
| Where               | filter                      |      |
| Take                | limit                       |      |
| OrderBy/OrderByDesc | sorted                      |      |
| All/Any             | allMatch/anyMatch/noneMatch |      |
| Distinct            | distinct                    |      |
| SelectMany          | flatMap                     |      |
| Min/Max             | min/max                     |      |
| First               | filter+findFirst+orElse     |      |



# 十七、Spring中常见的注解

- @SpringBootApplication：标明是SpringBoot项目，此注解等同于@Configuration，@EnableAutoConfiguration和@ComponentScan三个配置。
- @Configuration：标明是一个配置类，项目启动时会自动加载配置。相当于传统的xml配置文件，如果有些第三方库需要用到xml文件，建议仍然通过@Configuration类作为项目的配置主类——可以使用@ImportResource注解加载xml配置文件。
- @EnableAutoConfiguration：自动配置
- @ComponentScan：组件扫描注解。如果扫描到有@Component、@Controller、@Service等这些注解的类，并注册为Bean，可以自动收集所有的Spring组件，包括@Configuration类。
- @Import：用来导入其他配置类。
- @ImportResource：用来加载xml配置文件。
- @Controller：用于控制器类。（可以跳转页面，或返回接口数据）
- @RestController：用于控制器类。等效于@ResponseBody和@Controller组合。（只返回接口数据）
- @RequestMapping：提供路由信息，用在类或者API接口方法上。
- @ResponseBody：表示该方法的返回结果直接写入HTTP response body中。
- @PathVariable：获取接口请求路径中的参数。
- @Autowired：byType方式自动导入bean。一般用在类的成员属性上，表示自动导入bean，也可以用在构造方法上，当加上（required=false）时，就算找不到bean也不报错。
- @Service：用于修饰service层
- @Bean：放在方法的上面，是产生一个bean，并交给spring管理。
- @Value：注入Spring Boot配置文件application.properties中的属性值。
- @Component：泛指组件，当组件不好归类的时候，我们可以使用这个注解进行标注，同样可以被spring实例化。
- @Resource：默认byName方式自动导入bean。与@Autowired功能类似。



# 十八、JdbcTemplate使用

## 1.JdbcTemplate提供的主要方法：

- execute方法：可以执行任何SQL语句，一般用于执行DDL语句（数据定义语言，CREATE、ALTER与DROP这3个语法）。

```java
void execute(String sql);
```

- update方法：执行新增、删除、修改等语句。

```java
// 不带参数的
int update(String sql);
// 带参数的
int update(String sql, Object... args);
```

- batchUpdate方法：执行批处理语句。

```java
int[] batchUpdate(String sql, List<Object[]> batchArgs);
```

- query及queryForXXX方法：执行查询相关语句。
- call方法：执行存储过程、函数相关语句。



## 2.常用的查询方法示例：

**以下sql以MySQL为例进行举例**

- 查询单个值

```java
// 不带参数的
T queryForObject(String sql, Class<T> requiredType);
String name = jdbcTemplate.queryForObject("select name from user where id=1", String.class);

// 带参数的
T queryForObject(String sql, Class<T> requiredType, Object... args);
Integer age = jdbcTemplate.queryForObject("select age from user where id=?", String.class, 1);
```

- 查询单个对象信息

```java
// 不带参数的
T queryForObject(String sql, RowMapper<T> rowMapper);
User user = jdbcTemplate.queryForObject("select * from user where id=1", new BeanPropertyRowMapper<User>(User.class));

// 带参数的
T queryForObject(String sql, RowMapper<T> rowMapper, Object... args);
User user = jdbcTemplate.queryForObject("select * from user where id=?", new BeanPropertyRowMapper<User>(User.class), 1);
```

- 查询单个值的集合

```java
// 不带参数的
List<T> queryForList(String sql, Class<T> requiredType);
List<String> names = jdbcTemplate.queryForList("select name from user where age=18", String.class);

// 带参数的
List<T> queryForList(String sql, Class<T> requiredType, Object... args);
List<String> names = jdbcTemplate.queryForList("select name from user where age=?", String.class, 18);
```

- 查询多个对象信息

```java
// 不带参数的
List<T> query(String sql, RowMapper<T> rowMapper);
List<User> users = jdbcTemplate.query("select * from user where id<10", new BeanPropertyRowMapper<User>(User.class));

// 带参数的
List<T> query(String sql, RowMapper<T> rowMapper, Object... args);
List<User> users = jdbcTemplate.query("select * from user where id<?", new BeanPropertyRowMapper<User>(User.class), 10);
```

## 3.新增示例

```java
String sql = "insert into user(username, password) values (?, ?)";
int insertNum = jdbcTemplate.update(sql, new Object[]{"255", "255"});
```

## 4.删除示例

```java
String sql = "delete from user where id=?";
int deleteNum = jdbcTemplate.update(sql, new Object[]{1});
```

## 5.修改示例

```java
String sql = "update user set username=?, password=? where id=?";
int updateNum = jdbcTemplate.update(sql, new Object[]{"256", "256", 1});
```

## 6.批量操作示例

```java
List<Object[]> batchArgs = new ArrayList<Object[]>();
batchArgs.add(new Object[]{"777", "888"});
batchArgs.add(new Object[]{"666", "888"});
batchArgs.add(new Object[]{"555", "888"});
String sql = "insert into user(username, password) values (?, ?)";
jdbcTemplate.batchUpdate(sql, batchArgs);
```

以上方法基本满足了我们DAO层进行的操作,不过当你进行CRUD操作时如果传入的参数不确定,这时候你可能会想起ORM框架的便利。

没关系！Spring也为我们提供了这样的操作NamedParameterJdbcTemplate。



## 7.NamedParameterJdbcTemplate使用

在经典的 JDBC 用法中, SQL 参数是用占位符 ? 表示，并且受到位置的限制。

定位参数的问题在于，一旦参数的顺序发生变化，就必须改变参数绑定。

在 Spring JDBC 框架中，绑定 SQL 参数的另一种选择是使用具名参数(named parameter)。

**那么什么是具名参数？**

具名参数：SQL 按名称(以冒号开头)进行指定。具名参数更易于维护，也提升了可读性。

具名参数由框架类在运行时用占位符取代。

具名参数只在 NamedParameterJdbcTemplate 中得到支持。NamedParameterJdbcTemplate可以使用JdbcTemplate全部的方法。

**用法一：使用Map传参**

```java
String sql = "insert into user(username, password) values (:username, :password)";
Map<String, Object> paramMap = new HashMap<>();
paramMap.put("username", "111");
paramMap.put("password", "111");

int insertNum = namedParameterJdbcTemplate.update(sql, paramMap);
```



**用法二：使用对象传参**

```java
String sql = "insert into user(username, password) values (:username, :password)";
User user = new User();
user.setUsername("555");
user.setPassword("555");

SqlParameterSource sqlParameterSource = new BeanPropertySqlParameterSource(user);
int insertNum = namedParameterJdbcTemplate.update(sql, sqlParameterSource);
```

**获取新增的主键:**

NamedParameterJdbcTemplate还新增了KeyHolder类，使用它我们可以获得主键，类似Mybatis中的useGeneratedKeys。

```java
KeyHolder keyHolder = new GeneratedKeyHolder();
int insertNum = namedParameterJdbcTemplate.update(sql, sqlParameterSource, keyHolder);

// 获取新增用户的主键ID
long userId = keyHolder.getKey().longValue();
```



# Java新特性

- try-with-resources 语句确保了每个资源在语句结束时关闭。所谓的资源（resource）是指在程序完成后，必须关闭的对象。（Java9）

```java
public class Tester {
   public static void main(String[] args) throws IOException {
      System.out.println(readData("test"));
   } 
   static String readData(String message) throws IOException {
      Reader inputString = new StringReader(message);
      BufferedReader br = new BufferedReader(inputString);
      try (br) {
         return br.readLine();
      }
   }
}
```

- var局部变量类型推断。（Java10）

```java
var list = new ArrayList<>();
```

- javac HelloWorld.java和java HelloWorld两句可以合并成java HelloWorld.java执行（不会生成HelloWorld.class编译文件）（Java11）

以前

![image-20210220161526628](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210220161526628.png)

Java11中

![image-20210220161456959](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210220161456959.png)



# IDEA插件

File->Settings->Plugins

- Alibaba Java Coding Guidelines：阿里代码规范扫描。（建议安装）
- Lombok：简化实体类的setter、getter和构造方法等。**（必须）**
- SonarLint：代码规范扫描。（**必须**，比阿里更严格）



# 写在最后

- 阿里巴巴的《Java开发手册-嵩山版-20200803.pdf》**（必读）**，已上传至企业微信-微盘-书籍。
- 《Java8实战》.pdf在企业微信-微盘-书籍中，Java8新特性说明和使用。
- 阿里云大学->学习路线->基础入门->Java学习路线（免费视频课程）

![image-20210220110835726](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210220110835726.png)



- 菜鸟教程（https://www.runoob.com/java/java-tutorial.html），在线文档学习查阅方便。
- 设计模式第二版 刘伟 清华大学出版社
- 重构改善既有代码的设计 熊节  译  人民邮电出版社