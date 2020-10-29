#### 两个Activity之间怎么传递数据？
##### 1. 基本数据类型可以通过Intent传递数据，把数据封装至intent对象中
```
Intent intent = new Intent(content, MeActivity.class);
intent.putExtra("goods_id", goods_id);
content.startActivity(intent);
```

##### 2. 把数据封装至bundle对象中, 把bundle对象封装至intent对象中
```
Bundle bundle = new Bundle();
bundle.putString("malename", "李志");
intent.putExtras(bundle);
startActivity(intent); 
```

#### intent和bundle有什么区别？
> Intent传递数据和Bundle传递数据是一回事，Intent传递时内部还是调用了Bundle。
```
public @NonNull Intent putExtra(String name, String value) {
    if (mExtras == null) {
        mExtras = new Bundle();
    }
    mExtras.putString(name, value);
    return this;
}

```

#### 为什么有了intent还要设计bundle？
##### 1. 两者比较
+ Bundle只是一个信息的载体，内部其实就是维护了一个Map<String,Object>。
+ Intent负责Activity之间的交互，内部是持有一个Bundle的。

#### bundle使用场景
> Fragment之间传递数据；比如，某个Fragment中点击按钮弹出一个DialogFragment。最便捷的方式就是通过Fragment.setArguments(args)传递参数。
```
public static void showFragmentDialog(String title, String content, boolean is_open, AppCompatActivity activity) {
    ServiceDialogFragment mainDialogFragment = new ServiceDialogFragment();
    Bundle bundle = new Bundle();
    bundle.putString("title", title);
    bundle.putString("content", content);
    bundle.putBoolean("is_open",is_open);
    mainDialogFragment.setArguments(bundle);
    mainDialogFragment.show(activity.getSupportFragmentManager());
}

@Override
public void onCreate(Bundle savedInstanceState) {
    setLocal(Local.CENTER);
    super.onCreate(savedInstanceState);
    Bundle bundle = getArguments();
    if (bundle != null) {
        title = bundle.getString("title");
        content = bundle.getString("content");
        is_open = bundle.getBoolean("is_open");
    }
}
```


