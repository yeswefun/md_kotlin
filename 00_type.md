



类型

    Byte
        byte/Byte

    Short
        short/Short

    Int
        int/Integer

    Long
        long/Long

    Float
        float/Float
    
    Double
        double/Double

    Char
        char/Character

    Boolean
        boolean/Boolean

    String
        String



变量声明
    修饰符 变量名 : 类型 = 变量值

    修饰符
        var 可读可写
        val 只读变量


类型推导
    var a = 2
    val s = "kotlin"



类型转换
    不允许隐式转换

    implicit 隐式
    explicit 显式

    val a: Int = 10
    val b: Long = a.toLong()



类型比较
    a === b // reference，java(a == b)
    a ==  b // value，java(a.equals(b))



字符串模板
    println("hello $name")
    println("size: ${name.size})




数组
    IntArray
        int[]

    Array<Int>
        Integer[]
引用类型

    CharArray
        char[]

    Array<Char>
        Character[]


    Array<String>
        String[]


    基本类型元素组件的数组，XxxArray
    包装类型元素组成的数组，Array<Xxx>

    类型自动推导, arrayOf(引用类型)



数组初始化

    val c0 = intArrayOf(1, 2, 3)

    val c1 = IntArray(3) {it + 1} // it 为索引，索引从0开始


    val c2 = IntArray(5)
    println(c2.size)



数组访问
    val c3 = arrayOf("aa", "bb")
    c3[1] = "cc"
    println("[0] = ${c3[0]}, [1] = ${c3[1]}")



数组遍历
    val arr = arrayOf(1, 2, 3)

    for(elem in arr) {
        println(elem)
    }

    arr.forEach { elem ->
        println(elem)
    }

    arr.forEach {
        println(it)
    }


包含关系
    val arr = arrayOf(1, 2, 3)
    
    if (1 in arr) {

    }

    if (3 !in arr) {

    }


