


扩展方法

```java
fun main() {
    print("*".zrepeat(6))
}

fun String.zrepeat(n: Int): String {
    if (n <= 0) {
        return this
    }
    val sb = StringBuilder()
    for (i in 1..n) {
        sb.append(this)
    }
    return sb.toString()
}
```



空安全
    kotlin 的修饰符 var, val 默认为不可空类型

    var str : String = "*"
    var str2 : String = "#"

    var str : String? = null
    var str2 : String? = null




运算符，?

```java
type? == @Nullable type
type  == @NonNull type
```



运算符，?.

```java
    foo?.bar()

    等价于下面

    if (foo != null) {
        return foo.bar()
    } else {
        return null
    }
```



运算符，?:

```java
    foo ?: bar

    等价于下面

    if (foo != null) {
        return foo
    } else {
        return bar
    }
```



运算符，!!

```java
    foo!!

    等价于下面

    if (foo != null) {
        return foo
    } else {
        throw new NullPointerException("null")
    }
```



运算符，as?

```java
    foo as? Type

    等价于下面

    if (foo instanceof Type) {
        return (Type) foo
    } else {
        return null
    }
```




类型转换

```java
interface Device

class Phone(var id : String) : Device

fun main() {
    val device: Device = Phone("13838389438")
    // device 是 Device 类型
    if (device is Phone) { // device 是 Phone 类型
        //println((device as phone).id) // 类型转换
        println(device.id) // 智能类型转换
    }
    // device 是 Device 类型
}
```



```java
fun main() {
    var value: String? = null
    value = makeValue(2)
    if (value != null) { // 智能类型转换为 String
        println(value.length)
    }
}

fun makeValue(i: Int): String? = if (i % 2 == 0) "hello" else null

```



不支持智能类型转换的情况

```java
var tag : String? = null

fun main() {
    if (tag != null) {
        // Smart cast to 'String' is impossible, 
        // because 'tag' is a mutable property 
        // that could have been changed by this time
        println(tag.length) // warning
    }
}
```




安全类型转换

```java
    println((device as phone).id)       // as  类型转换，强转有风险
    println((device as? phone)?.id)     // as? 强转失败，返回null
```



建议
    尽量使用 val 声明不可变引用

    尽可能减少函数对外部变量的访问，为函数式编程提供基础

    必要时创建局部变量指向外部变量，避免因外部变量的变化而引起程序错误


