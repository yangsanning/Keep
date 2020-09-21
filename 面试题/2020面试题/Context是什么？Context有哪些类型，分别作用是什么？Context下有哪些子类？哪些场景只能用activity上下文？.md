##### Context是什么？
Context是一个抽象基类。在翻译为上下文，也可以理解为环境，是提供一些程序的运行环境基础信息。

##### Context有哪些类型，分别作用是什么？
* Context下有两个子类，ContextWrapper是上下文功能的封装类，而ContextImpl则是上下文功能的实现类。
* ContextWrapper又有三个直接的子类，ContextThemeWrapper（带主题的封装类）、Service和Application和Activity。
Activity和Service以及Application的Context是不一样的，只有Activity需要主题，Service不需要主题。

##### Context下有哪些子类，主要是干什么的？
* Context一共有三种类型，分别是Application、Activity和Service。
* 这三个类虽然分别各种承担着不同的作用，但它们都属于Context的一种，而它们具体Context的功能则是由ContextImpl类去实现的，
因此在绝大多数场景下，Activity、Service和Application这三种类型的Context都是可以通用的。
* 不过有几种场景比较特殊，比如启动Activity，还有弹出Dialog。出于安全原因的考虑，Android是不允许Activity或Dialog凭空出现的，
一个Activity的启动必须要建立在另一个Activity的基础之上，也就是以此形成的返回栈。而Dialog则必须在一个Activity上面弹出（除非是系统级别吐司），
因此在这种场景下，我们只能使用Activity类型的Context，否则将会出错。
