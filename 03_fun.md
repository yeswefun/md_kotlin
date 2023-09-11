

函数的基本用法

    fun main(args: Array<String>): Unit {
        println(args.contentToString())
    }

    函数组成
        名称
        参数列表
        返回值类型
        执行体


    函数与方法的区别
        方法是一种特殊的函数
            有receiver的函数即为方法


函数类型

```java
/*
    demo
    demo: 6
    demo: 3.14
    3
*/
fun main() {

    // 类型自动推导，但此处必须声明
    val fn1: () -> Unit = ::demo
    val fn2: (Int) -> Unit = ::demo
    val fn3: (Double) -> Int = :: demo

    fn1()
    fn2(6)
    println(fn3(3.14))
}

fun demo() {
    println("demo")
}

fun demo(x: Int) {
    println("demo: $x")
}

fun demo(x: Double): Int {
    println("demo: $x")
    return x.toInt()
}
```



函数的引用

```java
/*
    p0: 3, p1: ok
    p0: 6, p1: no
*/
fun main() {
    val foo = Foo()
    val bar = foo::bar
    val bar2: (Int, String) -> Unit = foo::bar
    bar(3, "ok")
    bar2(6, "no")
}

class Foo {
    fun bar(p0: Int, p1: String) {
        println("p0: $p0, p1: $p1")
    }
}
```



# 可变长参数

```java
public class Demo {
    public static void main(String[] args) {
        System.out.println(Arrays.toString(args))
    }
}

/*
    [a, b, c]
 */
fun main(args: Array<String>) {
    println(args.contentToString())
}
```



```java
public class Demo {
    public static void main(String... args) {
        System.out.println(Arrays.toString(args))
    }
}

/*
    [a, b, c]
 */
fun main(vararg args: String) {
    println(args.contentToString())
}
```




# 默认参数

```java
fun main() {
    log()
    log(1)
    log(1, 2)
    log(1, 2, 3)
}

/*
    0, 0, 0
    1, 0, 0
    1, 2, 0
    1, 2, 3
 */
fun log(x:Int = 0, y:Int = 0, z:Int = 0) {
    println("$x, $y, $z")
}
```




# 具名参数

```java
fun main() {
    log(x = 3)
    log(y = 6)
    log(z = 9)
}

/*
    3, 0, 0
    0, 6, 0
    0, 0, 9
*/
fun log(x:Int = 0, y:Int = 0, z:Int = 0) {
    println("$x, $y, $z")
}
```


```java
fun main() {
    log(z = -1, x = 3)
    log(z = -1, y = 6)
    log(z = 9)
}

/*
    3, 0, -1
    0, 6, -1
    0, 0, 9
*/
fun log(x: Int = 0, y: Int = 0, z: Int) {
    println("$x, $y, $z")
}
```



# 多个返回值

```java
fun main() {
    val (a, b, c) = test()
    println("$a, $b, $c")
}

/*
    1, 3.14, ok
*/
fun test():Triple<Int, Double, String> {
    return Triple(1, 3.14, "ok")
}
```
