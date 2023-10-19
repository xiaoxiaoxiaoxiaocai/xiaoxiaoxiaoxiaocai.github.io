



###  CTFshow

### 基础

#### misc1

打开附件中的图片即可得到 flag

#### misc2

在压缩包里是一个txt文件，该文件显示为乱码。在010中打开，发现是PNG的格式，将后缀改为PNG格式后打开就得到flag

#### misc3

为bpg格式只需用打开bpg文件的软件打开即可。

#### misc4

6个文件分别是png，jpg，bmp，gif，tif，wav格式。依次打开文件即可。

### 信息附加

#### misc5

用010打开文件后，在最后面即可找到flag。

#### misc6

同上

#### misc7

同上

#### misc8

用binwalk分析后，再用foremost分离jike。

#### misc9

用binwalk分析出bzip后，无法用foremost等分离，就用zsteg试试，结果成功分离。

#### misc10

直接用binwalk分离可能会出现安全问题，所以需要以用户的身份来进行执行。在后面加入 --run-as=root 即可。

#### misc11

根据提示flag在另一张图片里，使用工具TweakNPG

发现两个IDAT，删除第一个后重新打开图片即可。

#### misc12

用之前的方法在用F7观察时一直删，知道出现flag为止。

#### misc13

根据提示，很轻易在结尾找到一串字符，

ct¹f…s†hªoKw°{!aeS6¥eT446xc%4Ý8ïf«73•9b‚7ºeEb|2Td~1:däeñ6úeõ412fT8ñ329éal}

显而易见，每隔一个字符就是flag。写一个脚本

```py
s="631A74B96685738668AA6F4B77B07B216114655336A5655433346578612534DD38EF66AB35103195381F628237BA6545347C3254647E373A64E465F136FA66F5341E3107321D665438F1333239E9616C7D"
flag=""
for i in range(0,len(s),4):
    flag += s[i]
    flag += s[i+1]
print(flag)

```

再将16进制转化为ASCII即可得到flag。

#### misc14

提示在那张图片里，binwalk以及foremost无法分离。

在010中找到文件头开始复制，到另一张图片打开即可得到flag

#### misc15

在010打开后直接搜索ctf即可得到flag

#### misc16

用binwalk扫描发现隐藏文件但是无法分解，利用zsteg扫描并分解。

导入1.txt中，再用binwalk分解一下，就出现flag了。

#### misc17

重复上述内容即可。

#### misc18

根据提示，在图片的详细信息里找到flag。

#### misc19

用winhex打开后直接搜索ctf即可得到两段flag。

#### misc20

用exiftool打开后为 这图片也太难看了。来自：西替爱抚秀大括号西九七九六四必一诶易西爱抚零六易一弟七九西二一弟弟诶弟五九三易四二大括号

即ctfshow{c97964b1aecf06e1d79c21ddad593e42}

#### misc21

686578285826597329 16进制转字符串解码得hex(X&Ys)

3902939465237161861910824528172980145261

```py
k=[3902939465,2371618619,1082452817,2980145261]
key=''
for i in k:
    key+=hex(i)[2:]
flag='ctfshow{'+ key + '}'
print(flag)#ctfshow{e8a221498d5c073b4084eb51b1a1686d}
```



#### misc22

用exiftool发现是缩略图隐写。导出图片：

exiftool -ThumbnailImage -b misc22.jpg > 1.jpg 

发现flag

#### misc23

根据提示 得到 ctfshow{}, UnixTimestamp, DECtoHEX, getflag

1997:09:22 02:17:02+08:00（874865822）, 2055:07:15 12:14:48+08:00（2699237688）, 2038:05:05 16:50:45+08:00（2156662245）, 1984:08:03 18:41:46+08:00（460377706）。

转换为时间戳后转化为字符串。

```py
k=[874865822,2699237688,2156662245,460377706]
key=''
for i in k:
    key+=hex(i)[2:]
flag='ctfshow{'+ key + '}'
print(flag)
```

#### misc41

**根据提示：`H4ppy Apr1l F001's D4y！`**

**愚人节到了，一群笨蛋往南飞，一会儿排成S字，一会儿排成B字。**

使用`Editor` 打开 搜索 `F001` 可以看到 `ctf` 的样式 把他提取 出来即可。

### 文件结构

#### misc24

由于是在图片上，修改图片高度即可。

#### misc25

同上

#### misc26

根据图片宽修复图片的高为606

将其16进制，拼接得到flag。

#### misc27

同上修复图片。

#### misc28

同上。

#### misc29

gif图片，每一帧都需要改高度，全部改完后，在stesolve 中打开，采用Frame brower来分析，在第八帧可以看到flag。

#### misc30

根据题目，将宽度由900改到950.

打开即可得到flag。

#### misc31

```py
import os
with open(r'misc31.bmp', 'rb') as f:
    # 读取文件头
    file_header = f.read(14)
    # 读取图像信息头
    info_header = f.read(40)
    # 解析宽度
    width = int.from_bytes(info_header[4:8], byteorder='little')
    # 解析位深度
    bit_count = int.from_bytes(info_header[14:16], byteorder='little')
    # 计算每一行像素点占用的字节数
    bytes_per_row = width * bit_count // 8
    # 读取文件大小
    file_size = os.path.getsize(r'misc31.bmp')
    # 计算图像数据的长度
    data_size = file_size - 54
    # 计算高度
    height = data_size // bytes_per_row
    print('图像宽度：', width)
    print('图像高度：', height)
    # misc31.bmp 为文件地址
```

下面我们来着重看看**位图文件头**：

[![, width=500px](https://s2.loli.net/2022/12/12/RmQEphqy4CoMlwO.png)](https://s2.loli.net/2022/12/12/RmQEphqy4CoMlwO.png)

红色区为bfType：为bmp文件的标识，像png的89504E47一样，一定是 BM 二字。

橙色区为bfsize：表示整个bmp文件的大小。（注意Windows的数据是倒着念的，橙色框的数据为0x0070F685）

绿色区应该是八个0，没什么用。

粉色区为bfOffBits：位图文件头+位图信息头+调色板的大小。

**位图信息头**共四十个字节，我们主要关心宽度和高度就行。

颜色点阵的像素按照**自下而上，自左向右**排序，RGB也是倒着排的，排成B,G,R。

粗略知道这些信息之后，我们就能解出这道题真正的宽度：

我们只要**算出bmp像素数，再算下宽度**即可。

用010editor查看bitmapinforheader的位置，发现到53字节结束，整个文件最后一个字节是487255，用487255减去不表示像素的前面的文件头和信息头，得到487202，RGB三个字节表示一个像素，用487202除以三得到像素数，由于高度是正确的，我们只要再除以高度就能得到真正的宽度了。（有余数直接约去就可以，后面看样子是多加入了几个字节）

#### misc32

修复图片即可得到flag.

#### misc33

同上。

#### misc34

题目把IHDR里的CRC都改了。

将宽度从900开始爆破文件，放在一个目录里，进行查找。

```py
import struct

import zlib

\#爆破png宽度

f = open(r'misc34.png','rb')

c = f.read()

width = c[16:20]

height = c[20:24]

for i in range(900,1200):

  f1 = open(r"新建文件夹"+str(i)+'.png','wb')

  \# print(struct.pack('>i',i)[::-1])

  img = c[:16]+struct.pack('>i',i)+c[20:]

  f1.write(img)

  f1.close()
```

#### misc35

图片打开为空白，从而得知高度和宽度都出错了。

将高度改为600，可以看到有模糊的一列。再用脚本进行依次爆破在993到之后的一些宽度可以得到flag。

```py
import struct

with open(r"\\misc35.jpg", 'rb') as f:
    img = f.read()
    for i in range(901,1200):
        title = str(i) + ".jpg"
        f1 = open(title,"wb")
        img1 = img[:159]+struct.pack('>i',i)[2:4]+img[161:]
        f1.write(img1)
        f1.close()
```



#### misc36

 该gif只有一帧，将高度改为600进行爆破。

```py
import struct

with open("\\misc36.gif", 'rb') as f:
    img = f.read()
    for i in range(920,950):
        title = str(i) + ".gif"
        f1 = open(title,"wb")
        img1 = img[:37]+struct.pack('>i',i)[2:4]+img[39:]
        f1.write(img1)
        f1.close()
```

#### misc37

在stegsolve中进行一帧一帧的查看。`9、14、21、31、34中看到flag

#### misc38

该图片为apng文件，stegsolve并不能找到flag

利用软件honeyview可以一帧一帧的找

ctfshow{48b722b570c603ef58cc0b83bbf7680d}

#### misc39

gif图片有287帧，这道题是由不同帧之间的间隔时间来隐写。

用kali的identify进行读取间隔

```
identify -format "%T " misc39.gif > 1.txt
```

```
37 37 36 36 36 37 37 37 37 37 36 37 36 36 37 37 36 36 37 37 36 37 37 37 36 36 37 37 37 37 36 37 36 36 36 37 37 36 37 37 37 37 37 37 37 36 37 37 37 37 37 37 37 36 37 37 36 37 37 36 37 36 37 36 37 37 36 36 37 36 36 37 37 37 36 36 36 36 37 37 36 36 36 37 36 37 37 36 36 37 36 37 37 36 36 37 37 36 37 37 36 36 37 37 36 36 37 37 37 36 36 37 36 37 37 37 36 36 37 36 37 37 36 37 36 37 37 37 36 36 37 37 36 37 37 36 36 36 37 36 36 37 37 36 37 37 37 37 37 36 36 36 37 36 37 37 36 36 37 36 37 36 37 37 36 36 37 36 36 37 37 36 37 37 36 36 37 37 37 36 36 36 37 37 36 36 37 36 36 36 37 37 37 36 36 37 36 37 37 36 37 37 36 36 37 37 36 36 37 37 37 37 36 36 36 36 37 36 37 37 37 36 36 37 37 37 36 36 37 36 37 37 37 36 36 36 37 36 37 37 36 36 36 37 37 37 37 36 36 36 36 37 36 37 37 36 36 36 36 36 37 37 36 37 36 36 36 37 37 36 37 36 37 36 37 37 37 36 36 37 37 37 37 37 37 36 37 
```

猜测为二进制转化为字符串

```py
t='37 37 36 36 36 37 37 37 37 37 36 37 36 36 37 37 36 36 37 37 36 37 37 37 36 36 37 37 37 37 36 37 36 36 36 37 37 36 37 37 37 37 37 37 37 36 37 37 37 37 37 37 37 36 37 37 36 37 37 36 37 36 37 36 37 37 36 36 37 36 36 37 37 37 36 36 36 36 37 37 36 36 36 37 36 37 37 36 36 37 36 37 37 36 36 37 37 36 37 37 36 36 37 37 36 36 37 37 37 36 36 37 36 37 37 37 36 36 37 36 37 37 36 37 36 37 37 37 36 36 37 37 36 37 37 36 36 36 37 36 36 37 37 36 37 37 37 37 37 36 36 36 37 36 37 37 36 36 37 36 37 36 37 37 36 36 37 36 36 37 37 36 37 37 36 36 37 37 37 36 36 36 37 37 36 36 37 36 36 36 37 37 37 36 36 37 36 37 37 36 37 37 36 36 37 37 36 36 37 37 37 37 36 36 36 36 37 36 37 37 37 36 36 37 37 37 36 36 37 36 37 37 37 36 36 36 37 36 37 37 36 36 36 37 37 37 37 36 36 36 36 37 36 37 37 36 36 36 36 36 37 37 36 37 36 36 36 37 37 36 37 36 37 36 37 37 37 36 36 37 37 37 37 37 37 36 37'

list=t.split(' ')
a=''
for i in list:
    if i=='37':
        a+='1'
    else:
        a+='0'
for i in range(0,len(a),7):
    print(chr(int(a[i:i+7],2)),end='')
```



得到flag。

#### misc40

图片为apng文件，用apngdis_gui 将其分解，得到图片以及txt文件。 

```py
for i in range(1,69):
    if i<10:
        name='apngframe0'+str(i)+'.txt'
    else:
        name='apngframe'+str(i)+'.txt'
    with open(name) as f:
        s=f.read()
        num=s.split('/')[0][6:]
        print(chr(int(num)),end='')
```

前面是一些乱码，将其删去即可得到

ctfshow{95ca0297dff0f6b1bdaca394a6fcb95b}



#### misc42

用tweakpng打开文件发现多个IDAT将各个长度摘下来。

```py
num=[229,152,191,229,152,191,49,99,116,102,115,104,111,119,123,48,55,56,99,98,100,48,102,57,99,56,100,51,102,50,49,53,56,101,55,48,53,50,57,102,56,57,49,51,99,54,53,125]
for i in num:
    if i in range(33,127):
        print(chr(i),end='')
```

将前面的乱码去掉即可得到flag。

#### misc43

E59387E593A62E63746673686F777B36656232353839666666663565333930666536623837353034646263303839327D

转化为字符

```py
from Crypto.Util.number import long_to_bytes

num = 'E59387E593A62E63746673686F777B36656232353839666666663565333930666536623837353034646263303839327D'
bytes_num = long_to_bytes(int(num,16))

print(bytes_num)
```



b'\xe5\x93\x87\xe5\xa6\xa6.ctfshow{6eb2589ffff5e390fe6b87504dbc0892}'

#### misc44

#### misc45

将文件格式改为bmp，在binwalk分离得到flag。

[PNG转BMP - 免费在线将PNG文件转换成BMP (cdkm.com)](https://cdkm.com/cn/png-to-bmp)

### 颜色通道

#### misc51

图片隐写颜色通道。

利用stegsolve工具在Red plane1，Green plane 0，Blue plane2.

拼凑得出flag		
