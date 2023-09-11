




内部类的定义

```java
class Outer {
    /*
        非静态
    */
    inner class Inner {
    }

    /*
        静态
    */
    class StaticInner {
    }
}

fun main() {
    val inner = Outer().Inner()
    val staticInner = Outer.StaticInner()
}
```

```java
public final class Outer {
   public final class Inner {
   }

   public static final class StaticInner {
   }
}
```




内部object

```java
class OuterObject {
    object StaticInnerObject {
    }
}
```

```java
public final class OuterObject {

   public static final class StaticInnerObject {
      @NotNull
      public static final OuterObject.StaticInnerObject INSTANCE;

      private StaticInnerObject() {
      }

      static {
         OuterObject.StaticInnerObject var0 = new OuterObject.StaticInnerObject();
         INSTANCE = var0;
      }
   }
}
```



```java
object OuterObject2 {
    /*
        内部的object不存在非静态的情况，故不用inner修饰
    */
    object StaticInnerObject {
    }
}
```


```java
public final class OuterObject2 {

   @NotNull
   public static final OuterObject2 INSTANCE;

   private OuterObject2() {
   }

   static {
      OuterObject2 var0 = new OuterObject2();
      INSTANCE = var0;
   }

   public static final class StaticInnerObject {
      @NotNull
      public static final OuterObject2.StaticInnerObject INSTANCE;

      private StaticInnerObject() {
      }

      static {
         OuterObject2.StaticInnerObject var0 = new OuterObject2.StaticInnerObject();
         INSTANCE = var0;
      }
   }
}
```





匿名内部类

```java
new Runnable() {
    @Override
    public void run() {

    }
}
```

```java
/*
    object xxx
    object省略了名称，即为匿名
*/
object: Runnable {
    override fun run() {

    }
}
```



非静态内部类在非静态环境下会持有外部类的引用，这可能会导致内存泄露
在静态环境就没有这样的问题
静态环境: 静态类内部，静态代码块



kotLin的匿名内部类可以实现多个接口

```java
object: Cloneable, Runnable {
    override fun run() {

    }
}
```



本地类


本地函数



