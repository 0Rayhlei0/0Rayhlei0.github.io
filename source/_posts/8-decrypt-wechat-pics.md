---
title: "[信息安全]解码微信PC版中以dat格式存储的聊天图片"
date: 2022-03-04 22:00:09
tags: [微信,解码,Python,日常学习]
categories: 信息安全
description: "[第8篇]本篇中我稍微深入了解了一下微信存储聊天图片的方式(.dat文件)以及相应的解码方式。"
top_img: https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/blog_img/security.jpg
cover: https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/cover_img/8-decrypt-wechat-pics.jpg
katex: true
---

# 序言

最近有些好奇微信PC版的聊天文件在本地是如何保存的，因为这些文件要兼顾`可以快速随时访问`，又要`不能直接在文件夹中展示`，所以稍微研究了一下，发现原来这些文件虽然是被加密过,但解码的方法其实非常简单(与其说被加密不如说只是让它不能直接打开而已)，这里就分享一下这个dat文件的`解码原理`和我写的`解码小脚本`。

# 正文

## 方法论

我首先找到的是[这篇文章][1]，通过这篇文章我知道了两个原先不知道的小知识，`第一`是jpg有固定的`标识符FF D8`来标记图像的起始位置，`第二`是dat文件的加密方式是对图片文件的每一个字节做一个固定数值的`异或运算(XOR)`(既以比特(bit)各位计算，两值不同返回1，两值相同返回0，运算符号为⊕)，`异或运算`的一个重要特性就是`自反性`，既：
$$
a \oplus b \oplus a = b
$$
而我们现在已经有了一个经过`特定数值x`异或处理过的`FF D8`，那么我们只要在这个基础上再使用`FF D8`进行异或运算就能倒算出这个特定的数值`x`，既：

$$
\mathrm{0xffd8\ \oplus}\ x\ \mathrm{\oplus \ 0xffd8}=x
$$

然后使用这个计算出来的`x`将`dat文件`中的所有字节都进行异或运算就可以得到原来的图片数据了。我们可以先小试一下实际是不是这样。

## 小实验

我们就借用[这位大佬][1]的代码和思路，先随便拿张图试试。先用[sublime text编辑器][2]的十六进制模式查看一下这个被抽中的幸运图片的内容：

![dat文件开头是'6641'](https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics/post_img/image-20220305125220649.png)

这时用计算器的程序员模式算一下$\mathrm{0x6641\oplus 0xffd8}$的结果：

![结果是'9999'，因此可知x是'99'](https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics/post_img/image-20220305125751063.png)

那就把这个`幸运图片(.dat)`的每一个字节对`99`做一次`异或运算`吧：

```python
def imageDecode(f):
    dat_read = open(f,"rb") # 打开这个图片
    out = "00.png" 
    png_write = open(out, "wb") # 定义一个输出写入的文件
    # 遍历每一个字节并对每一个字节做99的异或运算后写入新png文件
    for now in dat_read:
        for nowByte in now:
            newByte = nowByte ^ 0x99
            png_write.write(bytes([newByte]))
    #关闭两个文件
    dat_read.close()
    png_write.close()

name = "0b64663254a42d95d4546fd03a85d921.dat"
imageDecode(name)
```

运行后发现果不其然，图片信息被还原了：

![image-20220305130647692](https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics/post_img/image-20220305130647692.png)

看来方法是没有问题的，但似乎用计算器算x这个步骤有些脱裤放屁的嫌疑了，直接用Python算好了自己代进去不就好了，这样就可以把解码步骤一般化啦。那就改进一下吧。

## 改进一下

我想让解码的工作更加方便快捷一些，只需要把我们的exe文件放进微信的存储文件夹下运行就可以自动解码所有的文件并且放在一个固定的文件夹中，这里我假设`每个文件夹中的dat文件都用相同的字节加密`，所以每次打开一个文件夹，程序都会用文件夹中的第一个dat文件的第一个字节来解码得到解码字节。

但事实上根据我的观察，似乎这个解码字节似乎是根据主机与用户号生成，也就是说同一个用户在同一台主机中的图片文件都被用同一个解码字节加密成dat文件，但用这个程序也不需要管那么多了，只要你没有把不同用户的dat文件混合在一个文件夹下就都没有问题。于此同时，我还给程序加了一些可视化的`进度条`，这样解码大量文件时也不会等得茫然。废话少说，放代码：

```python
import os
from tqdm import tqdm
import shutil


def get_decode_key(file):
    # 读取文件第一个字节并与0xFF做异或运算以得到解码字节
    dat_read = open(file, "rb")
    head = dat_read.read(1)
    x = int.from_bytes(head, byteorder='big')
    dat_read.close()
    return x ^ 0xFF


def image_decode(file_in, file_out ,key):
    # 将图片中每个字节分别与解码字节做异或运算并输出结果至指定地点
    dat_read = open(file_in,"rb")
    out = os.path.join(file_out)+".png"
    png_write = open(out, "wb")
    for now in dat_read:
        for nowByte in now:
            newByte = nowByte ^ key
            png_write.write(bytes([newByte]))
    dat_read.close()
    png_write.close()


def decode_all():
    # 列出当前文件夹下的所有文件
    fsinfo = os.listdir()
    num_folders = len([x for x in fsinfo if os.path.isdir(x) and x not in (".idea", "result")])
    i = 0

    # 创建一个result文件夹来存储结果
    if 'result' not in fsinfo:
        os.makedirs('result')
    else:
        shutil.rmtree('result')
        os.makedirs('result')

    # 遍历当前文件夹中的所有子文件夹
    # 并将里面所有dat文件进行解码后放入result文件夹中的相应位置
    for folders in fsinfo:
        # 只对文件夹中的内容解码
        if os.path.isdir(folders) and folders not in (".idea", "result"):
            i += 1
            print("\r", end="")
            print("Folders to be decoded: %s/%s" % (i, num_folders))
            temp_path = os.path.join("result", folders)
            os.makedirs(temp_path)
            key_flag = False # 每个文件夹只对第一个文件提取解码字节
            dat_files = [x for x in os.listdir(folders) if x.endswith(".dat")] # 只看文件夹中的dat文件
            if len(dat_files) == 0:
                print("No dat file in this folder")
            else:
                # 对每个文件夹中的dat文件分别解码并放入“result”文件夹中的相应位置
                for files in tqdm(dat_files, desc="Folder%s: " % i):
                    output_path = os.path.join(temp_path, files)
                    if key_flag is False:
                        file_path = os.path.join(folders, files)
                        key = get_decode_key(file_path)
                        image_decode(file_path, output_path, key)
                        key_flag = True
                    else:
                        file_path = os.path.join(folders, files)
                        image_decode(file_path, output_path, key)
            if i == num_folders:
                print("All Jobs Done!")


def main():
    decode_all()


if __name__ == '__main__':
    main()
```

## 打包测试一下

用py2exe包把文件打包成一个`exe文件`，大小大概`7.6M`比较合理。把这个exe文件复制去我自己的微信image文件夹下双击运行，程序就开始慢慢跑起来了。

![把exe文件放在微信image文件夹下双击便可运行](https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics/post_img/image-20220306195549214.png)

![所有图片都被复原了~！](https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/post_img/image-20220306195720817.png)

结果非常完美！运行体验也很好！

## 软件下载

我把这个exe文件放在这里`转需`，也可以看看自己的微信里都缓存了些什么玩意：[文件下载](/attachment/wechat_img_decryption.exe)

## 补充一个小bug的解决思路

我发现有一种情况可能导致解码失败，那就是当微信聊天的图片不仅仅有`jpg格式`还有`png格式`时，我们如果第一步获取解码字节是从这些`png加密的dat文件中`获取,这些图片的文件头是`89 50`(来自[这篇博文][3]，非常有用马克一下)，但我们是使用`jpg格式`的文件头`FF D8`来获取，这会导致获得错误的解码字节，从而导致一整个文件夹都解码失败。

我已经想到了一个`解决办法`，因为dat文件不管是`png图片`还是`jpg图片`都会被同一个解码字节进行异或处理，那也就是说因为异或运算的自反性，使用加密后的字节1与加密后的字节2进行异或运算所得的结果`与其加密前的异或结果会是一样的`，如下式：
$$
(\mathrm{字节1\ \oplus}\ x)\ \mathrm{\oplus \ (字节2\ \oplus}\ x)=(\mathrm{字节1\ \oplus\ 字节2})\ \mathrm{\oplus \ }x\ \mathrm{\oplus \ }x=\mathrm{字节1\ \oplus\ 字节2}
$$
而`png`的文件头`89 50`进行异或运算结果为`D9`，这与`FF D8`两字节的异或运算结果`27`是不一样的，由此我们可以增加一个判断，将dat文件的头两个字节进行异或运算，若得出结果为`27`，则判断`加密前为jpg文件`，使用`FF D8来获得解码字节`；若得出结果为`D9`，则判断`加密前为png文件`，使用`89 50来获得解码字节`。只要解码字节获取成功，后面的解码操作其实都是一样的。但我懒得改代码了，`反正也没那么多png图片`，有需要的自己把思路拿去改吧。

# 最后

通过这一次的这个好奇心驱使下的学习，实际上除了主题相关的`图片格式`，`微信dat文件加密`方式等等以外，最重要的是我重新复习了一下`Python操作文件`，`显示进度条`以及`打包`等等内容，都是非常基础但需要熟能生巧的技能。

[第8篇]

[1]: https://blog.csdn.net/ainivip/article/details/111772428	"微信Dat文件解码"
[2]: https://www.sublimetext.com/	"Sublime Text website"
[3]: https://blog.csdn.net/weixin_30847865/article/details/96186989	"利用文件头标志判断文件类型"

