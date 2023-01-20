# 一、java基础概念

## 1.1、字符集

演化历史(中国版)

1. ASCII：英文字符集  七位

2. IOS8859-1： 西欧字符集  八位

3. GB2312： 简体中文字符集  最多使用两个字节编码（中文：2个字节）

4. GBK：GB2312的升级，加入了繁体字 最多使用两个字节编码

5. Unicode：国际通用字符集，融合了目前人类使用的所有字符。为每个字符分配唯一的字符码。

   底层计算时候，按照码进行计算（jvm中全部转换为unicode）

   推出了UTF标准：

   三种编码方案：  UTF-8，UTF-16,UTF-32 

   - UTF-8：一个到六个字节
   - UTF-16：2个或者四个字节
   - UTF-32：四个字节

## 1.2、char

1. 字符用单引号''定义
2. 只能保存一个字符
3. 不可以表达null（char a = ''编译出错）
4. 转义字符（\ 会把之后的字母转换为特殊含义）

## 1.3、基本类型转换

1.  类型级别：(从低到高的)
    byte-->short-->char-->int--->long--->float--->double
2. 当一个表达式中有多种数据类型的时候，类型都转换为当前表达式中级别最高的类型进行计算。
3. 在进行赋值的时候：
   左=右  :   直接赋值
   左<右  ：强转
   左>右  ：直接自动转换

## 1.4、this

代指当前对象

## 1.5、类的组成

对象头：

1. 标记字：标记运行时信息，**待补充**
2. 类指针（ClassMetadataAddressClassWord）：指向生成该对象所在的类
3. 数组长度

![image-20220517135007513](../../images/image-20220517135007513.png)

### 1.5.1、类的组成：

类的组成：属性，方法，构造器，代码块（普通块，静态块，构造块，同步块），内部类

代码块：

1. 普通块：就是方法体
2. 构造块：每新建对象，就会执行一次
3. 静态块：类初始化的时候执行，只会执行一次
4. 构造块+synchronized
5. 创建对象执行顺序
   - 父类静态代码块，静态属性（同一级别间按照定义顺序执行）
   - 子类静态代码块，静态属性（同一级别间按照定义顺序执行）
   - 父类普通代码块，属性（同一级别间按照定义顺序执行）
   - 父类构造函数
   - 子类普通代码块，属性（同一级别间按照定义顺序执行）
   - 子类构造函数
   - 注：如果子类已经重写父类，那么新建子类对象的时候父类会执行子类重写方法

内部类：

1. 静态内部类

2. 成员内部类 ，可以有final static 属性(属性不能是方法），但是绝不能有静态方法

3. 局部内部类（位置：方法内，块内，构造器内）

4. 匿名内部类 ：继承一个父类或者实现一个接口的方式直接定义并使用的类

   ```java
   public abstract class Worker {
       private String name;
   
       public String getName() {
           return name;
       }
   
       public void setName(String name) {
           this.name = name;
       }
       public abstract int workTime();
   
   }
   public class Test{
       public void test(Worker worker){
           System.out.println(worker.getName()+"工作时间："+worker.workTime());
       }
   
       public static void main(String[] args) {
           Test test = new Test();
           //在方法中定义并使用匿名内部类
           test.test(new Worker() {
               @Override
               public int workTime() {
                   return 8;
               }
               public String getName(){
                   return "alex";
               }
           });
       }
   }
   ```

## 1.6、包

在Java中的导包没有包含和被包含的关系：

包可以包含类，但是不可以包含包 

导入的类是两个东西

<img src="../../images/image-20220401135034663.png" alt="image-20220401135034663" style="zoom:50%;" />

## 1.7、类之间的关系

1. 继承
2. 实现：类实现接口
3. 依赖：让类B作为参数被类A在某个method方法中使用
4. 关联：三者用法一样，都是某个类作为另一个类的属性：两者平等
5. 聚合：has-a，整体与部分的关系，即has-a的关系
6. 组合：体现的是一种contains-a的关系

## 1.8、向上转型，向下转型

Father f = new Father（）；

Child c = new Child ();

f = c

向上转型：此时父类在编译期无法访问子类特有的属性和方法

向下转型：父类转化为子类

## 1.9、抽象类

在抽象类中定义抽象方法，目的是为了为子类提供一个通用的模板

（1）抽象类不能创建对象，那么抽象类中是否有构造器？ 
抽象类中一定有构造器。构造器的作用  给子类初始化对象的时候要先super调用父类的构造器。

（2）抽象类是否可以被final修饰？
不能被final修饰，因为抽象类设计的初衷就是给子类继承用的。要是被final修饰了这个抽象类了，就不存在继承了，就没有子类。

## 2.0、接口

单继承，多实现

### 2.1.1、1.8之前

（1）常量：固定修饰符：public static final
（2）抽象方法：固定修饰符：public abstract 

## 2.1、异常

多重异常只会捕获第一个，之后的不会再捕获

throw声明异常，throws抛出异常，表示该方法不抛出异常

![image-20220403230418169](../../images/image-20220403230418169.png)

## 2.2、常用类

### 2.2.1、时间相关

1. java.util.date 表示  相对于1970年1月1号，经过n毫秒后的日期，如果参数为0（不是null）则时间为1970年1月1号

2. java.sql.date 只有年月日，用于数据库

3. SimpleDateFormat：parse，用于将string转化为date对象，format，用于将date转化为string

4. Calendar(抽象类）：Calendar.getInstance()或者new GregorianCalendar（），包含了日期中需要的各种属性，可以通过Calendar.get(Calendar.xxx)得到（除此外Calendar还有各种其他的getXXX属性））

   set方法可以更改日期

### 2.2.2、第三期日期相关

#### 2.2.2.1、LocalDate，LocalTime，LocalDateTime

LocalDate localDate = LocalDate.now();

LocalDate of = LocalDate.of(2010, 5, 6);

没有set方法，因为其不可变，有with

有加减操作

 LocalDateTime localDateTime1 = localDateTime.plusMonths(4);
 LocalDateTime localDateTime3 = localDateTime.minusMonths(5);

#### 2.2.2.2、DateTimeFormatter 

DateTimeFormatter df2 = DateTimeFormatter.ofLocalizedDateTime(FormatStyle.SHORT);

DateTimeFormatter df3 = DateTimeFormatter.ofPattern("yyyy-MM-dd hh:mm:ss");

df2.format、parse

![image-20220406154633239](../../images/image-20220406154633239.png)

## 2.3、IO流

1. 路径分隔符，winfows是"\\",linux是"/",所以用File.separator
2. mkdir(创建单级目录）,mkdirs(创建多级目录)
3. list，listfiles

![image-20220406223403016](../../images/image-20220406223403016.png)

## 2.4、测试

1. @Test加在方法上即可
2. @Before，@After

## 2.5、注解

1. @interface 定义注解

   ```java
   public @interface MyAnnotation{
     Object value() default = "aaa"
   }
   ```

2. 属性

   类型Object可以是8种类基本数据类型、string、枚举、注解、数组类型

   value()是属性名字，必须加()

3. 赋值

   如果注解没有默认值default的话，要赋值参数

   格式为 name = 。。。。

   属性名字是value，value= 可以不写

4. 元注解

   - @Retention

   ```java
   Retentionpolicy.SOURCE :.java 源文件中有效
   Retentionpolicy.CLASS（默认） : .java、.class文件中有效
   Retentionpolicy.RUNTIME : .java、.class、jvm中有效 
   ```

   - @Target

   ```java
   ElementType.TYPE：允许被修饰的注解作用在类、接口和枚举上
   ElementType.FIELD：允许作用在属性字段上
   ElementType.METHOD：允许作用在方法上
   ElementType.PARAMETER：允许作用在方法参数上
   ElementType.CONSTRUCTOR：允许作用在构造器上
   ElementType.LOCAL_VARIABLE：允许作用在本地局部变量上
   ElementType.ANNOTATION_TYPE：允许作用在注解上
   ElementType.PACKAGE：允许作用在包上
   ```

   - @Document

   ```java
   生成javadoc的时候会把该注解注释的注解写入document里面
   ```

   - @Inherited

   ```java
   使用@Inherited声明出来的注解，只有在类上使用才会有效，对方法和属性等其他无效。
   子类会自动继承注解
   ```

## 2.6、反射

反射机制可以操作字节码文件（可以读和修改字节码文件。）

```
相关的类在
java.lang.reflect.*;
```

1. 得到类信息方式

   - 对象.getClass() 
   - 任何类型.class;
   - Class.forName("完整包名+类名")，"Javase.reflectBean.User"
   - ClassLoader 

2. 可以作为类的实例

   ```
   类（内部，外部）
   接口
   注解
   数组
   基本数据类型
   void
   
   数组同一维度，同一元素类型的字节码是一个
   int arr1 = {1,2,3}
   int arr2 = {2,3,4}
   arr1.getClass = arr2.getClass
   ```

3. 常用方法

   ```java
   CLASS 方法：
   ///newInstance()方法内部实际上调用了无参数构造方法，必须保证无参构造存在才可以。
   class.newInstance()
   class.getName()//返回完整类名带包名
   class.getSimpleName()//返回类名
   class.getFields()//返回类中public修饰的属性 
   class.getDeclaredFields()//返回类中所有的属性  
   class.getDeclaredField(String name)//根据属性名name获取指定的属性  
   class.getModifiers()//获取属性的修饰符列表,返回的修饰符是一个数字，每个数字是修饰符的代号【一般配合Modifier类的toString(int x)方法使用】 
   class.getDeclaredMethods()  
   class.getDeclaredMethod(String name, Class<?>… parameterTypes) 
   class.getDeclaredConstructors()  
   class.getSuperclass()//返回调用类的父类
   class.getInterfaces()//返回调用类实现的接口集合
     
     
   Field方法：
   f.getName()
   f.getModifiers()
   f.getType()
   f.set(对象obj， 值value)
   f.get(对象obj)
   f.setAccessible(boolean) ///可以操作私有属性
     
   Method方法：
   m.getName()
   m.getModifiers()  ///一般配合Modifier.toString(int x)
   m.getReturnType()  ///一般配合Class类的getSimpleName()方法使用
   m.getParameterTypes() ////一般配合Class类的getSimpleName()方法使用
   m.invoke(Object obj, Object… args))  ////方法.invoke(对象, 实参);
   
   construct不介绍了
   ```


## 2.7、lambda

<u>**效率低下，比正常的方法调用慢了几十倍**</u>

1. 原理

   匿名内部类本质是**编译**时生成内部类

   lambda表达式是运行时生成类，类中重写调用lambda的方法，新增方法（内容是lambda）

   前提是必须有一个函数式接口----》有且只有**一个**抽象方法的接口，一般有@FunctionnaInterface注解，否则无法映射

2. 接口增强

   - 1.8之前只能有静态常量和抽象方法

   - 1.8之后可以存在默认方法和静态方法（否则不利于接口扩展，比如一个接口有几百个实现类，修改接口后要修改几百个地方）
   - 默认方法不强制重新给，但是可以重写
   - 静态方法不可以重写，并且只能通过. **接口类**.class调用，实现类或对象不能调用

   ```
   修饰符 default 返回值类型 方法名{
   
   }
   
   修饰符 static 返回值类型 方法名{
   
   }
   ```

3. 常用的函数式接口（jdk已经提供了大量的函数式接口，几乎可以满足一切要求，不需要我们再定义）

   ```java
   无参数有返回值 Supplier<Object> supplier
   有参，无返回值 Consumer<T> consumer
   有参，有返回值 Function<t，r> function
   有参，boolean返回值 Predicate<T> predicate
   ```

4. 语法格式

   ```java
   除了::（方法引用）符号外，其余语法不介绍
   对象名::普通方法名
   类名::普通方法名&&静态方法&& new 构造器
   数组::构造器
   ```

## 2.8、stream

早就会了，不介绍了。

https://blog.csdn.net/mu_wind/article/details/109516995

