~~~java
ClassFile {
    u4             magic; //Class 文件的标志 魔数
    u2             minor_version;//Class 的小版本号
    u2             major_version;//Class 的大版本号
    u2             constant_pool_count;//常量池的数量
    cp_info        constant_pool[constant_pool_count-1];//常量池
    u2             access_flags;//Class 的访问标记
    u2             this_class;//当前类
    u2             super_class;//父类
    u2             interfaces_count;//接口
    u2             interfaces[interfaces_count];//一个类可以实现多个接口
    u2             fields_count;//Class 文件的字段属性
    field_info     fields[fields_count];//一个类会可以有多个字段
    u2             methods_count;//Class 文件的方法数量
    method_info    methods[methods_count];//一个类可以有个多个方法
    u2             attributes_count;//此类的属性表中的属性数
    attribute_info attributes[attributes_count];//属性表集合
}
~~~

### 1.魔数

每个Class文件的头四个字节被称为魔数，它的唯一作用就是确定这个文件是否是一个能被虚拟机接收的Class文件，程序设计者很多时候都喜欢用一些特殊的数字或单词来表示固定的文件类型后者其他特殊含义

### 2.Class文件版本号

紧接着四个字节是版本号，其中开始是2个字节的次版本号，然后是2个字节的主版本号，版本号的作用是：高版本的虚拟机兼容低版本的编译器生成的字节码文件，但是低版本的虚拟机是不能执行高版本的字节码文件的

### 3.常量池

紧接着主次版本号的是常量池，常量池计数是从1开始的，常量池中主要存放两大常量：字面量和符号引用，字面量比如文本字符串，声明为final的常量值等。而符号引用则属于编译原理方面的内容，包括下面三种：

* 类和接口的全限定名
* 字段的名称和描述符
* 方法的名称和描述符

###  4.访问标志

在常量池结束以后，紧跟着两个字节代表访问标志，这个标志用于识别一些类或者接口层次的访问信息，比如这个class文件对应的是类还是接口，是否为public或者abstract，如果是类的话是否声明为final

### 5.当前类，父类，接口索引集合

类索引用于确定这个类的全限定名，父类索引用于确定这个类的父类的全限定名，由于java是单继承的，所以父类索引只有一个，除了object类以外，其他所有类都默认继承object，因此除了object类以外，所有java类的父类索引都不为0

接口索引集合用来描述这个类实现了哪些接口，由于类可以实现多个接口，所以接口索引是一个集合

### 6.字段表集合

字段表用于描述接口或类中声明的变量，字段包括类级变量和实例变量，但不包括定义在方法内部的局部变量

### 7.方法表集合

有方法的数量和方法表两个结构，这个方法表结构类似于字段表，都有访问标识，名称索引，描述符索引，属性表集合等这几项

### 8.属性表集合

在Class文件，字段表，方法表中都可以携带自己的属性表，以用来描述某些场景特有的信息

