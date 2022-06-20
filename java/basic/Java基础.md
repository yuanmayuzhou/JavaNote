# Java基础
## 1.String类
### String 特性：

1.String 表⽰字符串类型，属于引⽤数据类型，所以其储存的是地址；

2.java 中规定，双引号括起来的字符串是不可变的，也就说” name “永远也只能是” name “，不能改变；

3.由于字符串在使⽤中过于频繁，所以为了保证执⾏效率，SUN 公司设定把字符串放到了⽅法区的字符串常量池中；

4.凡是双引号括起来的，都在字符串常量池中有⼀份；

字符串常量池：
String str = ” zifu“ + ” chuan “ ；
//（先查找字符串常量池中有⽆“zifu”“chuan”，若⽆）在字符串常量池中创建 ” zifu “ ，” chuan “ ，”  zifuchuan “，三个字符
串；若print (str)，则str会直接指向字符串常量池，并返回“ zifuchuan ”
String strr = “  zifu ”；
//字符串常量池⽆变化（因为已存在“zifu”）；

辅助理解：
```java
  String s1=“ java ”；
  String s2=“ java ”；
  System.out.println( s1==s2 ) // 输出true/false？
```
答：true，因为字符串常量池中的“java”是不变的，所以⽆论是s1还是s2，储存的地址对应的都是那个字符串常量池中
的“java”，所以⾃然储存的地址是相同的，⽽“==”⽐较地址，输出true；
```java
  String s1=new String(“ java ”)；
  String s2=new String(“ java ”)；
  System.out.println( s1==s2 ) // 输出true/false？
```
答：false，s1与s2只是储存了“=”右边在堆内存中创建的String对象的地址，⽽这俩个new出来的地址是不同的，所以输
出“false”；

### 内存中⼀共创建了⼏个对象？

答：3个，⽅法区中⼀个 “java”，堆内存中俩个String对象；

## 2.equals和==的区别
equals()和“==”操作用于对象的比较，检查俩对象的相等性，但是他们俩的主要区别在于前者是方法后者是操作符。由于java不支持操作符重载(overloading)，“==”的行为对于每个对象来说与equals()是完全相同的，但是equals()可以基于业务规则的不同而重写(overridden )。另一个需要注意的不同点是“==”习惯用于原生(primitive)类型之间的比较，而equals()仅用于对象之间的比较。同时初学者奋力地想找到什么时候使用等号操作“==”，什么时候使用equals方法。这篇教程中你将将看到equals()方法和“==”操作是如果工作的、他们之间有什么不同、什么时候用“==”、什么时候使用equals()方法。

### “==”等号操作是什么

“==”或等号操作在Java编程语言中是一个二元操作符，用于比较原生类型和对象。就原生类型如boolean、int、float来说，使用“==”来比较两者，这个很好掌握。但是在比较对象的时候，就会与equals()造成困惑。“==”对比两个对象基于内存引用，如果两个对象的引用完全相同(指向同一个对象)时，“==”操作将返回true，否则返回false。

### 什么是equals方法

equals()方法定义在Object类里面，根据具体的业务逻辑来定义该方法，用于检查两个对象的相等性。例如：两个Employees被认为是相等的如果他们有相同的empId的话，你可以在你自己的domain对象中重写equals方法用于比较哪两个对象相等。equals与hashcode是有契约的(无论什么时候你重写了equals方法，你同样要重写hashcode()方法)，默认的equals方法实现是与“==”操作一样的，基于业务需求重写equals方法是最好的实践之一，同样equals与compareTo保持一致也不足为奇，以至于存储对象在Treemap或treeset集合中时，将使用compareTo方法检查相等性，行为是一致的。

### ==与equals方法的区别

==与equals的主要区别是：==常用于比较原生类型，而equals()方法用于检查对象的相等性。另一个不同的点是：如果==和equals()用于比较对象，当两个引用地址相同，==返回true。而equals()可以返回true或者false主要取决于重写实现。最常见的一个例子，字符串的比较，不同情况==和equals()返回不同的结果。

## 3.Bigdecimal
### BigDecimal概述

Java在java.math包中提供的API类BigDecimal，用来对超过16位有效位的数进行精确的运算。双精度浮点型变量double可以处理16位有效数，但在实际应用中，可能需要对更大或者更小的数进行运算和处理。一般情况下，对于那些不需要准确计算精度的数字，我们可以直接使用Float和Double处理，但是Double.valueOf(String) 和Float.valueOf(String)会丢失精度。所以开发中，如果我们需要精确计算的结果，则必须使用BigDecimal类来操作。

BigDecimal所创建的是对象，故我们不能使用传统的+、-、*、/等算术运算符直接对其对象进行数学运算，而必须调用其相对应的方法进行操作。

### 基本运算
加法
```java
bigDecimal.add(bigDecimal2);
```

减法
```java
bigDecimal.subtract(bigDecimal2);
```

乘法
```java
bigDecimal.multiply(bigDecimal2);
```

除法
```java
bigDecimal.divide(bigDecimal2);
```

平方
```
bigDecimal.pow(2);
```

取反
```java
bigDecimal.negate(2);
```

取绝对值
```java
bigDecimal.abs(2);
```

正负号函数
```
BigDecimal bigDecimal1 = new BigDecimal(25);
BigDecimal bigDecimal2 = new BigDecimal(0);
BigDecimal bigDecimal3 = new BigDecimal(-25);
System.out.println(bigDecimal1.signum());
System.out.println(bigDecimal2.signum());
System.out.println(bigDecimal3.signum());
//输出结果：1，0，-1，正数输出1，0输出0，负数输出-1
```

取最大值
```java
BigDecimal bigDecimal1 = new BigDecimal(25);
BigDecimal bigDecimal2 = new BigDecimal(12);
System.out.println(bigDecimal1.min(bigDecimal2));
//取两值较大者
```

取最小值
```java
BigDecimal bigDecimal1 = new BigDecimal(25);
BigDecimal bigDecimal2 = new BigDecimal(30);
System.out.println(bigDecimal1.min(bigDecimal2));
//取两值较小者
```

取余
```java
BigDecimal bigDecimal1 = new BigDecimal(21);
BigDecimal bigDecimal2 = new BigDecimal(5);
System.out.println(bigDecimal1.remainder(bigDecimal2));
//取余，20除5后余1
```

除后取余
```java
BigDecimal bigDecimal1 = new BigDecimal(32);
BigDecimal bigDecimal2 = new BigDecimal(5);
BigDecimal decimalArr[] = bigDecimal1.divideAndRemainder(bigDecimal2);
//返回数组，[0]为除法结果，[1]为余数
```

返回对象的精度(位数)
```java
BigDecimal bigDecimal1 = new BigDecimal("12.112");
System.out.println(bigDecimal1.precision());
//输出5
```

设置精度
```java
BigDecimal bigDecimal1 = new BigDecimal("12.112");
System.out.println(bigDecimal1.setScale(2, RoundingMode.DOWN));
BigDecimal bigDecimal2 = new BigDecimal(20.221);
System.out.println(bigDecimal2.setScale(2, RoundingMode.UP));
//输出12.11，保留两位小数，向下取整
//输出20.23，保留两位小数，向上取整
```

比较
```java
BigDecimal bigDecimal1 = new BigDecimal(20);
BigDecimal bigDecimal2 = new BigDecimal(10);
System.out.println(bigDecimal1.compareTo(bigDecimal2));
//输出1，比较两个对象的大小
//bigDecimal1大于bigDecimal2输出1，等于输出0，小于输出-1
```

## 4.重载和重写
重写`(Override)`

从字面上看，重写就是 重新写一遍的意思。其实就是在子类中把父类本身有的方法重新写一遍。子类继承了父类
原有的方法，但有时子类并不想原封不动的继承父类中的某个方法，所以在方法名，参数列表，返回类型(除过子
类中方法的返回值是父类中方法返回值的子类时)都相同的情况下， 对方法体进行修改或重写，这就是重写。但要
注意子类函数的访问修饰权限不能少于父类的。

```java
public class Father {
    public static void main(String[] args) {
        Son s = new Son();
        s.sayHello();
    }

    public void sayHello() {
        System.out.println("Hello");
    }
}

class Son extends Father {
    @Override
    public void sayHello() {
        System.out.println("hello by ");
    }
}
```

原因： 在某个范围内的整型数值的个数是有限的，而浮点数却不是。

重写总结：

1.发生在父类与子类之间

2.方法名，参数列表，返回类型（除过子类中方法的返回类型是父类中返回类型的子类）必须相同

3.访问修饰符的限制一定要大于被重写方法的访问修饰符（public>protected>default>private)

4.重写方法一定不能抛出新的检查异常或者比被重写方法申明更加宽泛的检查型异常

重载`（Overload）`

在一个类中，同名的方法如果有不同的参数列表（参数类型不同、参数个数不同甚至是参数顺序不同）
则视为重载。同时，重载对返回类型没有要求，可以相同也可以不同，但不能通过返回类型是否相同来
判断重载。

```java
public class Father {
    public static void main(String[] args) {
        Father s = new Father();
        s.sayHello();
        s.sayHello("wintershii");
    }

    public void sayHello() {
        System.out.println("Hello");
    }

    public void sayHello(String name) {
        System.out.println("Hello" + " " + name);
    }
}
```

重载总结：

1.重载Overload是一个类中多态性的一种表现

2.重载要求同名方法的参数列表不同(参数类型，参数个数甚至是参数顺序)

3.重载的时候，返回值类型可以相同也可以不相同。无法以返回型别作为重载函数的区分标准

