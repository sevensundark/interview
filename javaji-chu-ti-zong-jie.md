转载：[java面试题](http://blog.csdn.net/jackfrued/article/details/44921941)

1、面向对象的特征有哪些方面？

答：面向对象的特征主要有以下几个方面：

* 抽象：抽象是将一类对象的共同特征总结出来构造类的过程，包括数据抽象和行为抽象两方面。抽象只关注对象有哪些属性和行为，并不关注这些行为的细节是什么。

* 继承：继承是从已有类得到继承信息创建新类的过程。提供继承信息的类被称为父类（超类、基类）；得到继承信息的类被称为子类（派生类）。继承让变化中的软件系统有了一定的延续性，同时继承也是封装程序中可变因素的重要手段（如果不能理解请阅读阎宏博士的《Java与模式》或《设计模式精解》中关于桥梁模式的部分）。

* 封装：通常认为封装是把数据和操作数据的方法绑定起来，对数据的访问只能通过已定义的接口。面向对象的本质就是将现实世界描绘成一系列完全自治、封闭的对象。我们在类中编写的方法就是对实现细节的一种封装；我们编写一个类就是对数据和数据操作的封装。可以说，封装就是隐藏一切可隐藏的东西，只向外界提供最简单的编程接口（可以想想普通洗衣机和全自动洗衣机的差别，明显全自动洗衣机封装更好因此操作起来更简单；我们现在使用的智能手机也是封装得足够好的，因为几个按键就搞定了所有的事情）。

* 多态性：多态性是指允许不同子类型的对象对同一消息作出不同的响应。简单的说就是用同样的对象引用调用同样的方法但是做了不同的事情。多态性分为编译时的多态性和运行时的多态性。如果将对象的方法视为对象向外界提供的服务，那么运行时的多态性可以解释为：当A系统访问B系统提供的服务时，B系统有多种提供服务的方式，但一切对A系统来说都是透明的（就像电动剃须刀是A系统，它的供电系统是B系统，B系统可以使用电池供电或者用交流电，甚至还有可能是太阳能，A系统只会通过B类对象调用供电的方法，但并不知道供电系统的底层实现是什么，究竟通过何种方式获得了动力）。方法重载（overload）实现的是编译时的多态性（也称为前绑定），而方法重写（override）实现的是运行时的多态性（也称为后绑定）。运行时的多态是面向对象最精髓的东西，要实现多态需要做两件事：1\). 方法重写（子类继承父类并重写父类中已有的或抽象的方法）；2\). 对象造型（用父类型引用引用子类型对象，这样同样的引用调用同样的方法就会根据子类对象的不同而表现出不同的行为）。

2、访问修饰符public,private,protected,以及不写（默认）时的区别？

答：

修饰符 当前类 同 包 子 类 其他包

public  √   √   √   √

protected   √   √   √   ×

default √   √   ×   ×

private √   ×   ×   ×

类的成员不写访问修饰时默认为default。默认对于同一个包中的其他类相当于公开（public），对于不是同一个包中的其他类相当于私有（private）。受保护（protected）对子类相当于公开，对不是同一包中的没有父子关系的类相当于私有。Java中，外部类的修饰符只能是public或默认，类的成员（包括内部类）的修饰符可以是以上四种。

3、String 是最基本的数据类型吗？

答：不是。Java中的基本数据类型只有8个：byte、short、int、long、float、double、char、boolean；除了基本类型（primitive type），剩下的都是引用类型（reference type），Java 5以后引入的枚举类型也算是一种比较特殊的引用类型。

4、float f=3.4;是否正确？

答:不正确。3.4是双精度数，将双精度型（double）赋值给浮点型（float）属于下转型（down-casting，也称为窄化）会造成精度损失，因此需要强制类型转换float f =\(float\)3.4; 或者写成float f =3.4F;。

5、short s1 = 1; s1 = s1 + 1;有错吗?short s1 = 1; s1 += 1;有错吗？

答：对于short s1 = 1; s1 = s1 + 1;由于1是int类型，因此s1+1运算结果也是int 型，需要强制转换类型才能赋值给short型。而short s1 = 1; s1 += 1;可以正确编译，因为s1+= 1;相当于s1 = \(short\)\(s1 + 1\);其中有隐含的强制类型转换。

6、Java有没有goto？

答：goto 是Java中的保留字，在目前版本的Java中没有使用。（根据James Gosling（Java之父）编写的《The Java Programming Language》一书的附录中给出了一个Java关键字列表，其中有goto和const，但是这两个是目前无法使用的关键字，因此有些地方将其称之为保留字，其实保留字这个词应该有更广泛的意义，因为熟悉C语言的程序员都知道，在系统类库中使用过的有特殊意义的单词或单词的组合都被视为保留字）

7、int和Integer有什么区别？

答：Java是一个近乎纯洁的面向对象编程语言，但是为了编程的方便还是引入了基本数据类型，但是为了能够将这些基本数据类型当成对象操作，Java为每一个基本数据类型都引入了对应的包装类型（wrapper class），int的包装类就是Integer，从Java 5开始引入了自动装箱/拆箱机制，使得二者可以相互转换。

Java 为每个原始类型提供了包装类型：

* 原始类型: boolean，char，byte，short，int，long，float，double

* 包装类型：Boolean，Character，Byte，Short，Integer，Long，Float，Double

class AutoUnboxingTest {

```
public static void main\(String\[\] args\) {

    Integer a = new Integer\(3\);

    Integer b = 3;                  // 将3自动装箱成Integer类型

    int c = 3;

    System.out.println\(a == b\);     // false 两个引用没有引用同一对象

    System.out.println\(a == c\);     // true a自动拆箱成int类型再和c比较

}
```

}

最近还遇到一个面试题，也是和自动装箱和拆箱有点关系的，代码如下所示：

public class Test03 {

```
public static void main\(String\[\] args\) {

    Integer f1 = 100, f2 = 100, f3 = 150, f4 = 150;



    System.out.println\(f1 == f2\);

    System.out.println\(f3 == f4\);

}
```

}

如果不明就里很容易认为两个输出要么都是true要么都是false。首先需要注意的是f1、f2、f3、f4四个变量都是Integer对象引用，所以下面的==运算比较的不是值而是引用。装箱的本质是什么呢？当我们给一个Integer对象赋一个int值的时候，会调用Integer类的静态方法valueOf，如果看看valueOf的源代码就知道发生了什么。

```
public static Integer valueOf\(int i\) {

    if \(i &gt;= IntegerCache.low && i &lt;= IntegerCache.high\)

        return IntegerCache.cache\[i + \(-IntegerCache.low\)\];

    return new Integer\(i\);

}
```

IntegerCache是Integer的内部类，其代码如下所示：

/\*\*

```
 \* Cache to support the object identity semantics of autoboxing for values between

 \* -128 and 127 \(inclusive\) as required by JLS.

 \*

 \* The cache is initialized on first usage.  The size of the cache

 \* may be controlled by the {@code -XX:AutoBoxCacheMax=&lt;size&gt;} option.

 \* During VM initialization, java.lang.Integer.IntegerCache.high property

 \* may be set and saved in the private system properties in the

 \* sun.misc.VM class.

 \*/



private static class IntegerCache {

    static final int low = -128;

    static final int high;

    static final Integer cache\[\];



    static {

        // high value may be configured by property

        int h = 127;

        String integerCacheHighPropValue =

            sun.misc.VM.getSavedProperty\("java.lang.Integer.IntegerCache.high"\);

        if \(integerCacheHighPropValue != null\) {

            try {

                int i = parseInt\(integerCacheHighPropValue\);

                i = Math.max\(i, 127\);

                // Maximum array size is Integer.MAX\_VALUE

                h = Math.min\(i, Integer.MAX\_VALUE - \(-low\) -1\);

            } catch\( NumberFormatException nfe\) {

                // If the property cannot be parsed into an int, ignore it.

            }

        }

        high = h;



        cache = new Integer\[\(high - low\) + 1\];

        int j = low;

        for\(int k = 0; k &lt; cache.length; k++\)

            cache\[k\] = new Integer\(j++\);



        // range \[-128, 127\] must be interned \(JLS7 5.1.7\)

        assert IntegerCache.high &gt;= 127;

    }



    private IntegerCache\(\) {}

}
```

简单的说，如果整型字面量的值在-128到127之间，那么不会new新的Integer对象，而是直接引用常量池中的Integer对象，所以上面的面试题中f1==f2的结果是true，而f3==f4的结果是false。

提醒：越是貌似简单的面试题其中的玄机就越多，需要面试者有相当深厚的功力。

9、解释内存中的栈\(stack\)、堆\(heap\)和方法区\(method area\)的用法。

答：通常我们定义一个基本数据类型的变量，一个对象的引用，还有就是函数调用的现场保存都使用JVM中的栈空间；而通过new关键字和构造器创建的对象则放在堆空间，堆是垃圾收集器管理的主要区域，由于现在的垃圾收集器都采用分代收集算法，所以堆空间还可以细分为新生代和老生代，再具体一点可以分为Eden、Survivor（又可分为From Survivor和To Survivor）、Tenured；方法区和堆都是各个线程共享的内存区域，用于存储已经被JVM加载的类信息、常量、静态变量、JIT编译器编译后的代码等数据；程序中的字面量（literal）如直接书写的100、"hello"和常量都是放在常量池中，常量池是方法区的一部分，。栈空间操作起来最快但是栈很小，通常大量的对象都是放在堆空间，栈和堆的大小都可以通过JVM的启动参数来进行调整，栈空间用光了会引发StackOverflowError，而堆和常量池空间不足则会引发OutOfMemoryError。

String str = new String\("hello"\);

1

上面的语句中变量str放在栈上，用new创建出来的字符串对象放在堆上，而"hello"这个字面量是放在方法区的。

补充1：较新版本的Java（从Java 6的某个更新开始）中，由于JIT编译器的发展和"逃逸分析"技术的逐渐成熟，栈上分配、标量替换等优化技术使得对象一定分配在堆上这件事情已经变得不那么绝对了。

补充2：运行时常量池相当于Class文件常量池具有动态性，Java语言并不要求常量一定只有编译期间才能产生，运行期间也可以将新的常量放入池中，String类的intern\(\)方法就是这样的。

看看下面代码的执行结果是什么并且比较一下Java 7以前和以后的运行结果是否一致。

String s1 = new StringBuilder\("go"\)

```
.append\("od"\).toString\(\);
```

System.out.println\(s1.intern\(\) == s1\);

String s2 = new StringBuilder\("ja"\)

```
.append\("va"\).toString\(\);
```

System.out.println\(s2.intern\(\) == s2\);

10、Math.round\(11.5\) 等于多少？Math.round\(-11.5\)等于多少？

答：Math.round\(11.5\)的返回值是12，Math.round\(-11.5\)的返回值是-11。四舍五入的原理是在参数上加0.5然后进行下取整。

11、switch 是否能作用在byte 上，是否能作用在long 上，是否能作用在String上？

答：在Java 5以前，switch\(expr\)中，expr只能是byte、short、char、int。从Java 5开始，Java中引入了枚举类型，expr也可以是enum类型，从Java 7开始，expr还可以是字符串（String），但是长整型（long）在目前所有的版本中都是不可以的。

12、用最有效率的方法计算2乘以8？

答： 2 &lt;&lt; 3（左移3位相当于乘以2的3次方，右移3位相当于除以2的3次方）。

补充：我们为编写的类重写hashCode方法时，可能会看到如下所示的代码，其实我们不太理解为什么要使用这样的乘法运算来产生哈希码（散列码），而且为什么这个数是个素数，为什么通常选择31这个数？前两个问题的答案你可以自己百度一下，选择31是因为可以用移位和减法运算来代替乘法，从而得到更好的性能。说到这里你可能已经想到了：31 \* num 等价于\(num &lt;&lt; 5\) - num，左移5位相当于乘以2的5次方再减去自身就相当于乘以31，现在的VM都能自动完成这个优化。

public class PhoneNumber {

```
private int areaCode;

private String prefix;

private String lineNumber;



@Override

public int hashCode\(\) {

    final int prime = 31;

    int result = 1;

    result = prime \* result + areaCode;

    result = prime \* result

            + \(\(lineNumber == null\) ? 0 : lineNumber.hashCode\(\)\);

    result = prime \* result + \(\(prefix == null\) ? 0 : prefix.hashCode\(\)\);

    return result;

}



@Override

public boolean equals\(Object obj\) {

    if \(this == obj\)

        return true;

    if \(obj == null\)

        return false;

    if \(getClass\(\) != obj.getClass\(\)\)

        return false;

    PhoneNumber other = \(PhoneNumber\) obj;

    if \(areaCode != other.areaCode\)

        return false;

    if \(lineNumber == null\) {

        if \(other.lineNumber != null\)

            return false;

    } else if \(!lineNumber.equals\(other.lineNumber\)\)

        return false;

    if \(prefix == null\) {

        if \(other.prefix != null\)

            return false;

    } else if \(!prefix.equals\(other.prefix\)\)

        return false;

    return true;

}
```

}

13、数组有没有length\(\)方法？String有没有length\(\)方法？

答：数组没有length\(\)方法，有length 的属性。String 有length\(\)方法。JavaScript中，获得字符串的长度是通过length属性得到的，这一点容易和Java混淆。

14、在Java中，如何跳出当前的多重嵌套循环？

答：在最外层循环前加一个标记如A，然后用break A;可以跳出多重循环。（Java中支持带标签的break和continue语句，作用有点类似于C和C++中的goto语句，但是就像要避免使用goto一样，应该避免使用带标签的break和continue，因为它不会让你的程序变得更优雅，很多时候甚至有相反的作用，所以这种语法其实不知道更好）

15、构造器（constructor）是否可被重写（override）？

答：构造器不能被继承，因此不能被重写，但可以被重载。

16、两个对象值相同\(x.equals\(y\) == true\)，但却可有不同的hash code，这句话对不对？

答：不对，如果两个对象x和y满足x.equals\(y\) == true，它们的哈希码（hash code）应当相同。Java对于eqauls方法和hashCode方法是这样规定的：\(1\)如果两个对象相同（equals方法返回true），那么它们的hashCode值一定要相同；\(2\)如果两个对象的hashCode相同，它们并不一定相同。当然，你未必要按照要求去做，但是如果你违背了上述原则就会发现在使用容器时，相同的对象可以出现在Set集合中，同时增加新元素的效率会大大下降（对于使用哈希存储的系统，如果哈希码频繁的冲突将会造成存取性能急剧下降）。

补充：关于equals和hashCode方法，很多Java程序都知道，但很多人也就是仅仅知道而已，在Joshua Bloch的大作《Effective Java》（很多软件公司，《Effective Java》、《Java编程思想》以及《重构：改善既有代码质量》是Java程序员必看书籍，如果你还没看过，那就赶紧去亚马逊买一本吧）中是这样介绍equals方法的：首先equals方法必须满足自反性（x.equals\(x\)必须返回true）、对称性（x.equals\(y\)返回true时，y.equals\(x\)也必须返回true）、传递性（x.equals\(y\)和y.equals\(z\)都返回true时，x.equals\(z\)也必须返回true）和一致性（当x和y引用的对象信息没有被修改时，多次调用x.equals\(y\)应该得到同样的返回值），而且对于任何非null值的引用x，x.equals\(null\)必须返回false。实现高质量的equals方法的诀窍包括：1. 使用==操作符检查"参数是否为这个对象的引用"；2. 使用instanceof操作符检查"参数是否为正确的类型"；3. 对于类中的关键属性，检查参数传入对象的属性是否与之相匹配；4. 编写完equals方法后，问自己它是否满足对称性、传递性、一致性；5. 重写equals时总是要重写hashCode；6. 不要将equals方法参数中的Object对象替换为其他的类型，在重写时不要忘掉@Override注解。

17、是否可以继承String类？

答：String 类是final类，不可以被继承。

补充：继承String本身就是一个错误的行为，对String类型最好的重用方式是关联关系（Has-A）和依赖关系（Use-A）而不是继承关系（Is-A）。

18、当一个对象被当作参数传递到一个方法后，此方法可改变这个对象的属性，并可返回变化后的结果，那么这里到底是值传递还是引用传递？

答：是值传递。Java语言的方法调用只支持参数的值传递。当一个对象实例作为一个参数被传递到方法中时，参数的值就是对该对象的引用。对象的属性可以在被调用过程中被改变，但对对象引用的改变是不会影响到调用者的。C++和C\#中可以通过传引用或传输出参数来改变传入的参数的值。在C\#中可以编写如下所示的代码，但是在Java中却做不到。

using System;

namespace CS01 {

```
class Program {

    public static void swap\(ref int x, ref int y\) {

        int temp = x;

        x = y;

        y = temp;

    }



    public static void Main \(string\[\] args\) {

        int a = 5, b = 10;

        swap \(ref a, ref b\);

        // a = 10, b = 5;

        Console.WriteLine \("a = {0}, b = {1}", a, b\);

    }

}
```

}

说明：Java中没有传引用实在是非常的不方便，这一点在Java 8中仍然没有得到改进，正是如此在Java编写的代码中才会出现大量的Wrapper类（将需要通过方法调用修改的引用置于一个Wrapper类中，再将Wrapper对象传入方法），这样的做法只会让代码变得臃肿，尤其是让从C和C++转型为Java程序员的开发者无法容忍。

19、String和StringBuilder、StringBuffer的区别？

答：Java平台提供了两种类型的字符串：String和StringBuffer/StringBuilder，它们可以储存和操作字符串。其中String是只读字符串，也就意味着String引用的字符串内容是不能被改变的。而StringBuffer/StringBuilder类表示的字符串对象可以直接进行修改。StringBuilder是Java 5中引入的，它和StringBuffer的方法完全相同，区别在于它是在单线程环境下使用的，因为它的所有方面都没有被synchronized修饰，因此它的效率也比StringBuffer要高。

面试题1 - 什么情况下用+运算符进行字符串连接比调用StringBuffer/StringBuilder对象的append方法连接字符串性能更好？

面试题2 - 请说出下面程序的输出。

class StringEqualTest {

```
public static void main\(String\[\] args\) {

    String s1 = "Programming";

    String s2 = new String\("Programming"\);

    String s3 = "Program";

    String s4 = "ming";

    String s5 = "Program" + "ming";

    String s6 = s3 + s4;

    System.out.println\(s1 == s2\);

    System.out.println\(s1 == s5\);

    System.out.println\(s1 == s6\);

    System.out.println\(s1 == s6.intern\(\)\);

    System.out.println\(s2 == s2.intern\(\)\);

}
```

}

补充：解答上面的面试题需要清除两点：1. String对象的intern方法会得到字符串对象在常量池中对应的版本的引用（如果常量池中有一个字符串与String对象的equals结果是true），如果常量池中没有对应的字符串，则该字符串将被添加到常量池中，然后返回常量池中字符串的引用；2. 字符串的+操作其本质是创建了StringBuilder对象进行append操作，然后将拼接后的StringBuilder对象用toString方法处理成String对象，这一点可以用javap -c StringEqualTest.class命令获得class文件对应的JVM字节码指令就可以看出来。

20、重载（Overload）和重写（Override）的区别。重载的方法能否根据返回类型进行区分？

答：方法的重载和重写都是实现多态的方式，区别在于前者实现的是编译时的多态性，而后者实现的是运行时的多态性。重载发生在一个类中，同名的方法如果有不同的参数列表（参数类型不同、参数个数不同或者二者都不同）则视为重载；重写发生在子类与父类之间，重写要求子类被重写方法与父类被重写方法有相同的返回类型，比父类被重写方法更好访问，不能比父类被重写方法声明更多的异常（里氏代换原则）。重载对返回类型没有特殊的要求。

面试题：华为的面试题中曾经问过这样一个问题 - "为什么不能根据返回类型来区分重载"，快说出你的答案吧！

21、描述一下JVM加载class文件的原理机制？

答：JVM中类的装载是由类加载器（ClassLoader）和它的子类来实现的，Java中的类加载器是一个重要的Java运行时系统组件，它负责在运行时查找和装入类文件中的类。

由于Java的跨平台性，经过编译的Java源程序并不是一个可执行程序，而是一个或多个类文件。当Java程序需要使用某个类时，JVM会确保这个类已经被加载、连接（验证、准备和解析）和初始化。类的加载是指把类的.class文件中的数据读入到内存中，通常是创建一个字节数组读入.class文件，然后产生与所加载类对应的Class对象。加载完成后，Class对象还不完整，所以此时的类还不可用。当类被加载后就进入连接阶段，这一阶段包括验证、准备（为静态变量分配内存并设置默认的初始值）和解析（将符号引用替换为直接引用）三个步骤。最后JVM对类进行初始化，包括：1\)如果类存在直接的父类并且这个类还没有被初始化，那么就先初始化父类；2\)如果类中存在初始化语句，就依次执行这些初始化语句。

类的加载是由类加载器完成的，类加载器包括：根加载器（BootStrap）、扩展加载器（Extension）、系统加载器（System）和用户自定义类加载器（java.lang.ClassLoader的子类）。从Java 2（JDK 1.2）开始，类加载过程采取了父亲委托机制（PDM）。PDM更好的保证了Java平台的安全性，在该机制中，JVM自带的Bootstrap是根加载器，其他的加载器都有且仅有一个父类加载器。类的加载首先请求父类加载器加载，父类加载器无能为力时才由其子类加载器自行加载。JVM不会向Java程序提供对Bootstrap的引用。下面是关于几个类加载器的说明：

Bootstrap：一般用本地代码实现，负责加载JVM基础核心类库（rt.jar）；

Extension：从java.ext.dirs系统属性所指定的目录中加载类库，它的父加载器是Bootstrap；

System：又叫应用类加载器，其父类是Extension。它是应用最广泛的类加载器。它从环境变量classpath或者系统属性java.class.path所指定的目录中记载类，是用户自定义加载器的默认父加载器。

22、char 型变量中能不能存贮一个中文汉字，为什么？

答：char类型可以存储一个中文汉字，因为Java中使用的编码是Unicode（不选择任何特定的编码，直接使用字符在字符集中的编号，这是统一的唯一方法），一个char类型占2个字节（16比特），所以放一个中文是没问题的。

补充：使用Unicode意味着字符在JVM内部和外部有不同的表现形式，在JVM内部都是Unicode，当这个字符被从JVM内部转移到外部时（例如存入文件系统中），需要进行编码转换。所以Java中有字节流和字符流，以及在字符流和字节流之间进行转换的转换流，如InputStreamReader和OutputStreamReader，这两个类是字节流和字符流之间的适配器类，承担了编码转换的任务；对于C程序员来说，要完成这样的编码转换恐怕要依赖于union（联合体/共用体）共享内存的特征来实现了。

23、抽象类（abstract class）和接口（interface）有什么异同？

答：抽象类和接口都不能够实例化，但可以定义抽象类和接口类型的引用。一个类如果继承了某个抽象类或者实现了某个接口都需要对其中的抽象方法全部进行实现，否则该类仍然需要被声明为抽象类。接口比抽象类更加抽象，因为抽象类中可以定义构造器，可以有抽象方法和具体方法，而接口中不能定义构造器而且其中的方法全部都是抽象方法。抽象类中的成员可以是private、默认、protected、public的，而接口中的成员全都是public的。抽象类中可以定义成员变量，而接口中定义的成员变量实际上都是常量。有抽象方法的类必须被声明为抽象类，而抽象类未必要有抽象方法。

24、静态嵌套类\(Static Nested Class\)和内部类（Inner Class）的不同？

答：Static Nested Class是被声明为静态（static）的内部类，它可以不依赖于外部类实例被实例化。而通常的内部类需要在外部类实例化后才能实例化，其语法看起来挺诡异的，如下所示。

/\*\*

\* 扑克类（一副扑克）

\* @author 骆昊

\*

\*/

public class Poker {

```
private static String\[\] suites = {"黑桃", "红桃", "草花", "方块"};

private static int\[\] faces = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13};



private Card\[\] cards;



/\*\*

 \* 构造器

 \* 

 \*/

public Poker\(\) {

    cards = new Card\[52\];

    for\(int i = 0; i &lt; suites.length; i++\) {

        for\(int j = 0; j &lt; faces.length; j++\) {

            cards\[i \* 13 + j\] = new Card\(suites\[i\], faces\[j\]\);

        }

    }

}



/\*\*

 \* 洗牌 （随机乱序）

 \* 

 \*/

public void shuffle\(\) {

    for\(int i = 0, len = cards.length; i &lt; len; i++\) {

        int index = \(int\) \(Math.random\(\) \* len\);

        Card temp = cards\[index\];

        cards\[index\] = cards\[i\];

        cards\[i\] = temp;

    }

}



/\*\*

 \* 发牌

 \* @param index 发牌的位置

 \* 

 \*/

public Card deal\(int index\) {

    return cards\[index\];

}



/\*\*

 \* 卡片类（一张扑克）

 \* \[内部类\]

 \* @author 骆昊

 \*

 \*/

public class Card {

    private String suite;   // 花色

    private int face;       // 点数



    public Card\(String suite, int face\) {

        this.suite = suite;

        this.face = face;

    }



    @Override

    public String toString\(\) {

        String faceStr = "";

        switch\(face\) {

        case 1: faceStr = "A"; break;

        case 11: faceStr = "J"; break;

        case 12: faceStr = "Q"; break;

        case 13: faceStr = "K"; break;

        default: faceStr = String.valueOf\(face\);

        }

        return suite + faceStr;

    }

}
```

}

测试代码：

class PokerTest {

```
public static void main\(String\[\] args\) {

    Poker poker = new Poker\(\);

    poker.shuffle\(\);                // 洗牌

    Poker.Card c1 = poker.deal\(0\);  // 发第一张牌

    // 对于非静态内部类Card

    // 只有通过其外部类Poker对象才能创建Card对象

    Poker.Card c2 = poker.new Card\("红心", 1\);    // 自己创建一张牌



    System.out.println\(c1\);     // 洗牌后的第一张

    System.out.println\(c2\);     // 打印: 红心A

}
```

}

面试题 - 下面的代码哪些地方会产生编译错误？

class Outer {

```
class Inner {}



public static void foo\(\) { new Inner\(\); }



public void bar\(\) { new Inner\(\); }



public static void main\(String\[\] args\) {

    new Inner\(\);

}
```

}



注意：Java中非静态内部类对象的创建要依赖其外部类对象，上面的面试题中foo和main方法都是静态方法，静态方法中没有this，也就是说没有所谓的外部类对象，因此无法创建内部类对象，如果要在静态方法中创建内部类对象，可以这样做：

```
new Outer\(\).new Inner\(\);
```

1

