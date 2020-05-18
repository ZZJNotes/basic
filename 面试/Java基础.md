## Java内部类

### 1. 静态嵌套类(Static Nested Class)和内部类(Inner Class)的不同？

**内部类**

- 需要在外部类实例化之后才能实例化
- 可以访问外部类的所有成员和方法
  - 普通内部类对象隐式保存了一个引用，指向创建它的外部类对象

**静态嵌套类**

- 它可以不依赖于外部类实例而被实例化，这个内部类相当于变为外部类
- 只能访问外部类中的static属性和方法
- 不需要内部类对象与外部类对象之间有联系

**实例化内部类的格式**

- 非static定义的内部类：

  外部类.内部类 内部类对象 = new 外部类().new 内部类

  ```java
  Outer.Inner a = new Outer().new Inner();
  ```

- static定义的内部类：

  外部类.内部类 内部类对象 = new 外部类.内部类();

  ```java
  Outer.Inner a = new Outer.Inner();
  ```

  

### 2. 下面的代码哪些地方会产生编译错误？

   ```java
class Outer {
    
    class Inner {}
    
    public static void foo() { 
        new Inner(); 
    }
    
    public void bar() { 
        new Inner();
    }
    
    public static void main(String[] args) {
        new Inner();
    }
    
}
   ```

- 非静态内部类对象的创建要依赖于外部类对象

- 静态方法中没有this，也就是没有所谓外部类对象，因此无法创建类对象，如果要在静态方法中创建内部类对象，可以这样做

  ```java
  new Outer().new Inner;
  ```

  

