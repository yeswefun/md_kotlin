


class User constructor(var id: Int, var name: String)
    
    constructor: 在类声明中的主构造器
    
    在主构造器中使用var或val声明的变量，表示该变量作为类属性
        class User(var id: Int, var name: String)
            id，name 是类属性

        class User(var id: Int, name: String)
            id是类属性
            name是构造器的普通参数

            id在类内全局可见
            name在构造器内可见(init块，属性初始化)

        class User(var id: Int, name: String) {
            
            var name : String

            var test : String = name
            
            init { // 类似于主构造器的方法体
                this.name = name
            }

            init { // init块可以有多个，最终会合并执行
                println("init...")
            }

            init { // 相当于java的构造代码块

            }
        }




属性必须初始化
    class User(var id: Int, name: String) {
        
        var name : String // 显示报错
        
        init {
            // this.name = name
        }




继承父类

    abstract class Animal

    class User(var id: Int, var name: String) : Animal() // 调用父类的构造器

    class User(var id: Int, var name: String) : Animal() { // 调用父类的构造器
        /*
            类名称后面的是主构造器
            类内的是次构造器
        */
        constructor(id: Int) : this(id, "匿名") // 次构造器调用主构造器，确保构造路径唯一
    }

    class User(var id: Int, var name: String = "匿名") : Animal() // 主构造器上使用默认参数
    

    class User
    @JvmOverloads
    constructor(var id: Int, var name: String = "匿名") : Animal() // 主构造器上使用默认参数
        此时 constructor 关键字不能省
        @JvmOverloads 主构造器上的默认参数在java代码中可以以重载的形式调用



权限修饰符
    java
        public
        default，包内可见
        protected，包内及子类可见
        private，类内可见

    kotlin
        public
        internal 模块内可见
        protected 类内或子类可见
        private 类内或文件内可见



构造器的可见性
    class User private constructor(var id : Int, var name : String)


属性的可见性
    class User constructor(private var id : Int, var name : String)
        // 私有化属性，外部无法直接访问

    class User constructor(private var id : Int, var name : String) {
        // 私有化属性，外部无法直接访问
        private var age : Int = 18
    }

    class User constructor(private var id : Int, var name : String) {
        // 私有化属性，外部无法直接访问
        var age : Int = 18
            private set
            // 外部只读，相当于 val
    }




顶级声明的可见性
    顶级声明指的是文件内直接定义的属性，函数，类等

    顶级声明不支持 protected

    顶级声明被 private 修饰表示文件内部可见

