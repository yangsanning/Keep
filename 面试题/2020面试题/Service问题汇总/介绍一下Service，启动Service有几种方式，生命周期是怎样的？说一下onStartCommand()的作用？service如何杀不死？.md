#### Service分为两种
##### 1. 本地服务（同一个应用程序）
通过startService来启动或者通过bindService来绑定并且获取代理对象。<br>
如果只是想开个服务在后台运行的话，直接startService即可。<br>
如果需要相互之间进行传值或者操作的话，就应该通过bindService。
##### 2. 远程服务（不同应用程序之间）
通过bindService来绑定并且获取代理对象。

#### 对应的生命周期如下：
##### 1. 本地服务
context.startService() ->onCreate()- >onStartCommand()->Service running<br>
调用context.stopService() ->onDestroy()
##### 2. 远程服务
context.bindService()->onCreate()->onBind()->Service running<br>
调用>onUnbind() -> onDestroy()

#### Service生命周期诠释
| 生命周期 | 诠释 |
| ---- | ---- |
| onCreate() | 服务第一次被创建时调用 |
| onStartComand() | 服务启动时调用 |
| onBind() | 服务被绑定时调用 |
| onUnBind() | 服务被解绑时调用 |
| onDestroy() | 服务停止时调用 |

#### 说一下onStartCommand()的作用？service如何杀不死？
##### 1. onStartCommand方法，返回START_STICKY（粘性）当service因内存不足被kill，当内存又有的时候，service又被重新创建
##### 2. 设置优先级，在服务里的ondestory里发送广播 在广播里再次开启这个服务,双进程守护

#### 注意
Service默认是运行在main线程的，因此Service中如果需要执行耗时操作（大文件的操作，数据库的拷贝，网络请求，文件下载等）的话应该在子线程中完成。
