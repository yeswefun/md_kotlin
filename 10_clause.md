




变量

    java
        int x = 2;
        x = 3;

    kotlin
        var x = 2
        x = 3




只读变量
    java
        final int b = 3;

    kotlin
        val b:Int
            get() {
                return 3
            }

    作为局部变量时，以上两者没有区别

    作为类属性时
        class X {
            val b:Int
                get() { // 每次访问都是一个随机值
                    return (Math.random() * 100).toInt()
                }
        }




常量值
    java
        static final int b = 3;

    kotlin
        const val b = 3
            只写定义在全局范围
            只能修饰基本类型(及String)
            必须立即使用字面量初始化




常量引用
    val user = User(18, "Java") // 堆内存创建的对象
    user.id = 6 // 对象属性改变，但其引用没有改变





编译时常量 与 运行时常量

    编译时即可确定常量的值，并用值替换调用处
    const val int b = 3

    运行时才能确定值，调用处通过引用获取值
    val c: Int
        get() {
            return (Math.random() * 100).toInt()
        }


    java方法内部
        final int c;

        if (flag) {
            c = 3;
        } else {
            c = 4;
        }


    kotlin方法内部
        val c : Int

        if (flag) {
            c = 3
        } else {
            c = 4
        }








三目运算符
    java
        int z = x > y ? x : y;

    kotlin
        val z : Int = if(x > y) x else y




when
    java 的 switch
    kotlin 的 when

    eg-1:
        when(flag) {
            0 -> c = 5
            1 -> c = 10
            else -> c = 20
        }


    eg-2:
        var x : Any = ...
        when {
            x is String -> c = x.length
            x == 1 -> c = 10
            else -> c = 20
        }


    eg-3:
        var x : Any = ...
        c = when {
            x is String -> x.length
            x == 1 -> 10
            else -> 20
        }


    eg-4:
        c = when(val input = readLine()) {
            null -> 0
            else -> input.length
        }






try-catch

    try {
        c = a / b
    } catch (Exception e) {
        e.printStackTrace()
        c = 0
    }



    c = try {
        a / b
    } catch (Exception e) {
        e.printStackTrace()
        0
    }






运算符重载
    仅限于官方指定的符号


    x ==  y         // x.equals(y)
    x === y         // x == y


    2 + 3 -> 2.plus(3)


    val list = listOf(1, 2, 3)
    2 in list -> list.contains(2)


    val map = mapOf(1 to "one", 2 to "two")
    val value = map[2] -> map.get(2)
    map[2] = "sec" -> map.set(2, "sec")



    2 > 3 -> 2.compareTo(3) > 0


    val func = fun() {
        println("ok")
    }
    func() -> func.invoke()





    operator fun X.get(index: Int) : String = when(index) {
        1 -> "one"
        2 -> "two"
        else -> "other"
    }
    val x = X()
    println(x[1])





中缀表达式
    2 to 3 -> 2.to(3)

    infix fun <A, B> A.to(that : B) : Pair<A,B> = Pair(this, that)

