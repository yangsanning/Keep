##  Bitmap的高效加载？


#### glide思路：
1. 获取需要的长和宽，一般获取控件的长和宽。
2. 设置BitmapFactory.Options中的inJustDecodeBounds为true，可以帮助我们在不加载进内存的方式获得Bitmap的长和宽。
3. 对需要的长和宽和Bitmap的长和宽进行对比，从而获得压缩比例，放入BitmapFactory.Options中的inSampleSize属性。
4. 设置BitmapFactory.Options中的inJustDecodeBounds为false，将图片加载进内存，进而设置到控件中。
