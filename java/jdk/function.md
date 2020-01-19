### 函数式接口
（1） 只包含一个抽象方法的接口。<br>
（2） 接口中唯一抽象方法的命名并不重要，因为函数式接口就是`对某一行为进行抽象`，主要目的就是支持`Lambda表达式`。<br>
（3） 可以在任意函数式接口上使用 `@FunctionalInterface` 注解，这样做可以检测它是否是一个函数式接口，同时 javadoc 也会包含一条声明，说明这个接口是一个函数式接口<br>



### Function所有接口

> 所有函数式接口都在这个包：java.util.function

| |Bi.| Int.| Long.| Double.| other|
| ---- | ---- | ---- |---- | ---- | ---- |
| Function | BiFunction | IntFunction |LongFunction|DoubleFunction|DoubleToIntFunction、DoubleToLongFunction、IntToDoubleFunction、LongToDoubleFunction、LongToIntFunction、IntToLongFunction、ToIntBiFunction、ToIntFunction、ToLongBiFunction、ToLongFunction、ToDoubleBiFunction、ToDoubleFunction|
| Predicate | BiPredicate | IntPredicate |LongPredicate|DoublePredicate||
| Supplier |      | IntSupplier |LongSupplier|DoubleSupplier|BooleanSupplier|
| Consumer | BiConsumer | IntConsumer |LongConsumer|DoubleConsumer|ObjIntConsumer、ObjLongConsumer、ObjDoubleConsumer|
| BinaryOperator ||IntBinaryOperator|LongBinaryOperator|DoubleBinaryOperator||
| UnaryOperator ||IntUnaryOperator|LongUnaryOperator|DoubleUnaryOperator||

### 接口详解

#### 接口 Function<T, R>
```
方法：R apply(T t)
介绍：传入两个对象，根据T返回R；Function所传递的其实是一种行为，在定义时没有进行实现，在使用的时候由用户进行实现。

默认方法：
1. default <V> Function<V, R> compose(Function<? super V, ? extends T> before)  
	方法本身接收了一个函数式接口，同时又返回了一个函数式接口。before函数式接口优先执行。
2. default <V> Function<T, V> andThen(Function<? super R, ? extends V> after)
	方法本身接收了一个函数式接口，同时又返回了一个函数式接口。after函数式接口后执行。
3. static <T> Function<T, T> identity()

BiFunction<T, U, R>接口：
	1. Bi→Bidirectional：两个，双向
	2. T表示传递给函数的第一个参数类型，U表示传递给函数的第二个参数类型，R表示函数的结果类型
	3. default <V> BiFunction<T, U, V> andThen(Function<? super R, ? extends V> after)
		该方法传入的参数是Function而不是BiFunction，是因为首先它将传进来的两个参数进行操作，得到一个结果，而after对该结果进行操作，只接收该结果，即一个参数，因此传入的参数为Function即可。
```

####  接口Predicate<T>
```
方法： boolean test(T t)
介绍：传入一个对象，返回一个boolean；Predicate表示一个判断，针对给定的参数T，来进行计算，如果输入参数符合匹配的条件，返回ture，否则返回false。

默认方法：
1. default Predicate<T> and(Predicate<? super T> other)
	当前的Predicate与另外的一个Predicate进行逻辑与，如果当前的Predicate返回的结果为false，那么后者将不会被计算。
2. default Predicate<T> negate()
	表示当前的Predicate逻辑的相反面。
3. default Predicate<T> or(Predicate<? super T> other)
	表示当前的Predicate与另外一个Predicate的逻辑或的操作。

静态方法：
1. static <T> Predicate<T> isEqual(Object targetRef)
	判断与targetRef是否相等
```

#### 接口Supplier<T>
```
方法：T get()
介绍：	返回一个对象；Supplier表示结果的供应者，其作用就是不接收任何参数，同时返回一个结果。
```

#### 接口Consumer<T>
```
方法：void accept(T t)
介绍：传入一个对象，没有返回值； consumer表示一个接受单个输入参数并且没有返回值的操作，Consumer接口期望执行带有副作用的操作（即：Consumer的操作可能会更改输入参数的内部状态）。

默认方法：
1. default Consumer<T> andThen(Consumer<? super T> after)
	两个Consumer, 先执行当前的Consumer，再执行另外一个Consumer。
```

#### 接口UnaryOperator<T>
```
介绍：一元运算，继承自Function<T, T>；传入参数类型与返回类型相同
静态方法：
1. static <T> UnaryOperator<T> identity()
```

#### 接口BinaryOperator<T> 
```
介绍：二无运算，继承自 extends BiFunction<T,T,T>；返回类型与传入两个参数类型相同
静态方法：
1. public static <T> BinaryOperator<T> minBy(Comparator<? super T> comparator)
2. public static <T> BinaryOperator<T> maxBy(Comparator<? super T> comparator)
```

#### Bi系列
> BiConsumer,BiFunction,BiPredicate:从一个参数值,扩展支持到两个参数；

#### 基本类型系列
> 为了减小装箱拆箱而消耗的性能；
> 
> Double/Int/Long 简称 DIL<br>
> DILXXX：代表参数值泛型<br>
> ToDILXXX：代表返回值泛型<br>
> DILToDILXXX：To前面代表参数值泛型 ,To后边代表返回值泛型<br>
> ObjDILConsumer(特殊) :相当于BiConsumer, 代表的第二个参数类型的泛型

### Lamdba表达式
> Lamdba表达式可理解为简洁的匿名函数，<br>
> 简单地说，它即没有声明的方法，也没有访问修饰符、返回值声明和名字。<br>
> 它可以写出更简洁、更灵活的代码。作为一种更紧凑的代码风格，使 Java 语言的表达能力得到了提升。<br>
> 
> 语法：(parameters) -> expression<br>
>      (parameters) ->{ statements; }<br>
>
> Lambda是建立在函数式接口的基础上的<br>

### 方法引用
>  简单地说，就是一个Lambda表达式。<br>
>  方法引用提供了一种引用而不执行方法的方式，它需要由兼容的函数式接口构成的目标类型上下文。<br>
>  计算时，方法引用会创建函数式接口的一个实例。<br>
> 当Lambda表达式中只是执行一个方法调用时，不用Lambda表达式，直接通过方法引用的形式可读性更高一些。<br>

方法引用的方式：

| 类型               | 示例                        |
| ------------------ | --------------------------- |
| 引用对象的实例方法 | Oboject::instanceMethodName |
| 引用类的静态方法   | ClassName::staticMethodName |
| 引用类的实例方法   | ClassName::methodName<br> /* 第一个参数为调用方法，后面的参数作为实例方法的传参 */ |
| 引用构造函数       | ClassName::new              |
| 数组引用  | Type::new (new String[]::new) |






