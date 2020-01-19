## JDK 8 特性

### lamdba表达式
内容来源： [https://www.cnblogs.com/qdhxhz/p/9393724.html](https://www.cnblogs.com/qdhxhz/p/9393724.html)

1. Lamdba表达式
Lamdba表达式是一种匿名函数，简单地说，它是没有声明的方法，也即没有访问修饰符、返回值声明和名字。它可以写出更简洁、更灵活的代码。作为一种更紧凑的代码风格，使 Java 语言的表达能力得到了提升。

2. Lambda表达式的语法
```
基本语法：
i.  (parameters) -> expression
ii. (parameters) -> {statements;}

简单例子：
// 1. 不需要参数,返回值为 5  
() -> 5  
  
// 2. 接收一个参数(数字类型),返回其2倍的值  
x -> 2 * x  
  
// 3. 接受2个参数(数字),并返回他们的差值  
(x, y) -> x – y  
  
// 4. 接收2个int型整数,返回他们的和  
(int x, int y) -> x + y  
  
// 5. 接受一个 string 对象,并在控制台打印,不返回任何值(看起来像是返回void)  
(String s) -> System.out.print(s)
```

3. 函数式接口
> Lamdba表达式建立在函数式接口的基础上
> （1） 只包含一个抽象方法的接口，称为函数式接口
> （2） 可以通过Lamdba表达式来创建该接口的对象
> （3） 

