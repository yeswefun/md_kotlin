



object

```java
    public class Singleton {
        public static final Singleton INSTANCE = new Singleton();
    }

    /*
        定义单例，类加载时实例化对象
        Singleton既是类名也是对象名
    */
    object Singleton {

    }
```



访问object的成员
```java
object Singleton {
    var x : Int = 6
    fun y() {

    }
}
```

```java
fun main() {
    // 在 kotlin 中使用形式
    println(Singleton.x)
    println(Singleton.y())
}

public class Test {
    public static void main(String[] args) {
        // 在 java 中使用形式
        println(Singleton.INSTANCE.x)
        println(Singleton.INSTANCE.y())
    }
}
```

```java
public final class Singleton {

   private static int x;

   @NotNull
   public static final Singleton INSTANCE;

   public final int getX() {
      return x;
   }

   public final void setX(int var1) {
      x = var1;
   }

   public final void y() {
   }

   private Singleton() {
   }

   static {
        Singleton var0 = new Singleton();
        INSTANCE = var0;
        x = 6;
   }
}
```






静态成员, @JvmStatic

    object的成员直接按照java静态成员生成字节码
    对kotlin内部无任何影响
    java调用object的成员可以直接视为调用静态成员

```java
object Singleton {
    @JvmStatic
    var x: Int = 6
    @JvmStatic
    fun y() {
    }
}
```

```java
fun main() {
    // 在 kotlin 中使用形式
    println(Singleton.x)
    println(Singleton.y())
}

public class Test {
    public static void main(String[] args) {
        // 在 java 中使用形式
        Singleton.setX(8);
        println(Singleton.getX())
        println(Singleton.y())
    }
}
```

```java
public final class Singleton {
   
   private static int x;
   
   @NotNull
   public static final Singleton INSTANCE;

   @JvmStatic
   public static void getX$annotations() {
   }

   public static final int getX() {
      return x;
   }

   public static final void setX(int var0) {
      x = var0;
   }

   @JvmStatic
   public static final void y() {
   }

   private Singleton() {
   }

   static {
      Singleton var0 = new Singleton();
      INSTANCE = var0;
      x = 6;
   }
}
```





不生成 getter/setter, @JvmField
    属性不生成getter/setter
    访问方式等同于java的Field

```java
object Singleton {
    @JvmField
    var x: Int = 6
    @JvmStatic
    fun y() {
    }
}
```

```java
fun main() {
    // 在 kotlin 中使用形式
    println(Singleton.x)
    println(Singleton.y())
}

public class Test {
    public static void main(String[] args) {
        // 在 java 中使用形式
        println(Singleton.x)
        println(Singleton.y())
    }
}
```

```java
public final class Singleton {
   @JvmField
   public static int x;
   @NotNull
   public static final Singleton INSTANCE;

   @JvmStatic
   public static final void y() {
   }

   private Singleton() {
   }

   static {
      Singleton var0 = new Singleton();
      INSTANCE = var0;
      x = 6;
   }
}
```





普通类的静态成员

```java
class Foo {
    /*
        Only members in named objects and companion objects
        can be annotated with '@JvmStatic'
     */
    @JvmStatic fun y() { // error
    }
}
```


静态方法

```java
class Foo2 {
    companion object {
        @JvmStatic
        fun y() {
            
        }
    }
}
```

```java
public final class Foo2 {

   @NotNull
   public static final Foo2.Companion Companion = new Foo2.Companion((DefaultConstructorMarker)null);

   @JvmStatic
   public static final void y() {
      Companion.y();
   }

   public static final class Companion {
      @JvmStatic
      public final void y() {
      }

      private Companion() {
      }

      // $FF: synthetic method
      public Companion(DefaultConstructorMarker $constructor_marker) {
         this();
      }
   }
}
```



静态属性

```java
class Foo3 {
    /*
        生成非静态 Field
     */
    @JvmField var x : Int = 6
}
```

```java
public final class Foo3 {
   @JvmField
   public int x = 6;
}
```



```java
class Foo4 {
    companion object {
        /*
            生成静态 Feild
         */
        @JvmField var x : Int = 6
    }
}
```

```java
public final class Foo4 {

   @JvmField
   public static int x = 6;

   @NotNull
   public static final Foo4.Companion Companion = new Foo4.Companion((DefaultConstructorMarker)null);

   public static final class Companion {
      private Companion() {
      }

      // $FF: synthetic method
      public Companion(DefaultConstructorMarker $constructor_marker) {
         this();
      }
   }
}
```



object的构造器

```java
object Singleton { // 不能自定义构造器
    init { // 可以有若干个init块

    }
}
```

object的类继承

```java
object Singleton : Runnable {
    override fun run() {
        
    }
}
```

