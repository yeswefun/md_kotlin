




data class 的定义

```java
data class Book(var id: Long, var title: String)
```

```java
public final class Book {
   
   private long id;
   
   @NotNull
   private String title;

   // id 的 getter / setter
   // title 的 getter / setter

   public Book(long id, @NotNull String title) {

   }

   public final long component1() {
      return this.id;
   }

   @NotNull
   public final String component2() {
      return this.title;
   }

   @NotNull
   public final Book copy(long id, @NotNull String title) {

   }

   // $FF: synthetic method
   public static Book copy$default(Book var0, long var1, String var3, int var4, Object var5) {

   }

   @NotNull
   public String toString() {
      return "Book(id=" + this.id + ", title=" + this.title + ")";
   }

   public int hashCode() {

   }

   public boolean equals(@Nullable Object var1) {

   }
}
```


component
    定义在主构造器中的属性又称为 component
    编译器基于 component 生成 equals/hashCode/toString/copy



数据类可以进行解构操作
    val book = Book(100, "java")
    val (id, title) = book
        id == component1
        title == component2



javaBean 与 data class
    javaBean 可以被继承
    data class 不可以被继承
        思考



data class
    javaBean
    component
        主构造器
        相等性
        解构
    final



数据类 component 不可以自定义 getter/setter

属性最好使用 val

数据类并没有提供无参构造
    可以使用插件, NoArg
    AllOpen


无参构造
    反射，cls.newInstance()
    继承，子类的构造会自动调用父类的构造

