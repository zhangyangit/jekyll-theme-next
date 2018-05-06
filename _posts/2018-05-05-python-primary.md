---
title: Python Primary
categories:
 - Techs blog
tags:
- python
- program
---

This is the Primary of Python. It try to introduce the basic knowledge. 

---

# Third ： 

---

# Second ：

---

# First ： 图片转字符串
## Preposition 相关库
### argparse 命令项选项与参数解析的模块
#### 1.基本步骤
创建 ArgumentParser() 对象

调用 add_argument() 方法添加参数
1.dest 参数
大部分ArgumentParser动作给parse_args()返回对象的某个属性添加某些值。
该属性的名字由add_argument()的dest关键字参数决定。对于位置参数的动作，
dest 通常作为第一个参数提供给add_argument()，如例：

```python
parser.add_argument('integer', type=int, help='display an integer')
```

 'integer' 为添加的属性，通过add_argument()添加。此参数为必须添加的参数。
2.可选参数
parse_args()方法支持几种指定一个选项的值的方法。最简单的方法是，将选项和它的值以两个分开的参数传递：
对于长选项（名字长度超过一个字符的选项），选项和它的值还可以用一个单一的命令行参数传递，并用=分隔它们：

```python
parser.add_argument("--square", help="display a square of a given number", type=int)
```

 对于短选项（长度只有一个字符的选项），选项及其值可以连在一起：

```python
parser.add_argument("-v", "--verbose", type=int, help="the base")
```

几个短选项可以连在一起仅使用一个-前缀，只要只有最后一个选项要求有值或者都不要有值：

```python
parser.add_argument("-vwww", "--verbose", help="increase output verbosity", action="store_true")
```

3.混合使用
定位参数和选项参数可以混合使用，看下面一个例子，给一个整数序列，输出它们的和或最大值（默认）：

```python
parser.add_argument('integers', metavar='N', type=int, nargs='+',
                   help='an integer for the accumulator')
```

使用 parse_args() 解析添加的参数

#### 2.参数冲突
1.add_mutually_exclusive_group函数

add_mutually_exclusive_group()。它可以让我们指定某个参数和其他参数冲突。
      
```python
group = parser.add_mutually_exclusive_group()
group.add_argument("-v", "--verbose", action="store_true")
group.add_argument("-q", "--quiet", action="store_true")
```

```
python 1.py -v -q
usage: 1.py [-h] [-v | -q]
test.py: error: argument -q/--quiet: not allowed with argument -v/--verbose
```

2.位置参数只有在它们看上去像负数且解析器中没有选项看上去是负数时才可以以-开始：
    
```
parser = argparse.ArgumentParser(prog='PROG')
parser.add_argument('-x')
parser.add_argument('foo', nargs='?')

# no negative number options, so -1 is a positional argument
parser.parse_args(['-x', '-1'])
Namespace(foo=None, x='-1')

# no negative number options, so -1 and -5 are positional arguments
parser.parse_args(['-x', '-1', '-5'])
Namespace(foo='-5', x='-1')

# negative number options present, so -2 is an option
parser.parse_args(['-2'])
usage: PROG [-h] [-1 ONE] [foo]
PROG: error: no such option: -2

# negative number options present, so both -1s are options
parser.parse_args(['-1', '-1'])
usage: PROG [-h] [-1 ONE] [foo]
PROG: error: argument -1: expected one argument
```

如果你有必须以- 开始的位置参数且不是负数，你可以插入伪参数'--'告诉parse_args()其后的所有内容都为位置参数

3.参考文章

https://www.cnblogs.com/xiaofeiIDO/p/6154953.html

### PIL 的 Image 模块 
Image模块是PIL中最重要的模块，它有一个类叫做image，与模块名称相同。
#### 1.Image类的属性
1.Format 源文件格式

```python
from PIL import Image
im= Image.open("D:\\Code\\Python\\test\\img\\test.jpg")
im.format
```

2.Mode 图像模式
这个字符串表明图像所使用像素格式。该属性典型的取值为“1”，“L”，“RGB”或“CMYK”

#### 2.PIL基本概念
1.通道
每张图片都是由一个或者多个数据通道构成。PIL允许在单张图片中合成相同维数和深度的多个通道。
对于一张图片的通道数量和名称，可以通过方法getbands()来获取。方法getbands()是Image模块的方法，
它会返回一个字符串元组（tuple）。该元组将包括每一个通道的名称。

```python
im.getbands()
```

2.模式
图像的模式定义了图像的类型和像素的位宽。当前支持如下模式：
1：1位像素，表示黑和白，但是存储的时候每个像素存储为8bit；
L：8位像素，表示黑和白；
P：8位像素，使用调色板映射到其他模式；
RGB：3x8位像素，为真彩色；
RGBA：4x8位像素，有透明通道的真彩色；
CMYK：4x8位像素，颜色分离；
YCbCr：3x8位像素，彩色视频格式；
I：32位整型像素；
F：32位浮点型像素；
PIL也支持一些特殊的模式，包括RGBX（有padding的真彩色）和RGBa（有自左乘alpha的真彩色）。

```python
im.mode
```

3.尺寸
通过size属性可以获取图片的尺寸。这是一个二元组，包含水平和垂直方向上的像素数。

```python
im.size
(800, 450)
```

4.坐标系统
PIL使用笛卡尔像素坐标系统，坐标(0，0)位于左上角。注意：坐标值表示像素的角；位于坐标（0，0）处的像素的中心实际上位于（0.5，0.5）。

坐标经常用于二元组（x，y）。长方形则表示为四元组，前面是左上角坐标。例如，一个覆盖800x600的像素图像的长方形表示为（0，0，800，600）。

5.调色板
调色板模式 ("P")使用一个颜色调色板为每个像素定义具体的颜色值

6.信息
使用info属性可以为一张图片添加一些辅助信息。这个是字典对象。加载和保存图像文件时，多少信息需要处理取决于文件格式。

```python
im.info
{'jfif_version':(1, 1), 'jfif': 257, 'jfif_unit': 1, 'jfif_density': (96, 96), 'dpi': (96, 96)}
```

7.滤波器
对于将多个输入像素映射为一个输出像素的几何操作，PIL提供了4个不同的采样滤波器：
NEAREST：最近滤波。从输入图像中选取最近的像素作为输出像素。它忽略了所有其他的像素。
BILINEAR：双线性滤波。在输入图像的2x2矩阵上进行线性插值。注意：PIL的当前版本，做下采样时该滤波器使用了固定输入模板。
BICUBIC：双立方滤波。在输入图像的4x4矩阵上进行立方插值。注意：PIL的当前版本，做下采样时该滤波器使用了固定输入模板。
ANTIALIAS：平滑滤波。这是PIL 1.1.3版本中新的滤波器。对所有可以影响输出像素的输入像素进行高质量的重采样滤波，以计算输出像素值。在当前的PIL版本中，这个滤波器只用于改变尺寸和缩略图方法。
Image模块中的方法resize()和thumbnail()用到了滤波器。

#### 3.PIL的ImageOps模块
1.Autocontrast

2.Colorize

3.Crop

4.Deform

5.Equalize

6.Expand

7.Fit

8.Flip

9.Grayscale

10.Invert

11.Mirror

12.Posterize

13.Solarize

未完待续

## Theory
字符画就是一系列的字符组合，把字符看做一个像素，一个字符代表一种颜色。
转换一张彩色的图片，就需要将多彩颜色对应到相应的字符，可以采用灰度值表示。
灰度值：指黑白图像中点的颜色深度，范围一般从0到255，白色为255，黑色为0，故黑白图片也称灰度图像
其中将RGB值映射到灰度值：

```python
gray ＝ 0.2126 * r + 0.7152 * g + 0.0722 * b
```

通过这样的方法，就可以将对应灰度值指向一个不重复的字符列表。

## code

{% highlight ruby linenos %}
# _*_ coding: utf-8 _*_

__author__ = 'Morgan'

'''
python dataView.--Little APP
'''
# 图像处理
from PIL import Image
# 命令行处理
import argparse


# 命令行处理参数
# 1.构建 ArgumentParser对象
parser = argparse.ArgumentParser()
# 2.添加参数
parser.add_argument('file')                            # 输入文件
parser.add_argument('-o', '--output')                  # 输出文件
parser.add_argument('--width', type=int, default=80)   # 输出字符宽度
parser.add_argument('--height', type=int, default=80)  # 输出字符高度
# 3.解析参数
args = parser.parse_args()

# 创建Image 对象
IMG = args.file
WIDTH = args.width
HEIGHT = args.height
OUTPUT = args.output

# 构建字符列表
ascii_char = list("$@B%8&WM#*oahkbdpqwmZO0QLCJUYXzcvunxrjft/\|()1{}[]?-_+~<>i!lI;:,\"^`'.")


# 将256 灰度映射到对应的字符
def get_char(r, g, b, alpha=256):
    if alpha == 0:
        return ' '
    length = len(ascii_char)
    gary = int(0.2126 * r + 0.7152 * g + 0.0722 * b)
    unit = (256.0 + 1) / length
    return ascii_char[int(gary/unit)]

if __name__ == '__main__':
    im = Image.open(IMG)
    im = im.resize((WIDTH, HEIGHT), Image.NEAREST)
    txt = ""
    for i in range(HEIGHT):
        for j in range(WIDTH):
            txt += get_char(*im.getpixel((j, i)))
        txt += '\n'

    print(txt)
    # 输出到文件
    if OUTPUT:
        with open(OUTPUT, 'w') as f:
            f.write(txt)
    else:
        with open("output.txt", 'w') as f:
            f.write(txt)
{% endhighlight %}
---

# Normal block

```
parser = argparse.ArgumentParser(prog='PROG')
parser.add_argument('-x')
```
    print 'helloworld'

# Highlight block

```javascript
alert( 'Hello, world!' );
```

```python
gray ＝ 0.2126 * r + 0.7152 * g + 0.0722 * b
```

```ruby
def foo
  puts 'foo'
end
```

{% highlight ruby %}
def foo
  puts 'foo'
end
{% endhighlight %}

{% highlight ruby linenos %}
def foo
  puts 'foo'
end
{% endhighlight %}

```c++
#include <iostream>

using namespace std;

void foo(int arg1, int arg2)
{

}

int main()
{
  string str;
  foo(1, 2);
  cout << "Hello World" << endl;
  return 0;
}
```
