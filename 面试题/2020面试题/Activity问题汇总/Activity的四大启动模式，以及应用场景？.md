#### Activity的四大启动模式，以及应用场景？

standard：标准模式，每次都会在活动栈中生成一个新的Activity实例。通常我们使用的活动都是标准模式。

singleTop：栈顶复用，如果Activity实例已经存在栈顶，那么就不会在活动栈中创建新的实例。比较常见的场景就是给通知跳转的Activity设置，因为你肯定不想前台Activity已经是该Activity的情况下，点击通知，又给你再创建一个同样的Activity。

singleTask：栈内复用，如果Activity实例在当前栈中已经存在，就会将当前Activity实例上面的其他Activity实例都移除栈。常见于跳转到主界面。

singleInstance：单实例模式，创建一个新的任务栈，这个活动实例独自处在这个活动栈中。

[See](https://github.com/yangsanning/Keep/blob/master/Android%20%E5%9F%BA%E7%A1%80/02.Activity%E5%9B%9B%E7%A7%8D%E5%90%AF%E5%8A%A8%E6%A8%A1%E5%BC%8F%E4%BB%A5%E5%8F%8A%E4%BD%BF%E7%94%A8%E5%9C%BA%E6%99%AF.md)
