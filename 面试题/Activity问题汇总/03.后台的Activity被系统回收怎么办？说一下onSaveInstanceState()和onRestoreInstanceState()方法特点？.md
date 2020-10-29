#### 后台的Activity被系统回收怎么办？
Activity中提供了一个 onSaveInstanceState()回调方法，这个方法会保证一定在活动被回收之前调用，可以通过这个方法来解决活动被回收时临时数据得不到保存的问题。
onSaveInstanceState()方法会携带一个Bundle类型的参数，Bundle提供了一系列的方法用于保存数据。</br >
比如可以使用putString()方法保存字符串，使用putInt()方法保存整型数据。每个保存方法需要传入两个参数，第一个参数是键，用于后面从 Bundle中取值，第二个参数是真正要保存的内容。

#### 说一下onSaveInstanceState()和onRestoreInstanceState()方法特点？
Activity的 onSaveInstanceState()和onRestoreInstanceState()并不是生命周期方法，它们不同于onCreate()、onPause()等生命周期方法，它们并不一定会被触发。
```
//保存数据
@Override
protected void onSaveInstanceState(Bundle outBundle) {
	super.onSaveInstanceState(outBundle);
 	outBundle.putBoolean("Change", mChange);
}

//取出数据
@Override 
protected void onRestoreInstanceState(Bundle savedInstanceState) {
	super.onRestoreInstanceState(savedInstanceState);
	mChange = savedInstanceState.getBoolean("Change");
}

/*
* 或者在onCreate方法取数据也可以
* onCreate()方法其实也有一个Bundle类型的参数。这个参数在一般情况下都是null，
* 但是当活动被系统回收之前有通过 onSaveInstanceState()方法来保存数据的话，这个参就会带有之前所保存的全部数据
*/
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    if (savedInstanceState != null) {
        String data = savedInstanceState.getString("data");
    }
}
```

#### 什么时候会触发走这两个方法？
当应用遇到意外情况（如：内存不足、用户直接按Home键）由系统销毁一个Activity，onSaveInstanceState() 会被调用。但是当用户主动去销毁一个Activity时，例如在应用中按返回键，
onSaveInstanceState()就不会被调用。除非该activity是被用户主动销毁的，通常onSaveInstanceState()只适合用于保存一些临时性的状态，而onPause()适合用于数据的持久化保存。

#### onSaveInstanceState()被执行的场景有哪些？
系统不知道你按下HOME后要运行多少其他的程序，自然也不知道activityA是否会被销毁，因此系统都会调用onSaveInstanceState()，让用户有机会保存某些非永久性的数据。

##### 以下几种情况的分析都遵循该原则当用户按下HOME键时
+ 长按HOME键，选择运行其他的程序时
+ 锁屏时
+ 从activity A中启动一个新的activity时
+ 屏幕方向切换时
