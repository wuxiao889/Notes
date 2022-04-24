## ==

**==比较的是变量(栈)内存中存放的对象的(堆)内存地址，用来判断两个对象的地址是否相同，即是否是指相同一个对象。比较的是真正意义上的指针操作。**

1. 比较的是操作符两端的操作数是否是同一个对象。

2. 两边的操作数必须是同一类型的（可以是父子类之间）才能编译通过。

3. 比较的是地址，如果是具体的阿拉伯数字的比较，值相等则为true。如：`int a=10`与`long b=10L`与`double c=10.0`都是相同的（为true），因为他们都指向地址为10的堆。
```java
public static void main(String[] args) {
    Integer i2 = 10;
    Integer i3 = 10;
    System.out.println(i2 == i3); // true
    Integer i4 = 128;
    Integer i5 = 128;
    System.out.println(i4 == i5); // false
}
```
## equals

**equals用来比较的是两个对象的内容是否相等，由于所有的类都是继承自`java.lang.Object`类的，所以适用于所有对象，如果没有对该方法进行覆盖的话，调用的仍然是Object类中的方法，而Object中的equals方法返回的却是==的判断。**

equals方法最初是在所有类的基类Object中进行定义的，源码是：

```java
public boolean equals(Object obj) {
    return (this == obj);
}
```

由equals的源码可以看出这里定义的equals与==是等效的（Object类中的equals没什么区别），不同的原因就在于有些类（像**String、Integer**等类）对**equals进行了重写**，但是没有对equals进行重写的类（比如我们自己写的类）就只能从Object类中继承equals方法，其equals方法与==就也是等效的，除非我们在此类中重写equals。

String类对equals的重写如下：

```csharp
public boolean equals(Object anObject) {
    if (this == anObject) {
        return true;
    }
    if (anObject instanceof String) {
        String anotherString = (String)anObject;
        int n = value.length;
        if (n == anotherString.value.length) {
            char v1[] = value;
            char v2[] = anotherString.value;
            int i = 0;
            while (n-- != 0) {
                if (v1[i] != v2[i])
                    return false;
                i++;
            }
            return true;
        }
    }
    return false;
}
```

