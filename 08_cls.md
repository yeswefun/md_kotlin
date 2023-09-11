


类的定义

```java
public class Demo {

}

// 默认为 public, 且类里面没有东西时可省略 {}
class Demo
```


```java
public class Demo {
    
    private int x;

    public Demo(int x) {
        this.x = x;
    }
}

/*
    第一种形式
*/
class Demo {

    val x : Int

    constructor(x : Int) {
        this.x = x
    }
}

/*
    第二种形式
*/
class Demo constructor(x : Int) {
    val x : Int = x
}

/*
    第三种形式
*/
class Demo(x : Int ) {
    val x : Int = x
}

/*
    第四种形式
*/
class Demo(val x : Int )
```



类的实例化

```java
fun main() {
    val d = Demo(6)
    println(d.x)
}
```



抽象类的定义

```java
// 默认是 public 且是 open
abstract class Test {
    // abstract 修饰的方法默认就是 open
    abstract fun a()
    // 可重写
    open fun b() {}
    // 不可重写
    fun c() {}
}

class Demo : Test() {
    override fun a() {
        println("a")
    }
}
```



接口的定义

```java
// 默认是 public 且是 open
interface Test {
    fun test()
}

class Demo : Test {
    override fun test() {
        println("test")
    }
}
```




类的继承

```java
/*
    final 用来声明方法不可被重写
*/
class Demo : TestInterface, TestAbstract() {

}
```



backing field

    property = backing field + getter +  setter

    backing field 在接口或扩展方法中不存在


```java
public class Demo {
    
    private int id;

    public Demo() {

    }

    public Demo(int id) {
        this.id = id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public int getId() {
        return this.id;
    }
}


/*
    类的非静态属性
        默认是带有 getter, setter
*/
class Demo
@JvmOverloads
constructor(var id : Int)

class Demo
@JvmOverloads
constructor(id : Int) {
    /*
        id 是一个 属性 property
    */
    var id : Int = id
        get() {
            return field
        }
        set(value) {
            field = value
        }
}
```






属性引用

```java

class Item(var id: Int, var name: String)

fun main() {
    val item = Item(6, "匿名")
    val idRef = Item::id
    val nameRef = item::name

    println(idRef.get(item))
    println(nameRef.get())

    idRef.set(item, 8)
    nameRef.set("java")

    println(idRef.get(item))
    println(nameRef.get())
}
```
