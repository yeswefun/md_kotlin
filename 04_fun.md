


匿名函数
    Lambda
    SAM转换


    一个普通的函数
        fun test() {
            println("ok")
        }

    一个匿名函数
        fun() {
            println("ok")
        }

    函数类型
        val func = fun() {
            println("ok")
        }

    匿名函数的类型
        val func : () -> Unit = fun() {
            println("ok")
        }


    无参数，Lambda表达式的定义
        Runnable r = () -> {
            System.out.println("ok");
        }

        val r : () -> Unit = {
            println("ok")
        }

        val r = {
            println("ok")
        }

        lambda表达式的返回值是最后一个表达式的值



    有参数，Lambda表达式的定义
        interface Func1 {
            void invoke(int p);
        }

        Func1 fn1 = (p) -> {
            System.out.println(p)
        }


        val fn1 : (int) -> Unit = { p : Int ->
            println(p)
        }

        val fn1 : Functaion1<Int, Unit> = { p : Int  -> 
            println(p)
        }

        类型自动推导
        val fn1 : Functaion1<Int, Unit> = { p -> 
            println(p)
        }

        类型自动推导
        val fn1 = { p : Int  -> 
            println(p)
        }

        只有一个参数可以省略，kotlin会将参数以it传入
        val fn1 : Functaion1<Int, Unit> = { p -> 
            println(p)
        }


        val fn1 : Functaion1<Int, Unit> = { it -> 
            println(it)
        }

        val fn1 : Functaion1<Int, Unit> = {
            println(it)
        }



    SAM: Single Abstract Method
        interface Function1 {
            String invoke(int p);
        }





高阶函数
    常见高阶函数
    函数式编程

    参数包含函数类型
        fun test(block: () -> Unit) {
            block()
        }

    返回值为函数类型
        fun test() : () -> Long {
            return {
                System.currentTimeMillis()
            }
        }

    高阶函数: 参数包含函数类型 或 返回值为函数类型 的函数

    常见高阶函数
        inline fun IntArray.forEach(action : (Int) -> Unit) : Unit {
            for (e in this) {
                action(e)
            }
        }

        inline fun <R> IntArray.map(transform : (Int) -> R) : List<R> {
            return mapTo(ArrayList<R>(size), transform)
        }

    高阶函数的调用
        intArray.forEach(::println)
            println 的类型为 (Int) -> Unit

        intArray.forEach({
            println("-> $it")
        })

        参数为函数类型，且为最后一个参数，可以移动到括号外
        intArray.forEach() {
            println("-> $it")
        }

        只有一个 lambda 表达式作为参数可省略小括号
        intArray.forEach {
            println("-> $it") // 只有一个参数的lambda表达式
        }


    自定义高阶函数
        fun cost(block : () -> Unit) {
            val start = System.currentTimeMillis()
            block()
            println(System.currentTimeMillis() - start)
        }


        fun fibonacci() : () -> Long {
            var first = 0L
            var second = 1L

            return {
                val next = first + second
                val current = first
                first = second
                second = next
                current
            }
        }





内联函数
    这里暂时跳过

