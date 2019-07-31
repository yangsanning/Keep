## String, StringBuffer, StringBuilder的区别

#### String 与 StringBuffer
+ 不同点： <br />
String 是一个常量，创建之后其内容不能更改，如果需要更改内容则会产生新的对象 <br />
StringBuffer 每次更改都是对自身对象的操作，不会重新产生新对象

+ 速度对比 
```java
* 场景一: String > StringBuffer 
    String S1 = "aa" + "bb" + "cc";
    StringBuffer Sb = new StringBuilder("aa").append("bb").append("cc");

* 场景二: StringBuffer > String 
    String S1 = "aa";
    String S2 = "bb";
    String S3 = "cc";
    String S4 = S1 + S2 + S3;
    StringBuffer Sb = new StringBuilder("aa").append("bb").append("cc");
```
实际开发中，如果字符串需要频繁更改，推荐使用 StringBuffer

-------------

#### StringBuffer 与 StringBuilder
+ 相同点： <br />
StringBuilder 与 StringBuffer 同是字符串缓冲类，都使用用于存储字符数据，内部都是维护了一个字符数组 <br />
StringBuilder 的方法与 StringBuffer 一模一样

+ 不同点： <br />
StringBuffer jdk1.0出现， StringBuilder jdk1.5出现 <br />
StringBuffer 线程安全，StringBuilder 是线程非安全 <br />
StringBuffer 操作效率低，StringBuilder ，操作效率高 <br />

+ 速度对比 
StringBuilder  > StringBuffer

-----------

#### 总结
+ 速度 StringBuilder  > StringBuffer > String 
+ 使用场景 <br />
    1、操作少量的数据用 String <br />
    2、字符串缓冲区被单个线程使用的时候用 StringBuilder <br />
    3、字符串缓冲区被多个线程使用的时候用 StringBuffer

