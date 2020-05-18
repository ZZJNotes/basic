

[toc]

# 深入剖析Java中的装箱和拆箱

## 1. 什么是装箱？什么是拆箱？

- **装箱：**将基本类型用它们对应的引用类型包装起来；
- **拆箱：**将包装类型转换为基本数据类型；

```Java
Integer i = 10; //装箱
int n = i; //拆箱
```

Java为每种基本数据类型都提供了对应的包装器类型：

![image-20200513230859213](C:%5CUsers%5Cheihei%5CDesktop%5CTypora%5C%E5%AD%A6%E4%B9%A0%5C%E7%8E%8B%E9%81%93%5C%E9%9D%A2%E8%AF%95%5Cimage-20200513230859213.png)



## 2. 装箱和拆箱是如何实现的

以Integer类为例：

```java
public class Main {
    public static void main(String[] args) {
         
        Integer i = 10;
        int n = i;
    }
}
```

在装箱的时候，自动调用的是Integer的`valueOf(int)`方法，而在拆箱的时候，自动调用的是Integer的`intValue()`方法，即

- **装箱**的过程是通过包装器的`valueOf()`方法
- **拆箱**过程是通过包装器的`xxxValue()`方法(xxx代表对应的基本数据类型)

## 3. 面试中的相关问题

###题目1：

```java
public class Main {
    public static void main(String[] args) {
         
        Integer i1 = 100;
        Integer i2 = 100;
        Integer i3 = 200;
        Integer i4 = 200;
         
        System.out.println(i1==i2);
        System.out.println(i3==i4);
    }
}

//true
//false
```
Integer的valueOf()方法

```java
public static Integer valueOf(int i) {
        if(i >= -128 && i <= IntegerCache.high)
            return IntegerCache.cache[i + 128];
        else
            return new Integer(i);
    }
```

其中IntegerCache类的实现为：

```java
private static class IntegerCache {
        static final int high;
        static final Integer cache[];

        static {
            final int low = -128;

            // high value may be configured by property
            int h = 127;
            if (integerCacheHighPropValue != null) {
                // Use Long.decode here to avoid invoking methods that
                // require Integer's autoboxing cache to be initialized
                int i = Long.decode(integerCacheHighPropValue).intValue();
                i = Math.max(i, 127);
                // Maximum array size is Integer.MAX_VALUE
                h = Math.min(i, Integer.MAX_VALUE - -low);
            }
            high = h;

            cache = new Integer[(high - low) + 1];
            int j = low;
            for(int k = 0; k < cache.length; k++)
                cache[k] = new Integer(j++);
        }

        private IntegerCache() {}
    }

```



在通过valueOf方法创建Integer对象的时候，如果数值在[-128,127]之间，便返回指向IntegerCache.cache中已经存在的对象的引用；否则创建一个新的Integer对象。

上面的代码中i1和i2的数值为100，因此会直接从cache中取已经存在的对象，所以i1和i2指向的是同一个对象，而i3和i4则是分别指向不同的对象。





###题目2：

```java
public class Main {
    public static void main(String[] args) {
         
        Double i1 = 100.0;
        Double i2 = 100.0;
        Double i3 = 200.0;
        Double i4 = 200.0;
         
        System.out.println(i1==i2);
        System.out.println(i3==i4);
    }
}

//false
//false
```
Double类的valueOf方法会采用与Integer类的valueOf方法不同的实现。很简单：在某个范围内的整型数值的个数是有限的，而浮点数却不是。

Integer、Short、Byte、Character、Long这几个类的valueOf方法的实现是类似的。

Double、Float的valueOf方法的实现是类似的。

###题目3：

```java
public class Main {
    public static void main(String[] args) {
         
        Boolean i1 = false;
        Boolean i2 = false;
        Boolean i3 = true;
        Boolean i4 = true;
         
        System.out.println(i1==i2);
        System.out.println(i3==i4);
    }
}

//true
//true
```
Boolean的valueOf方法的具体实现：

```java
public static Boolean valueOf(boolean b) {
        return (b ? TRUE : FALSE);
    }
```



其中TRUE和FALSE是什么呢？在Boolean中定义了2个静态成员属性：

```java
public static final Boolean TRUE = new Boolean(true);

    /** 
     * The <code>Boolean</code> object corresponding to the primitive 
     * value <code>false</code>. 
     */
    public static final Boolean FALSE = new Boolean(false);
```



###题目4：

谈谈`Integer i = new Integer(xxx)`和`Integer i =xxx;`这两种方式的区别。

- 第一种方式不会触发自动装箱的过程；而第二种方式会触发；
- 在执行效率和资源占用上的区别。第二种方式的执行效率和资源占用在一般性情况下要优于第一种情况（注意这并不是绝对的）



###题目5：

```java
public class Main {
    public static void main(String[] args) {
         
        Integer a = 1;
        Integer b = 2;
        Integer c = 3;
        Integer d = 3;
        Integer e = 321;
        Integer f = 321;
        Long g = 3L;
        Long h = 2L;
         
        System.out.println(c==d);
        System.out.println(e==f);
        System.out.println(c==(a+b));
        System.out.println(c.equals(a+b));
        System.out.println(g==(a+b));
        System.out.println(g.equals(a+b));
        System.out.println(g.equals(a+h));
    }
}

true
false
true
true
true
false
true
```

当 "=="运算符的两个操作数都是 包装器类型的引用，则是比较指向的是否是同一个对象，而如果其中有一个操作数是表达式（即包含算术运算）则比较的是数值（即会触发自动拆箱的过程）。另外，对于包装器类型，equals方法并不会进行类型转换。

　第一个和第二个输出结果没有什么疑问。第三句由于 a+b包含了算术运算，因此会触发自动拆箱过程（会调用intValue方法），因此它们比较的是数值是否相等。而对于c.equals(a+b)会先触发自动拆箱过程，再触发自动装箱过程，也就是说a+b，会先各自调用intValue方法，得到了加法运算后的数值之后，便调用Integer.valueOf方法，再进行equals比较。同理对于后面的也是这样，不过要注意倒数第二个和最后一个输出的结果（如果数值是int类型的，装箱过程调用的是Integer.valueOf；如果是long类型的，装箱调用的Long.valueOf方法）。

如果对上面的具体执行过程有疑问，可以尝试获取反编译的字节码内容进行查看。