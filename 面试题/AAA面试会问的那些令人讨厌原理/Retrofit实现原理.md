## 网络封装框架：Retrofit  实现原理

### 说说Retrofit
Retorfit是一个基于OkHttp封装的网络请求框架，采用了大量设计模式，动态注解生成对应业务代码，可以结合RxJava进行使用。

### Retrofit1和Retrofit2的区别
Retrofit是一个 RESTFUL 的网络请求框架的封装，Retrofit2.0开始内置 OkHttp。前者专注于接口封装，后者专注于网络请求的高效。

### <span id="jump">你为什么会用到 Retrofit？</span>
#### 功能强大：
* 支持同步异步
* 支持多种数据的解析 & 序列化格式
* 支持RxJava

#### 简洁易用
* 通过注解配置网络请求参数
* 采用大量设计模式简化使用

#### 可扩展性好
* 功能模块高度封装
* 解耦彻底，如自定义Converters


### 说说Retrofit的优缺点：
* 优点： 详看问题 [你为什么会用到 Retrofit？](#jump)
* 缺点： 扩展性差，高度封装所带来的必然后果， 如果服务器不能给出统一的 API 形式，会很难处理。


### Retrofit 的核心原理
Retrofit主要是在 create方法中采用动态代理模式（通过访问代理对象的方式来间接访问目标对象）实现接口方法，
这个过程构建了一个ServiceMethod对象，根据方法注解获取请求方式、参数类型、参数注解拼接请求的链接，当一切准备好之后会把数据添加到Retrofit的RequestBuilder中。
当我们主动发起网络请求时会调用OkHttp发起网络请求，OkHttp的配置（包括请求方式，Url等）都是在 Retrofit的 RequestBuilder的 build()方法中实现。


### 你知道Retrofit都用了哪些设计模式吗？
> 我们都知道Retrofit使用大量设计模式，为了方便讲解，我们进行一下简要剖析。

#### 1.创建Retrofit实例
* 使用 **建造者模式** 通过内部Builder类创建了Retrofit实例
* 网络请求工程使用了 **工厂方法模式**

#### 2.创建网络请求接口的实例
* 首先，使用 **外观模式** 统一调用创建网络请求接口实例和网络请求参数配置方法
* 然后，使用 **动态代理模式** 动态的去创建网络请求接口实例
* 接着，使用 **建造者模式** 以及 **单例模式* 创建了ServiceMethod对象。
* 再者，使用 **策略模式** 对ServiceMethod对象进行网络请求参数配置（既通过解析网络请求接口方法的参数、返回值和注解类型，
从Retrofit对象中获取相应的网络url地址、网络请求执行器、网络请求适配器和数据转换器）。
* 最后，使用 **装饰者模式** ExecuteCallBack 为 serviceMethod 对象加入线程切换的操作，便于接受数据后通过 Handler 从子线程切换到主线程从而对返回数据结果进行处理。

#### 3.发起网络请求
* 在异步请求时，通过静态 delegate **代理** 对网络请求接口的方法中的每个参数使用对应的ParameterHanlder 进行解析。

#### 4.解析数据

#### 5.切换线程
* 使用 **适配器模式** 通过检测不同的Platform 使用不同的回调执行器，然后使用回调执行器切换线程，这里同样是使用了 **装饰模式**。

#### 6.处理结果


### 网络框架这么多，你为什么会选择Retrofit？
[Android 主流网络请求开源库的对比（Android-Async-Http 、Volley 、OkHttp 、Retrofifit）](https://www.jianshu.com/p/050c6db5af5a)
