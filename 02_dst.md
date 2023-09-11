



集合框架
    List<T>
        可变, MutableList<T>
        不可变, List<T>


    Map<T>
        可变, MutableMap<T>
        不可变, Map<T>


    Set<T>
        可变, MutableSet<T>
        不可变, Set<T>




初始化

    val list = listOf(1, 2, 3)

    val list2 = mutableListOf(1, 2, 3)


    val map = mapOf<String, Any>("one" to 1, "two" to "2")

    val map = mutableMapOf<String, Any>("one" to 1, "two" to "2")


    Any -> Object，所有类的父类
    Nothing -> null，所有类的子类



别名
    val list = ArrayList<String>()
    
    typealias ArrayList<E> = java.util.ArrayList<E>
    typealias HashMap<K, V> = java.util.HashMap<K, V>



访问
    val list = listOf(1, 2, 3)

    list += 4           // list.add(4)
    list -= 3           // list.remove(3)

    println(list.size)

    println(list[0])    // list.get(0)

    list[0] = 6         // list.set(0, 6)

    println(list[0])



    val map = mapOf<String, Integer>("one" to 1, "two" to 2)

    println(map["one])  // map.get("one")

    map["one"] = 6      // map.put("one", 6)

    println(map["one])





Pair
    val pair = "one" to 1
    val pair2 = Pair("one", 1)


    val key = pair.first
    var value = pair.second

    val (key, value) = pair




Triple
    val triple = Triple("one", 2, 3.14)

    val x = triple.first
    val y = triple.second
    val z = triple.third

    val (x, y, z) = triple




集合遍历, for, forEach


集合包含关系, in


