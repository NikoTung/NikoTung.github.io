---
layout: post
title: "二进制世界"
description: "二进制的世界"
category: "2014-07"
tags: [翻译,二进制]
---


原文链接地址[Binary World](http://blog.db-in.com/binary-world/)


![](http://db-in.com/images/binary_featured.jpg)

 Hello 大家好！

在这片文章中，我会说一下二进制。文章会覆盖大部分的重要概念和操作，并给大家带来一些关于什么时候，怎么使用以及如何在日常工作中使用二进制的样例。如果你正在寻找一篇关于二进制的教程，恭喜你，来到这里。

让我们深入二进制的世界吧

#  文章目录

* 比特和字节
  ** 自己尝试（ps:这部分会被忽略掉）
* 组合字节
* 位运算
* 位移运算
* 实际应用
  ** 奇偶数循环
  ** 颜色应用
  ** 文件和比特
* 总结

## 概览

为什么说二进制是任何编程语言的最小单位和最快的操作速度呢？我们的计算机，我是说任何有处理器的机器，是由布满电路循环的电路板在上面组成的。每次电子脉冲通过这些回路，只需要一个电子回路就能每秒中通过数以千计的电子脉冲。

![](http://db-in.com/images/electrical_impulse_example.jpg)

脉冲接收器只接收一种信息:"是否有脉冲"，有或者无。这种信息就是比特信息了。一个比特位可以有1或0("是" 或者 "否")两种值。非常简单，有木有。

只就是为什么二进制操作是最快的，没有之一。因为它是电子脉冲非常单一的一个表现，最基本的硬件的之间的交互。文章接下来就是关于这些信息的一个简单组织而成。我会向大家展示如何由比特到字节，数据类型，文件和在虚拟世界的任何东西！

在我们了解了二进制世界后，我们会应用一些数学的方法做一些简单的位操作。最后我们来到高级编程语言层面并展示二进制如何使用在日常编程中并去提高我们的应用程序效率。


## 比特和字节

有时候我们会被这两个名字给混淆了，所以让我们把一切都清清楚楚:"一个比特不等于一个字节"。对于我们现代的高级编程语言，单一的一个比特是不可见的，我们不可能独立的设置一个比特，所有的操作都是在字节的层面。对于我们程序员来说，字节是最基本的单位，而不是比特。但是这特么的比特和字节有什么区别呢？

好吧，一个字节是由八个比特组成的，这是一个等式，也是一个规则，永远不会变的哦。1 Byte = 8 Bits。

所以，如果我们从组合的角度来看这8个比特，我们可以说8个bit(2个可能的值，0 和1)可以出现256中可能的结果(2^8 = 256)。为了能够完全使用这256中可能的结果，我们可以认为这些排列组合是2的幂的力量。

![](http://db-in.com/images/binary_values_example.jpg)

是不是有点疑惑了？好，让我们看看下面的这一列数据，应该能帮你理解这个概念:

### 二进制计算

* 第一个比特(从右到左):2^0 = 1
* 第二个比特(从右到左):2^1 = 2
* 第三个比特(从右到左):2^2 = 4
* 第四个比特(从右到左):2^3 = 8
* 第五个比特(从右到左):2^4 = 16
* 第六个比特(从右到左):2^5 = 32
* 第七个比特(从右到左):2^6 = 64
* 第八个比特(从右到左):2^7 = 128

要计算一个二进制的值，查看每一个比特的看它是否有效(0或1)，如果它有效就把它代表的值给加上。最后你就得到一个字节对应的值了。下面的图展示了一个例子：

![](http://db-in.com/images/binary_base_example.jpg)

上图的计算方式是：128＋64+32+4+1=229。非常简单，对不对？


## 组合字节

我们已经知道了一个字节有256种结果，0-255。但是我们已经习惯了使用一些范围比较大的数据类型，比如 `int` 表示的值的范围是2,147,483,648 to 2,147,483,647或者更大的浮点型，它是怎么做到的呢？

非常简单，使用超过一个字节去表示数据。如果你回到20年前，也许你会记得那种8字节位设备。像8位的任天堂游戏机。你现在知道了这种游戏每次只能处理只有一个字节的数据类型。之后来到了16位，32位或者说今天的32位的平台。这意味着什么呢？

当是16位的情况，意味着一个字节可以同时和另外一个字节（2x8 bits）一起处理，对于32位的，意味着4个字节（4x8 bits）可以同时处理，64位的话就是8个字节（8x8 bits）同时处理等等。下面这张图展示了32位的int 和 float型。

![](http://db-in.com/images/binary_combinations_example.jpg)

想想这个吧:一个简单的处理改变，由读取一个字节到超过一个字节，能够改变在设备上的一切。比如说，如果每次读取8比特，我们有256个颜色值，你还记得这种设备么，很糟糕，是吧。现在每次可以读取4字节，系统就可以运行 4,294,967,296种不同的颜色值.想像一下由于这个改变而从硬件上获取到的性能的提升，由读取一个字节到读取很多个。

扯一个题外话。现在很多人都在说一个种新的处理器：量子处理器。想法是从电子脉冲改变到电子状态。简单说电子有三种能量状态：正(up),中立(Middle)和负(negative),用三种状态：up，middle和negative替代yes 或 no。这个简单的事实可以给到我们一个新的视角和新的类型的比特。另外，不想电路板上的电路脉冲，原子空间上的电子不需要带有一个物理上的路径，只是需要一个简单的原子震动就行了，想想它能多快吧。现在再想想一个原子中有多少电子存在，我们可以同时处理多少字节。现代的一些超级电脑运行在128比特，256比特，512比特或者更多，但是无法跟量子处理器相比。实话说吧，我知道一个由耶鲁大学领导的研究小组已经创建了第一个量子处理器了。当然这个距离商用还有很长距离要走，但是它已经出现在现实世界了。

好吧，扯够了，回来吧。

非常好，我们已经知道了高级编程语言如何处理二进制，我们也知道了二进制如何工作的。所以每一次你创建一个int的数据类型，比如说，实际上，你正在创建一系列的32bit，或者简单说32个0或者1:00000000 0000000 00000000 0000000 。

是时候去学习一些让我们能够在比特层面上的操作了。

## 位操作

仅仅有很少的位操作，实际上4个。它们的操作跟传统的数学操作完全不一样。

####  与:&

用&表示，只有当两个比特的的某一个同时为1是才为1。比如：

	   01001101
	&  00101011
	   --------
	   00001001

上面的结果用伪代码符号可以这样表示：77 && 43 = 9



#### 或:|

用 ｜ 表示，只要两个比特的某一个为1时就为1.比如：

	   01001101
    |  00101011
	   --------
   	   01101111

上面的结果用伪代码符号可以这样表示：77 ｜ 43 = 111

#### 异或:^

用 ^ 表示，只要两个比特的不一样就为1.一样就为0

	  01001101
	^  00101011
	   --------
	   01100110

上面的结果用伪代码符号可以这样表示：77 ^ 43 = 102

#### 取反:~

用~表示，和其他操作不一样，它只跟一个比特序列进行运算，,也称补码。它对比特中的每一个取反。所以如果一个比特为0，它就变成1，反之亦然。比如:

	~  01001101
	   --------
	   10110010

上面的结果用伪代码符号可以这样表示：~77 = 178

所有的要两个操作数的位操作，仅能和同样长度的比特进行运算。但是如果其中一个序列有不足的序列位的话，它会在左边补零，直到它和另外一个一样长。比如说：01010100 & 111 其实就是: 01010100 & 00000111. 请记住，在左边的0没有任何意义。

只需要简单的操作我们就可以创造出让人无法想像的程序。好处是二进制是太特么快了，我们已经说过了。很快我们就能看到一些在日常工作中的真实例子了。在此之前，我们需要了解一下位移操作，它们就像位操作的补充。

## 位移操作

世界上仅存在两种位移操作，左和右。就这么简单。使用位移操作，你需要把比特放到字节中去，这就是说，如果你的数据类型有一个字节，比特仅仅会在一个字节中移动，如果你的数据类型有4字节，比特会在这4个字节中移动。


### 左移 :<<

左移用 "<<"表示，它会把所有的比特位往左边移动。在最左边的比特位将会被废弃掉，右边新增加的将会用0去替代。比如：

    01001101 <<
    --------
    10011010
    
上面的结果用伪代码符号可以这样表示：77 << = 154

### 右移 ：>>

右移用 ">>"表示，它会把每一个比特往右边移动一位。在最右边的比特位将会被废弃掉，左边新增的将会用0去替代。比如：

    01001101 >>
    --------
    00100110
    
上面的结果用伪代码符号可以这样表示：77 >> = 38

位移操作符号总是在表达式的右边。你可以指定多少个比特去往左或往右移动。比如：

    01001101 << 4
    --------
    11010000

    01001101 >> 3
    --------
    00001001

好了，亲们。上面就是所有的二进制操作了。这些简单的操作就可以做出很漂亮的事情来了，包括在你的日常工作中。


## 真正的二进制程序

现在我给你展示的就是一些简单的在日常工作中可以用到的例子，简单到不需要重复编码就可以对你的程序提升性能，只需要简单的改变。我就是跟你说简单的例子，开始吧。

#### 奇偶循环

先从一个简单的例子开始。想象一下这个场景：你需要在一张表中填充线条，你象要用成对的先去填充，其中一条是有颜色，另外一条是没有颜色的。一个简单的一个做法就是数行数，在每一个奇数行给它填上颜色，偶数行让它空白。这样我们就需要用一个循环去检查x%2的结果，但是最快的方法应该是用二进制。一个二进制的循环应该是这样的。

    // Assume the numberOfRows variable was set.
    for (i = 0; i < numberOfRows; ++i)
    {
        if (i&1)
        {
            // The "i" is an odd number.
        }
        else
        {
            // The "i" is an even number.
        }
    }
    .


我太喜欢这个循环了。它就让我想到每一个隐藏在二进制中的规则。在上面的例子中我们实际上做的就是：00000001&xxxxxxx.只要在第一位的值是1，唯一的可能性去创建一个奇数就是使用我们的一个比特。所以，通过是用&操作，我们检查了当前的i是否使用了这一个比特。很简单。

#### 颜色应用

二进制和颜色是一个很热门的话题。基本上主流的图像软件都是使用了二进制去转换图像的。比如，Photoshop在像素级别的二进制改变去生成所有的图像效果。第一件关于二进制和颜色的关系就是要了解十六进制。一个十六进制通过0xN(总是需要通过0x开头)，N有16个不同的值:0-9,A-F.所以，真实的值在十六进制的表达形式如下：

    0x0 = 0
    0x1 = 1
    0x2 = 2
    0x3 = 3
    0x4 = 4
    0x5 = 5
    0x6 = 6
    0x7 = 7
    0x8 = 8
    0x9 = 9
    0xA = 10
    0xB = 11
    0xC = 12
    0xD = 13
    0xE = 14
    0xF = 15

现在我们可以把两个十六进制的数放在一起，其中一个就像我们说的单位，另外一个就象我们平常使用的十进制中的。所以第一个会有16个可能的值，第二个也会有16个可能的值，总共就是256个可能值。等等，256？它是一个字节对吧。所以，我们可以每两个十六进制的数组合在一起(0xNN)表示一个字节。

![](http://db-in.com/images/hexadecimal_example.jpg)


为了使步骤更清晰，下面是一个用十六进制表示的值。

    0x00 = 0      (0 x 16 + 0)
    0x10 = 16     (1 x 16 + 0)
    0x20 = 32     (2 x 16 + 0)
    0x21 = 33     (2 x 16 + 1)
    0x22 = 34     (2 x 16 + 2)
    0xA0 = 160    (10 x 16 + 0)
    0xA9 = 169    (10 x 16 + 9)
    0xAA = 170    (10 x 16 + 10)
    0xAB = 171    (10 x 16 + 11)
    0xF0 = 240    (15 x 16 + 0)
    0xFF = 255    (15 x 16 + 15)

在32位的机器中，我们可以用4个字节去表示一个颜色值，如果我们是在RGB模式下思考的话，加上Alpha,我们为每一个颜色频道保留一个字节大小的容量。这种方式的话，每一个颜色会有256中可能的值。我们可以通过两个十六进制的数(0xNN)表示表示一个字节。所以我们就可以用这样的的一个十六进制组合0xNNNNNNNN完整的表示一个颜色，或者使用这样的表示：0xRRGGBBAA.

由于历史遗留的原因，aplha的处理没有一个固定的模式，所以每一个软件都会有自己的实现，一些使用0xRRGGBBAA,另外一些使用OxAARRGGBB,还有一些使用0xRRGGBB+0xAA.直到今天，我们都还没有一个通用的alpha格式。所以我们就只关注这种格式:0xRRGGBB,在这边文章中。

根据上面的了解，取出每一个颜色值是很简单的事情：

    unsigned int color = 0x99AA44

    unsigned char redChannel = color >> 16;  
    unsigned char greenChannel = ( color >> 8 ) & 0xFF;  
    unsigned char blueChannel = color & 0xFF;

非常简单就可以直到上面的表达式。如果我们通过二进制的方式去表达，color这个变量可能就是：RRRRRRRRGGGGGGGGBBBBBBB. 这样，我们移动十六位到右边，结果就是：

    RRRRRRRRGGGGGGGGBBBBBBBB >> 16 = RRRRRRRR

相似的，我们移动8位去获得绿色值，但是这是绿色值并没有完全孤立出来，红色值还在。所以，为了孤立出来绿色值，我们使用&0xFF(255),通过这样，我们就可以把红色值给丢弃掉，留下绿色值：

    RRRRRRRRGGGGGGGGBBBBBBBB >> 8 = RRRRRRRRGGGGGGGG & 11111111 = GGGGGGGG

最后，我们几乎是做同样的事情去获取蓝色值。

    RRRRRRRRGGGGGGGGBBBBBBBB & 11111111 = BBBBBBBB

如果你是从图片中读到像素数据，它可能会包含alpha的信息(ARGB).所以，为了能够正确的读出每一个颜色值，还要做&0xFF的运算在红色值上。如果是RGBA的话，我们还需要再右移八位。

    unsigned int color = "one pixel data"

    // To pixel data in format ARGB
    unsigned char redChannel = ( color >> 16 ) & 0xFF;  
    unsigned char greenChannel = ( color >> 8 ) & 0xFF;  
    unsigned char blueChannel = ( color >> 0 ) & 0xFF;

    // To pixel data informat RGBA
    unsigned char redChannel = ( color >> 24 ) & 0xFF;  
    unsigned char greenChannel = ( color >> 16 ) & 0xFF;  
    unsigned char blueChannel = ( color >> 8 ) & 0xFF;


一旦你得到了每一个像素点的颜色值，你可以对图像做任何事情。你可以去掉或者替换掉一个颜色值，把它转换到一个灰色缩放的图片，单独修改每一个颜色...看看Photoshop吧，所有的效果都是通过这种方式去做都的。当然，为了能够做出更复杂的效果，比如毛玻璃或者动态模糊，你需要对每一个像素点进行更多的处理，并且还依赖于图片的大小，这是一个非常复杂的过程。

我曾经写过一篇如何通过二进制办法减少图片的颜色范围的的文章。它是我最后的一篇关于OpenGL的教程，你可以从[这里](http://blog.db-in.com/all-about-opengl-es-2-x-part-3/)看到。

关于这个颜色值与二进制的话题的所有信息，都是关于最流行的图片格式，每一个颜色频道使用8比特。但是有些图片会使用更多的比特位，比如16比特／32比特。这些高分辨率的格式支持了非常多的颜色值范围，它们通常是用于彩印的格式，使用的是CMYK而不是RGBA格式。但是如果你需要使用这个高分辨率的图片，代码基本上是一样的，只是改变了一些位移的数量。在虚拟网络，我们假设所有的图片都是使用8bit/channel。下面这张图片展示了现在流行的图片格式的每一个颜色频道所支持的比特数。那些支持32位的也同时向下兼容16位和8位，支持16位的同样也支持8位的。

![](http://db-in.com/images/image_bits_example.jpg)


##  文件和比特位

每一个东西都是由二进制组成的。所有的文件，在最底层，都是比特。所以我们可以从任何文件中解析和提取出信息。前提是你知道了文件中比特的组织结构。这就是文件完全和加密的基本原理了。如果你做了一个编码和解码器去组织文件的比特位，这样文件就会被加密了。更复杂的技术会做一些比如假的比特或者在文件中创建一个密钥然后以一个完全新的结构去创建文件。其实在深层次上，所有的事情都是比特并且能够被读出来。

下面是一些可以了解文件格式的很好的网站

 * [http://www.fileformat.info](http://www.fileformat.info)
 * [http://www.wotsit.org](http://www.wotsit.org)
 * [http://www.martinreddy.net/ - for 2D image files](http://www.martinreddy.net/)
 * [http://www.martinreddy.net/ - for 3D format files](http://www.martinreddy.net/)

当然，你也有另外两个选择：在维基百科上搜索你需要的文件格式或者去文件的创造者的公司网站查找。如果你不知道创造者，你可以去这个网站:[http://whatis.techtarget.com](http://whatis.techtarget.com),然后搜索文件的扩展名，如果存在的话，你就可以看到一个官方链接。


说到文件格式，总的来说，主要的文件制造者都是通过4个字节去组织信息，就算那些信息需要少于4字节。这是一个为了让文件更好的组织和可读性的一个好的实践方法。但是它并不是一个规定，一些文件依然会把很多信息放在4个字节中。

我们的一些高级编程语言通常都会提供一类，或者一系列的类，能够可以去操作二进制文件。所以你可以很轻松的使用任何数据类型并且那些类会给你创建二进制流，格式化一个比特数组。把所有信息放到文件中后，你只需要简单的保存一下，或通过网络发送。我会展示一些用Objective-C写的代码片段。


    // Creates some generic data to save into a file.
    // As in C language the strings are made with an array of chars
    // we must to know the length of the string to calculate
    // the number of bits necessary to write it.
    float floatNumber = 15.2;  
    char *charString = "this is a string";  
    int strLength = strlen(charString) + 1;

    // Initializes the Cocoa class that deals with binaries.
    NSMutableData *data = [[NSMutableData alloc] init];

    // Inserts the data to save. This order is very important.
    [data appendBytes:&floatNumber length:sizeof(float)];
    [data appendBytes:&strLength length:sizeof(int)];
    [data appendBytes:&charString length:sizeof(char) * stringLength];

    // Saves the file.
    [data writeToFile:@"/path/to/save/file.test" atomically:YES];

    // Frees the memory allocated.
    [data release];



就算你不熟悉Objective-C,你也能明白上面的每一步骤。通过标准的c语言库，我们也可以fopen函数去读取一个二进制格式的文件。

最重要的是要理解二进制文件每一个的顺序和每一个信息的长度。在上面的例子中，如果我们改变了调用"appendBytes:length:"的顺序，文件的保存结果就会不一样了。下面的图片展示了两个文件在保存结果：

![](http://db-in.com/images/binary_files_example.jpg)

你能看到的，简单的改变了顺序就会生成了两个不同的文件。上面的图片是通过文本编辑器("十六进制编辑器")，这种软件向我们展示任何文件的二进制格式，每隔四个字节把数据分开。你还记得如何用十六进制表示一个字节吧。0xNNNNNNNN代表四个字节。

为了读取二进制文件内容，你需要由反的方向走：选择一部分比特接着解析它。比如，如果你知道了下四个字节表示一个浮点类型的数据，解析成浮点数，如果你知道下一个字节表示一个字符，解析成字符等等。这有一个重要的事情，去解析一个可变长度的信息，比如一个字符串，你需要知道它的长度。所以每一次我们需要保存一个可变长度的信息，我们都会保存一些比特，通常32bitØs，保存信息的内容。

使用上面的例子，我们可以去写一段打开文件的代码

    // Creates the variables to receive the data from binary file.
    float floatNumber;  
    char *charString;  
    int strLength;

    // Creates a location/pointer to guide the position of the bytes inside the binary file.
    int lastLocation = 0;

    // Initializes the Cocoa class that deals with binaries.
    NSData *data = [[NSData alloc] initWithContentsOfFile:@"/path/to/save/file.test"];

    // Retrieves the floating number from the file and updates the location/pointer.
    [data getBytes:&floatNumber range:NSMakeRange(lastLocation, sizeof(float))];
    lastLocation += sizeof(float);

    // Retrieves the string length from the file and updates the location/pointer.
    [data getBytes:&strLength range:NSMakeRange(lastLocation, sizeof(int))];
    lastLocation += sizeof(int);

    // Allocates the necessary memory to receive the string and retrieves the data.
    charString = malloc(sizeof(char) * strLength);  
    [data getBytes:&charString range:NSMakeRange(lastLocation, sizeof(char) * strLength)];

    // Frees the memory allocated.
    [data release];


通过二进制我们可以做很多了不起的事情。我们可以提高安全，我们可以创建二进制文件去保存信息或者打开二进制文件。性能和容量也是很让人吃惊的，几千字节就能存放很多信息了。


## 总结

好了，现在你能想象到了，我们可以用把二进制的运用到很多地方去了：挺高程序性能；提高安全行；读写文件，二进制对每一件事情都很有用。最后的建议是：尽情的使用二进制吧。在我学习了二进制后，我可是等了好几个月后才去用它。不要学我，去探索二进制的世界吧。就像黑客帝国中一样，你就会看清楚世界背后的二进制了。

好了，让我们再回顾一下吧：

* 比特是计算机电路版中脉冲的最基本表现形式；
* 一比特可以是0或者1；
* 一字节有8比特，总共有256个不同的值；
* 字节可以组合成强大的平台：16位的，32位的，64位的；
* 位操作（&,|,^,~）通过在原来的比特上做出的一些变换生成新的值；
* 位移操作(>>,<<)可以生成新的比特通过改变比特的位置；
* 一对十六进制值可以表示一个自己；
* 在电脑上的每一个文件都是一个二进制形式，并且能够被读出来如果你知道比特的序列。

亲们，这就是关于二进制的一切了。就像你看的一样，它们很简单，非常简单，虽然简单但是非常强大。如果你有什么疑问，尽管问吧。


