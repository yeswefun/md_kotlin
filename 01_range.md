




闭区间
    val intRange = 1 .. 3           // [1, 3]

    val charRange = 'a' .. 'z'      // ['a', 'z']



开区间
    val intRange = 1 until 3        // [1, 3)

    val charRange = 'a' until 'z'   // ['a', 'z')



倒序闭区间
    val rIntRange = 3 downTo 1      // [3, 2, 1]

    val rCharRange = 'z' downTo 'z' // ['z', ... , 'a']



区间步长
    val intRange = 1 .. 3 step 2    // [1, 3]

    val charRange = 'a'..'z' step 2 // ['a', 'c', ...]



遍历
    val intRange = 1 .. 3 step 2

    for (e in  intRange) {
        println(e)
    }

    intRange.forEach { it -> 
        println(it)
    }



包含
    val intRange = 1 .. 3 step 2

    if (1 in intRange) {

    }

    if (2 !in intRange) {

    }



应用
    val arr = intArrayOf(1, 2, 3)

    for (index in 0 until arr.size) {
        println(arr[index])
    }

    for (index in arr.indices) {
        println(arr[index])
    }



