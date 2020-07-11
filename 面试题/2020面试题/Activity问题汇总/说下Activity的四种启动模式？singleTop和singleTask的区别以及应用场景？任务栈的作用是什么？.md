#### 说下Activity的四种启动模式？
+ standard标准模式：每次启动一个Activity就会创建一个新的实例
+ singleTop栈顶复用模式：如果新Activity已经位于任务栈的栈顶，就不会重新创建，并回调 onNewIntent(intent) 方法
+ singleTask栈内复用模式：只要该Activity在一个任务栈中存在，都不会重新创建，并回调 onNewIntent(intent) 方法。
如果不存在，系统会先寻找是否存在需要的栈，如果不存在该栈，就创建一个任务栈，并把该Activity放进去；如果存在，就会创建到已经存在的栈中
+ singleInstance单实例模式：具有此模式的Activity只能单独位于一个任务栈中，且此任务栈中只有唯一一个实例

#### singleTop和singleTask的区别以及应用场景？
+ singleTop：同个Activity实例在栈中可以有多个，即可能重复创建；该模式的Activity会默认进入启动它所属的任务栈，即不会引起任务栈的变更；
为防止快速点击时多次startActivity，可以将目标Activity设置为singleTop
+ singleTask：同个Activity实例在栈中只有一个，即不存在重复创建；可通过android：taskAffinity设定该Activity需要的任务栈，即可能会引起任务栈的变更；常用于主页和登陆页

#### singleTop或singleTask的Activity在以下情况会回调onNewIntent()
singleTop：如果新Activity已经位于任务栈的栈顶，就不会重新创建，并回调 onNewIntent(intent) 方法
singleTask：只要该Activity在一个任务栈中存在，都不会重新创建，并回调 onNewIntent(intent) 方法

#### 任务栈的作用是什么？
它是存放 Activity 的引用的，Activity不同的启动模式，对应不同的任务栈的存放；
可通过 getTaskId()来获取任务栈的 ID，如果前面的任务栈已经清空，新开的任务栈ID+1，是自动增长的；
首先来看下Task的定义，Google是这样定义Task的：Task实际上是一个Activity栈，通常用户感受的一个Application就是一个Task。从这个定义来看，Task跟Service或者其他Components是没有任何联系的，它只是针对Activity而言的。


