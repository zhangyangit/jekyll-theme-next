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
  1. 基本步骤
    创建 ArgumentParser() 对象

    调用 add_argument() 方法添加参数
      1.dest 参数
        大部分ArgumentParser动作给parse_args()返回对象的某个属性添加某些值。该属性的名字由add_argument()的dest关键字参数决定。对于位置参数的动作，dest 通常作为第一个参数提供给add_argument()，如例：

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

  2. 参数冲突
    1.
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

    如果你有必须以- 开始的位置参数且不是负数，你可以插入伪参数'--'告诉parse_args()其后的所有内容都为位置参数：

### PIL 的 Image 模块 
## Theory

## code
---

# Normal block

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

    print 'helloworld'

# Highlight block

```javascript
alert( 'Hello, world!' );
```

```python
group = parser.add_mutually_exclusive_group()
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
