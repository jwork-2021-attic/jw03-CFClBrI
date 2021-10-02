# W03

## 代码工作原理

本次实验的代码分为两个部分：BubbleSorter类的编码与隐写术图片的生成、BubbleSorter类的解码与类的生成。

第一部分由encoder包中的SteganographyFactory模块来实现，后者接受一个文件路径和一张图片路径,
通过classloader包中的Steganography模块，将文件进行编码后写入图片。
具体的，getSteganography函数先调用compile函数对BubbleSorter.java进行编译，
生成对应的class文件。接着，读取源图片Bubble.jpeg，将读取到的数据传递给SteganographyEncoder类，
并调用EncodeFile函数。后者读取生成的class文件，对其进行编码，与源图片进行融合。最后，将生成的图片保存在本地。

第二部分由classloader包中的SteganographyClassLoader模块来实现，后者接受一张图片路径，
读取解析这一图片，并动态构造一个类。
具体的，根据双亲委派机制，loadClass函数会向上委派一个AppClassLoader在本地寻找BubbleSorter这样一个类，
若找不到，则调用自己的findClass函数来进行查找。而我们重载的findClass函数会先对图片进行解码得到类的代码，
再调用defineClass函数来构造这样一个类。

在类被构造后，被返回给Scene中的main函数，后者被转换为Sorter类的对象，并被提供给Geezer来进行排序。

## 编码两种排序算法

使用QuickSorter.java生成的隐写术图链接为：

[QuickSorter](file:///C:/Users/唐家昕/Desktop/jwork-2021/jw03-CFClBrI/S181860086.QuickSorter.png)

使用HeapSorter.java生成的隐写术图链接为：

[HeapSorter](file:///C:/Users/唐家昕/Desktop/jwork-2021/jw03-CFClBrI/S181860086.HeapSorter.png)

## 生成对应的排序动画

使用QuickSorter.java生成的排序动画链接为：

[asciinema.org](https://asciinema.org/a/szibBP0bwaKZKIQy95htpWITC)

使用HeapSorter.java生成的排序动画链接为：

[asciinema.org](https://asciinema.org/a/LiwgoSC2julKjd6ktlHeDhr2Y)

## 使用另一位同学的图片

使用 202220008 刘睿哲 同学的[ShellSorter](file:///C:/Users/唐家昕/Desktop/jwork-2021/jw03-CFClBrI/example.ShellSorter.png)图片，
得到的结果正确。