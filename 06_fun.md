


SAM: Single Abstract Method




java的匿名内部类

    ExecutorService executor = ...

    executor.submit(new Runnable() {
        @Override
        public voic run() {
            System.out.println("run...");
        }
    })


java的SAM
    ExecutorService executor = ...

    executor.submit(() -> System.out.println("run..."));



kotlin 的匿名内部类
    executor.submit(object: Runnable {
        override fun run() {
            println("run...")
        }
    })


kotlin的SAM
    executor.submit { println("run...") }

    lambda表达式可以被内联





kotlin的匿名内部类传统写法
    Runnable {
        override fun run() {
            println("run...")
        }
    }


kotlin的匿名内部类接口简化写法
    Runnable {
        println("run...")
    }




SAM转换
    SAM: Single Abstract Method
    
    方法: 只有一个参数
    参数: 只有一个方法的接口

    调用时可用lambda表达式转换为参数

    java, kotlin
