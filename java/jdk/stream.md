## Stream

#### 创建流Stream
Java8 中的 Collection 接口被扩展，提供两个获取流的方法 :
```
default Stream stream() : 返回一个顺序流
default Stream parallelStream() : 返回一个并行流
```

#### 由数组创建流
> 1. Java8 中的 Arrays 的静态方法 stream() 可以获取数组流 : static Stream stream(T[] array) : 返回一个流
> 2. 重载形式，能够处理对应基本类型的数组IntStream/LongStream/DoubleStream :
> 3. 由值创建流<br>
>	可以使用静态方法 Stream.of(), 通过显示值创建一个流，它可以接收任意数量的参数：public static Stream of(T… values) : 返回一个流
> 4. 由方法创建流 : 创建无限流<br>
> 可以使用静态方法 Stream.iterate() 和 Stream.generate(), 创建无限流
> 5. 迭代<br>
>	public static Stream iterate(final T seed, final UnaryOperator f)
> 6. 生成<br>
>	public static Stream generate(Supplier s)

#### Stream的中间操作实操
多个中间操作可以连接起来形成一个流水线，除非流水线上触发终止操作，否则中间操作不会执行任何的处理。而在终止操作时一次性全部处理，称为`惰性求值`。

* 筛选与切片系列

| 方法 | 描述 |
| ---- | ---- |
| filter(Predicate) | 接收 Lambda ， 从流中排除某些元素（true表示通过，false表示被过滤掉了） |
| distinct() | 筛选，通过流所生成元素的 hashCode() 和 equals() 去除重复元素 |
| limit(Long) | 截断流，使其元素不超过给定数量 |
| peek(Consumer) | 生成一个包含原Stream的所有元素的新Stream，同时会提供一个消费函数（Consumer实例），新Stream每个元素被消费的时候都会执行给定的消费函数； |
| S unordered() | 属于BaseStream的一个方法。使用较少。unordered操作不会进行任何显式的打乱流的操作(后面会有例子)。它的工作是：消除流中必须保持的有序约束，因此允许之后的操作使用 不必考虑有序的优化。 |
| skip(long) | 跳过元素，返回一个扔掉了前 n 个元素的流。若流中元素不足 n 个，则返回一个空流。与 limit(n) 互补 |

* 映射系列

| 方法 | 描述 |
| ---- | ---- |
| map(Function f)  | 接收一个函数作为参数，该函数会被应用到每个元素上，并将其映射成一个新的元素 |
| mapToInt(ToIntFunction f) | 同上，将其映射成一个Integer元素 |
| mapToLong(ToLongFunction f) | 同上，将其映射成一个Long元素 |
| mapToDouble(ToDoubleFunction f) | 同上,将其映射成一个Double元素 |
| flatMap(Function f) | 接收一个函数作为参数，将流中的每个值都换成另一个流，然后把所有流连接成一个流 |

* 排序

| 方法 | 描述 |
| ---- | ---- |
| sorted() | 产生一个新流，其中按自然顺序排序 |
| sorted(Comparator) | 产生一个新流，其中按比较器顺序排序 |



####  Stream的终止操作

终端操作会从流的流水线生成结果，其结果可以是任何不是流的值，例如 : List、 Integer，甚至是 void

> 注 : 流进行了终止操作后，不能再次使用

* 查找与匹配

| 方法 | 描述 |
| ---- | ---- |
| allMatch(Predicate p) | 检查是否匹配所有元素 |
| anyMatch(Predicate p) | 检查是否至少匹配一个元素 |
| noneMatch(Predicate p) | 检查是否没有匹配所有元素 |
| findFirst() | 返回第一个元素 |
| findAny() | 返回当前流中的任意元素 |
| count() | 返回流中元素总数 |
| max(Comparator c) | 返回流中最大值 |
| min(Comparator c) | 返回流中最小值 |
| forEach(Consumer c) | 内部迭代(使用 Collection 接口需要用户去做迭代，称为外部迭代。相反， Stream API 使用内部迭代) |
| forEachOrdered(Consumer c) | 基本同forEach |
| toArray() toArray(IntFunction g) | 这个使用起来和List的toArray差不多 |

> 除了使用forEachOrdered保证顺序外，Collectors.toList（）也可以保证顺序，二都最终都是通过ForEachOrderedTask类来实现的，具体可以参看ForEachOp.ForEachOrderedTask类中的代码。