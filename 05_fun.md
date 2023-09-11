




let, run - 返回表达式结果

    val r = X.let { x -> R }

    val r = X.run { this: X -> R}



also, apply - 返回表receiver

    val x = X.also { x -> Unit }

    val x = X.apply { this: X -> Unit }



use - 自动关闭资源

    val r = Closeable.use { c -> R }


    File("x.txt").inputStream()
                .reader()
                .buffered()
                .use {
                    println(it.readLine())
                }



for
    for (i in 0 .. 9) { // [0, 9]
        println(i)
    }


    for (e in list) {
        println(e)
    }


forEach
    java
        list.forEach((e) -> {
            System.out.println(e);
        });

    kotlin
        list.forEach {
            println(it)
        }


    注: forEach 函数不能 continue 或 break

    list.forEach((e) -> {
        if (e == 2) {
            return;
        }
        System.out.println(e);
    })

    list.forEach {
        if (it == 2) {
            return @forEach
        }
        println(it)
    }





集合映射操作

filter - 保留满足条件的元素
    [1, 2, 3, 4]

    e % 2 == 0, [2, 4]

    list.stream()
        .filter( e -> e % 2 == 0);

    list.filter {
        it % 2 == 0
    }

    list.asSequence
        .filter {
            it % 2 == 0
        }



map - 类型A映射成类型B
    [1, 2, 3, 4]

    e * e, [1, 4, 9, 16]

    list.stream()
        .map(e -> e*e)

    list.map {
        it * it
    }

    list.asSequence()
        .map {
            it * it
        }


flatMap - 将一个元素映射成一个集合，再将所有的集合合并成一个集合
    [1, 2, 3]

    1 -> [0]
    2 -> [0, 1]
    3 -> [0, 1, 2]

    [0, 0, 1, 0, 1, 2]

    list.stream()
        .flatMap(e -> {
            List<Integer> all = new ArrayList<>();
            for (int x = 0; x < e; x++) {
                all.add(x);
            }
            return all.stream()
        })
    
    list.flatMap {
        0 until it
    }





集合的聚合操作

sum

reduce

flod

zip







