---
title: scala_笔记_01
date: 2019-09-29 15:49:06
tags: scala
---

##### 定义变量

可以使用 val 或者 var 来定义变量

 val 定义的是常变量，类似于java的final变量，一经定义就不可以再重新赋值

 var 定义任意非final变量，可以任意重新赋值

```shell
scala> val msg1 = "wojiushiwo"

msg1: String = wojiushiwo


scala> msg1 = "wojiushiwo "

​            ^
​       error: reassignment to val
```



```shell
scala> var msg2 = "wojiushiwo"

msg2: String = wojiushiwo


scala> msg2 = "wojiushiwo "

mutated msg2
```



指定类型的声明变量

```shell
scala> val msg3:String = "wojiushiwo3"

msg3: String = wojiushiwo3
```



##### 遍历

读取输入进行打印的几种方式

方式一: while

```scala
var i = 0
while (i < args.length) {
	println(args(i))
  i+=1
}
```

⚠️  scala中没有 i++ 或者 ++i的操作，scala中访问数组的方式不是[] 而是 ()



方式二: foreach

```scala
args.foreach(arg => println(arg))
```



方式二点五: foreach 简化

```scala
args.foreach(println)
```

⚠️ 如果一个函数只有一个参数并且只包含一个表达式，那么你无需明确指明参数



方式三: for

```scala
for (arg <- args)
	println(arg)
```



##### 数组

定义参数的几种方式

```scala
val greetStrings = new Array[String](3)
greetStrings(0) = "Hello"
greetStrings(1) = ","
greetStrings(2) = "World"

for (i <- 0 to 2)
	print(greetStrings(i))
```



```scala
val greetStrings = new Array[String](3)
greetStrings.update(0, "Hello")
greetStrings.update(1, ",")
greetStrings.update(2, "World")

for (i <- 0 to 2)
	print(greetStrings.apply(i))
```



```scala
val greetStrings = Array("Hello", ",", "World")
```



```scala
val greetStrings = Array.apply("Hello", ",", "World")
```

⚠️ scala数组的数据是可变的，想要不可变使用 List



##### List

使用 ::: 可以将两个List进行连接

```scala
val oneTwo = List(1, 2)
val threeFour = List(3, 4)
val oneTwoThreeFour = oneTwo ::: threeFour
```



可以使用 :: 来通过向List中添加元素的方式来创建List

```scala
val oneTt = 1 :: 2:: 3 :: Nil

val oneTd = Nil.::(3).::(2).::(1)
```

⚠️ List中的数据只能是同一种数据类型



##### Tuples

可以使用 ._和索引来访问员组的元素 (矢量的分量，注意和数组不同的是，元组的索引从 1 开始)

```scala
val pair = (99, "wojiushiwo")
print(pair._1)
print(pair._2)
```

⚠️ 目前 scala支持的元祖最大长度为22，如果需要，可以自己扩展长度



##### Set

```scala
var jetSet = Set("Beoing", "Airbus")
jetSet += "Lear"
println(jetSet.contains("Cessna"))
```



##### Map

```scala
val romanNumeral = Map(1 -> "I", 2 -> "II", 3 -> "III", 4 -> "IV", 5 -> "V")
print(romanNumeral(4))
```



#####函数编程风格

- Scala 语言的一个特点是支持面向函数编程
- 如果代码中含有 var 类型的变量，这段代码就是传统的指令式编程，如果代码只有 val 变量，这段代码就很有可能是函数式代码，因此学会函数式编程关键是不使用 vars 来编写代码
- 能不用 Vars，尽量不用 vars,能不用 mutable变量，尽量不用 mutable变量，能避免函数的副作用，尽量不产生副作用



##### 读取文件

```scala
import scala.io.Source

if (args.length > 0) {
	for (line <- Source.fromFile(args(0)).getLines())
		println(line.length + " " + line)
} else 
		Console.err.println("Please enter filename")
```







```scala
import scala.collection.mutable.Map

class ChecksumAccumulator{
  private var sum = 0
  def add (b:Byte):Unit = sum += b
  def checksum():Int = ~(sum & 0xFF) + 1
}

object ChecksumAccumulator{
  private val cache = Map[String, Int]()
  def calculate(s:String):Int = 
  	if (cache.contains(s))
  		cache(s)
 		else {
      var acc = new ChecksumAccumulator
      for (c <- s)
      	acc.add(c.toByte)
    	val cs = acc.checksum()
      cache += (s -> cs)
      cs
    }
}

println(ChecksumAccumulator.calculate("welcome to scala"))
```





- Scala 的类定义可以有参数，称为类参数
- 类定义和主构造函数合并在一起，在定义类的同时也定义了类的主构造函数
- 在 Scala 中，可以使用 override 来重载基类定义的方法，必须使用 override 关键字表示重新定义基类中的成员
- Scala 调用这些函数或方法的调用者需要满足的条件; Scala 中解决这个问题的一个方法是使用 require 方法





scala 辅助构造函数


