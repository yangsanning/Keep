## Android消息机制介绍？

#### Android消息机制中的四大概念：
* ThreadLocal：当前线程存储的数据仅能从当前线程取出。
* MessageQueue：具有时间优先级的消息队列。
* Looper：轮询消息队列，看是否有新的消息到来。
* Handler：具体处理逻辑的地方。


#### 过程：
1) 准备工作：创建Handler，如果是在子线程中创建，还需要调用Looper#prepare()，在Handler的构造函数中，会绑定其中的Looper和MessageQueue。
2) 发送消息：创建消息，使用Handler发送。
3) 进入MessageQueue：因为Handler中绑定着消息队列，所以Message很自然的被放进消息队列。
4) Looper轮询消息队列：Looper是一个死循环，一直观察有没有新的消息到来，之后从Message取出绑定的Handler，最后调用Handler中的处理逻辑，这一切都发生在Looper循环的线程，这也是Handler能够在指定线程处理任务的原因。
