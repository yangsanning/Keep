## IdleHandler介绍？
> IdleHandler是在Hanlder空闲时处理空闲任务的一种机制。

#### 执行场景：
1. MessageQueue没有消息，队列为空的时候。
2. MessageQueue属于延迟消息，当前没有消息执行的时候。


#### 问:：会不会发生死循环？
答：不会，MessageQueue使用计数的方法保证一次调用MessageQueue#next方法只会使用一次的IdleHandler集合。
