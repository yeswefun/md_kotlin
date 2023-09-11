



延迟初始化
    类属性必须在构造时初始化

    某些成员只有在类构造之后才会被初始化
        MainActivity#onCreate获取各种View


    方案一， 初始化为null
        clas MainActivity : AppCompatActivity() {

            private var nameView : TextView? = null

            override fun onCreate(...) {
                ...
                nameView = findViewById(R.id.name_view)
                nameView?.text = "kotlin"
            }
        }


    方案二，lateinit
        clas MainActivity : AppCompatActivity() {

            private lateinit var nameView : TextView

            override fun onCreate(...) {
                ...
                nameView = findViewById(R.id.name_view)
                if (::nameView.isInitialized) {
                    nameView.text = "kotlin"
                }
            }
        }

        lateinit会让编译器忽略变量的初始化，不支持Int等基本类型

        开发者必须能够在完全确定变量的生命周期下使用


    方案三，lazy
        clas MainActivity : AppCompatActivity() {

            private var nameView by lazy {
                /*
                    其实就是一种代理
                    只有在nameView首次被访问时才会执行
                    Lamba表达式的返回值是最后一个语句的值
                */
                findViewById<TextView>(R.id.name_view)
            }

            override fun onCreate(...) {
                ...
                nameView.text = "kotlin"
            }
        }




代理

    接口代理，对象X 代替当前 类A 实现 接口B 的方法

    属性代理，对象X 代替 属性A 实现 setter/getter方法



接口代理，对象X 代替当前 类A 实现 接口B 的方法

```java
    interface Api {
        fun a()
        fun b()
        fun c()
    }

    class ApiImpl: Api {
        override fun a() {
            println("*** a ***")
        }

        override fun b() {
            println("*** b ***")
        }

        override fun c() {
            println("*** c ***")
        }
    }

    class ApiWrapper(val api: Api) : Api {
        override fun a() {
            api.a()
        }

        override fun b() {
            api.b()
        }

        override fun c() {
            println("*** decoration ***")
            api.c()
        }
    }

    class ApiWrapper2(val api: Api) : Api by api { // api的唯一要求就是实现Api接口
        override fun c() {
            println("*** decoration ***")
            api.c()
        }
    }
```




属性代理，对象X 代替 属性A 实现 setter/getter方法



lazy

```java
    clas MainActivity : AppCompatActivity() {

        private var nameView by lazy {
            /*
                其实就是一种代理
                只有在nameView首次被访问时才会执行
                Lamba表达式的返回值是最后一个语句的值
            */
            findViewById<TextView>(R.id.name_view)
        }

        override fun onCreate(...) {
            ...
            nameView.text = "kotlin"
        }
    }    


public actual fun <T> lazy(initializer: () -> T): Lazy<T> 
    = SynchronizedLazyImpl(initializer)

public interface Lazy<out T> {
    /*
        lazy 返回的对象代理了属性nameView的getter方法
    */
    public inline operator fun <T> Lazy<T>.getValue(thisRef: Any?, property: KProperty<*>): T 
        = value
}
```
 


observable

```java
    class StateManager {
        var state : Int by Delegates.observable(0) {
            property, oldValue, newValue ->
            println("onChange: p: $property(o: $oldValue -> n: $newValue)")
            println("************************************")
        }
    }


    /*
        onChange: p: var com.z.kt22.StateManager.state: kotlin.Int(o: 0 -> n: 3)
        ************************************
        onChange: p: var com.z.kt22.StateManager.state: kotlin.Int(o: 3 -> n: 6)
        ************************************
        onChange: p: var com.z.kt22.StateManager.state: kotlin.Int(o: 6 -> n: 9)
    */
    fun main() {
        val sm = StateManager()
        sm.state = 3
        sm.state = 6
        sm.state = 9
    }


public inline fun <T> observable(
    initialValue: T, 
    crossinline onChange: (property: KProperty<*>, oldValue: T, newValue: T) -> Unit
): ReadWriteProperty<Any?, T> = object : ObservableProperty<T>(initialValue) {
    override fun afterChange(property: KProperty<*>, oldValue: T, newValue: T) = onChange(property, oldValue, newValue)
}

/*
    ObservableProperty的实例代理了属性state的getter/setter
*/
public interface ReadWriteProperty<in T, V> : ReadOnlyProperty<T, V> {

    public override operator fun getValue(thisRef: T, property: KProperty<*>): V

    public operator fun setValue(thisRef: T, property: KProperty<*>, value: V)
}
```




```java
class GetterTest {
    val x: Int by X()

    var y: Int by X()
}

class X {
    operator fun getValue(thisRef: Any, property: KProperty<*>): Int {
        return Random(System.currentTimeMillis()).nextInt()
    }

    operator fun setValue(thisRef: Any, property: KProperty<*>, i: Int) {
        // 此处如何实现???
    }
}

fun main() {
    val g = GetterTest()
    println(g.x)
    println(g.x)
    TimeUnit.SECONDS.sleep(1)
    println(g.x)
}
```
