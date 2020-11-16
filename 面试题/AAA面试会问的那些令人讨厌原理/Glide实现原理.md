## 图片加载框架：Glide实现原理

### 这个库是做什么的?
Glide 是 Android 中的一个图片框架，用于实现图片加载。

### 为什么要使用Glide？有什么特点？
* 多样化媒体加载：不仅可以进行图片缓存，还支持Gif、WebP、缩略图、Video。
* 动态管理生命周期：可以通过设置绑定生命周期，使加载图片的生命周期动态管理起来。
* 高效的缓存策略：支持内存、Disk缓存。Picasso只会缓存原始图片尺寸，而Glide缓存是多规格（根据ImageView的大小进行缓存图片）
* 内存开销小：Picasso默认格式是ARGB_8888格式，而Glide默认格式是RGB_565，内存开销足足小一半。

### Glide都有哪些用法，对应什么使用场景?
* 图片加载： Glide.with(this).load(iamgeUrl).into(imageView)。
* 多媒体加载: asBitmap()，asGif()。
* 缓存策略： ALL、NONE、SOURCE、RESULT。
* 生命周期集成。
