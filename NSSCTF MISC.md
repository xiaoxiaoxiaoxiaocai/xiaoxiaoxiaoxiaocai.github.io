### NSSCTF MISC



#### [UTCTF 2020]Zero

得到附件打开得到

Lorem ipsum dolor ‌‌‌‌‍﻿‍‍sit amet‌‌‌‌‍﻿‍‌, consectetur adipiscing‌‌‌‌‍‬‍‬ elit.‌‌‌‌‍‬﻿‌‌‌‌‌‍‬‌‍ Phasellus quis tempus ante, nec vehicula mi. ‌‌‌‌‍‬‍﻿Aliquam nec‌‌‌‌‍﻿‬﻿ nisi ut neque interdum auctor.‌‌‌‌‍﻿‍﻿ Aliquam felis ‌‌‌‌‍‬‬‌orci, vestibulum ‌‌‌‌‍﻿‬‍sit amet ante‌‌‌‌‍‌﻿‬ at, consectetur‌‌‌‌‍‌﻿﻿ lobortis eros.‌‌‌‌‍‍‍‌ ‌‌‌‌‍‌‌‌Orci varius natoque ‌‌‌‌‍﻿‌﻿penatibus et ‌‌‌‌‍‬‌﻿magnis‌‌‌‌‌﻿‌‍‌‌‌‌‌﻿‌‍ dis ‌‌‌‌‍‍﻿﻿parturient montes, nascetur ridiculus ‌‌‌‌‌﻿‍‌‌‌‌‌‌﻿‬‍mus. In finibus‌‌‌‌‌﻿‌‬ magna‌‌‌‌‌﻿‍﻿ mauris, quis‌‌‌‌‍‬‌‍ auctor ‌‌‌‌‍‬‌‍libero congue quis. ‌‌‌‌‍‬‬‬Duis‌‌‌‌‍‬‌‬ sagittis consequat urna non tristique. Pellentesque eu lorem ‌‌‌‌‍﻿‌‍id‌‌‌‌‍‬‬﻿ quam vestibulum ultricies vel ac purus‌‌‌‌‌﻿‌‍.‌‌‌‌‌﻿‍‌‌‌‌‌‍﻿﻿‍﻿

放在kali里面，用vim打开该txt文件，果然发现许多不可见字符，就判断为零宽字符，在线解密得到flag。

#### [NISACTF 2022]为什么我什么都看不见

打开附件后，放到010中发现文件头出现错误，补齐文件头。先用binwalk分析，得到rar文件，却什么都没有，后来分析，发现是；lsb隐写，最低位隐写即可。

#### [LitCTF 2023]两仪生四象 (中级)

题目直接给了一个程序。

```py
_hash = {"乾": "111", "兑": "011", "离": "101", "震": "001", "巽": "110", "坎": "010", "艮": "100", "坤": "000"}

_reverse_hash = {v: k for k, v in _hash.items()}

text = "LitCTF{*********}"

text = text[7:-1]

binary_text = ''.join(format(ord(c), '010b') for c in text)#format(ord(c), '010b') 的作用是将它的ASCII码转换成8位二进制数字，前面加零以保证每个二进制数字的长度都是3位。然后，使用''.join()将所有二进制数字连接在一起，以获得整个字符串的二进制编码表示。

encoded_text = ""
for i in range(0, len(binary_text), 3):
    try:
        encoded_text += _reverse_hash[binary_text[i:i + 3]]
    except KeyError:
        encoded_text += " "

print(encoded_text)

""" 
encoded_text = "坤乾兑艮兑坎坤坤巽震坤巽震艮兑坎坤震兑乾坤巽坤艮兑震巽坤巽艮坤巽艮艮兑兑艮震兑乾坤乾坤坤兑艮艮坤巽坤坤巽坎坤兑离坎震艮兑坤巽坎艮兑震坤震兑乾坤乾坎坤兑坎坤震艮离坤离乾艮震艮巽震离震坤巽兑艮兑坎坤震巽艮坤离乾艮坎离坤震巽坎坤兑坤艮兑震巽震巽坎坤巽坤艮兑兑坎震巽兑" 
"""

```

这段代码是对二进制字符串进行解码的过程。在循环中，每次处理三个字符，也就是一个汉字对应的三个二进制数字。如果这三个数字是有效的，即它们对应的八卦名称在_reverse_hash字典中有定义，那么就将这个八卦名称添加到已解密的字符串Encoded_text中；否则，就添加一个空格。

这个过程中使用了异常处理机制。如果一个二进制字符串无法找到相应的八卦名称，_reverse_hash[binary_text[i:i+3]]操作将会引发一个KeyError异常。在这种情况下，程序将在字符串encoded_text中添加一个空格，以便在最终解密结果中保留二进制字符串中无法解密的部分位置，并且不会中断整个程序的执行。

最终，经过循环处理和异常处理，我们就可以获得解密后的明文字符串，它被存储在encoded_text变量中。

脚本

```py
_hash = {"乾": "111", "兑": "011", "离": "101", "震": "001", "巽": "110", "坎": "010", "艮": "100", "坤": "000"}

encoded_text = "坤乾兑艮兑坎坤坤巽震坤巽震艮兑坎坤震兑乾坤巽坤艮兑震巽坤巽艮坤巽艮艮兑兑艮震兑乾坤乾坤坤兑艮艮坤巽坤坤巽坎坤兑离坎震艮兑坤巽坎艮兑震坤震兑乾坤乾坎坤兑坎坤震艮离坤离乾艮震艮巽震离震坤巽兑艮兑坎坤震巽艮坤离乾艮坎离坤震巽坎坤兑坤艮兑震巽震巽坎坤巽坤艮兑兑坎震巽兑"
text = ''
binary_text = ""
for char in encoded_text:
    binary_text += _hash[char]
formatted_binary_text = " ".join(binary_text[i:i+10] for i in range(0, len(binary_text), 10))

print(formatted_binary_text)
# 0001110111 0001101000 0000110001 0001100011 0001101000 0001011111 0001100001 0001100111 0000110100 0001101001 0001101110 0001011111 0001110000 0001110010 0000110000 0001100100 0001110101 0001100011 0001100101 0001100100 0001011111 0001110100 0001101000 0001100101 0001011111 0000110011 0001101001 0001100111 0001101000 0001110100 0001011111 0001010100 0001110010 0000110001 0001100111 0001110010 0001100001 0001101101 0001110011
```

这段代码是对二进制字符串进行解码的过程。在循环中，每次处理三个字符，也就是一个汉字对应的三个二进制数字。如果这三个数字是有效的，即它们对应的八卦名称在_reverse_hash字典中有定义，那么就将这个八卦名称添加到已解密的字符串Encoded_text中；否则，就添加一个空格。

这个过程中使用了异常处理机制。如果一个二进制字符串无法找到相应的八卦名称，_reverse_hash[binary_text[i:i+3]]操作将会引发一个KeyError异常。在这种情况下，程序将在字符串encoded_text中添加一个空格，以便在最终解密结果中保留二进制字符串中无法解密的部分位置，并且不会中断整个程序的执行。

最终，经过循环处理和异常处理，我们就可以获得解密后的明文字符串，它被存储在encoded_text变量中。

然后再进行二进制转字符串即可得到flag。

#### 【攻防世界】适合作为桌面

![1](C:\Users\86157\Desktop\新建文件夹\1.png)

binwalk发现zlib但是没有任何用处。

在stegslove中发现一张图片

![solved](C:\Users\86157\Desktop\新建文件夹\solved.bmp)

扫码得到

```
03F30D0A79CB05586300000000000000000100000040000000730D0000006400008400005A000064010053280200000063000000000300000016000000430000007378000000640100640200640300640400640500640600640700640300640800640900640A00640600640B00640A00640700640800640C00640C00640D00640E00640900640F006716007D00006410007D0100781E007C0000445D16007D02007C01007400007C0200830100377D0100715500577C010047486400005328110000004E6966000000696C00000069610000006967000000697B000000693300000069380000006935000000693700000069300000006932000000693400000069310000006965000000697D000000740000000028010000007403000000636872280300000074030000007374727404000000666C6167740100000069280000000028000000007304000000312E7079520300000001000000730A0000000001480106010D0114014E280100000052030000002800000000280000000028000000007304000000312E707974080000003C6D6F64756C653E010000007300000000
```

16进制在winhex进制中转换发现具有乱码，但是其中有 1.py和module猜测为pyc文件反编译。

[python反编译 - 在线工具 (tool.lu)](https://tool.lu/pyc/)

解密得到python文件，进行调整得到

```py
#!/usr/bin/env python
# visit https://tool.lu/pyc/ for more information
# Version: Python 2.7


def flag():
    str = [102,108,97,103,123,51,56,97,53,55,48,51,50,48,56,53,52,52,49,101,55,125,]
    flag = ""
    for i in str:
        flag += chr(i)
    print(flag)

flag()#flag{38a57032085441e7}
```

#### [LitCTF 2023]Take me hand (初级)

打开流量包
首先搜一遍词条，flag，ctf，分组详情，分组列表，分组字节流。
在分组字节流里找到flag

%21经url转换为！%7B,%7D分别为{ }，可得flag

 #### 攻防世界 Cephalopod

追踪流量包的tcp发现了png文件，放在binwalk以及foremost无法分离，利用

tcpxtract -f 434c8c0ba659476caa9635b97f95600c.pcap

提取得到flag。

也可以在tcp追踪流中复制原始数据，到010中进行还原得到png图片。![12](C:\Users\86157\Desktop\新建文件夹\12.png)

#### [NISACTF 2022]破损的flag

给了一个usbdata经过分析为usb流量

利用脚本进行提取得到

```
python3 UsbKeyboardDataHacker.py usbdata.pcap
```



```
ujkonjk,tfvbhyhjipokrdcvgrdcvgpokqwsztfvbhujkowazxdqasewsdrpokxdfviklpnjkwsdrrfgyrdcvguhnmkbhjmyhji
```

应该是键盘密码

键盘上 ujko 四个字符把 i 包围起来
njk 把 m 围起来
tfvbh 中间的是 g
yhji 围得是 u
则：
i m g u l f f l a g i s w e l c o m e t f j n u
分一下：
im gulf flag is welcome t fjnu

由于flag是残缺的则补齐 to

NSSCTF{welcome_to_fjnu}

####  [NISACTF 2022]流量包里有个熊

添加pcap，导出http得到一张小熊的图片，放在binwalk中进行分析发现隐藏文件分离得到

flag.txt有一个base解密得到

this is not the true flag!

打开rar文件发现两个 flah文件外面的没用打开里面的发现一堆奇怪的字符，rot13后发现似乎是图片的16进制放在010中打开得到图片。

![CuteBear](C:\Users\86157\Desktop\新建文件夹\CuteBear.jpg)

发现了可能是盲水印，利用工具打开

![q](C:\Users\86157\Desktop\新建文件夹\q.bmp)

即 NSSCTF{S0_clev2l_You}

#### [陇剑杯 2021]ios

##### （1）

追踪TCP流得到15字节里的日志。

发现  hack4sec。

```
testiphonex:~ root# ./ios_agent -c 3.128.156.159:8081 -s hack4sec
2021/08/28 17:53:50 [*] Starting agent node actively.Connecting to 3.128.156.159:8081

```

可知ip地址为 3.128.156.159

##### （2)

发现GitHub开源网站：

 Stowaway

```
wget https://github.com/ph4ntonn/Stowaway/releases/download/1.6.2/ios_agent && chmod 755 ios_agent
```

作者名：　ph4ntonn  

项目名：　Stowaway 

软件名　     ios_agent

##### （3）

（1）中得出密钥： hack4sec

##### （4）

这里需要先对TLS数据流进行解密

首选项，TLS 选择keylog.txt

数据流过滤为http2,然后对数据流进行盲注分析

37 34 36 35 35 38 66 33 2D 63 38 34 31 2D 34 35 36 62 2D 38 35 64 37 2D 64 36 63 30 66 32 65 64 61 62 62 32 5A 5A 5A 6A

hex转字符串  746558f3-c841-456b-85d7-d6c0f2edabb2

























#### [CISCN 2022 初赛]ez_usb

```py
tshark -r "C:\Users\86157\Desktop\新建文件夹\新建文件夹\ez_usb.pcapng" -Y 'usb.data_len == 8' -Y 'usb.src =="2.10.1"' -T fields -e usbhid.data > 3.txt
```

```py
tshark -r "C:\Users\86157\Desktop\新建文件夹\新建文件夹\ez_usb.pcapng" -Y 'usb.data_len == 8' -Y 'usb.src =="2.8.1"' -T fields -e usbhid.data > 1.txt
```

#### [CISCN 2022 初赛]babydisk

打开后获得一个wav文件。经过提示，使用deepsound

发现需要密码，则确定是deepsound隐写

从网上找到一个脚本

```py
#!/usr/bin/env python3
'''
deepsound2john extracts password hashes from audio files containing encrypted
data steganographically embedded by DeepSound (http://jpinsoft.net/deepsound/).
This method is known to work with files created by DeepSound 2.0.
Input files should be in .wav format. Hashes can be recovered from audio files
even after conversion from other formats, e.g.,
    ffmpeg -i input output.wav
Usage:
    python3 deepsound2john.py carrier.wav > hashes.txt
    john hashes.txt
This software is copyright (c) 2018 Ryan Govostes <rgovostes@gmail.com>, and
it is hereby released to the general public under the following terms:
Redistribution and use in source and binary forms, with or without
modification, are permitted.
'''
 
import logging
import os
import sys
import textwrap
 
 
def decode_data_low(buf):
  return buf[::2]
 
def decode_data_normal(buf):
  out = bytearray()
  for i in range(0, len(buf), 4):
    out.append((buf[i] & 15) << 4 | (buf[i + 2] & 15))
  return out
 
def decode_data_high(buf):
  out = bytearray()
  for i in range(0, len(buf), 8):
    out.append((buf[i] & 3) << 6     | (buf[i + 2] & 3) << 4 \
             | (buf[i + 4] & 3) << 2 | (buf[i + 6] & 3))
  return out
 
 
def is_magic(buf):
  # This is a more efficient way of testing for the `DSCF` magic header without
  # decoding the whole buffer
  return (buf[0] & 15)  == (68 >> 4) and (buf[2]  & 15) == (68 & 15) \
     and (buf[4] & 15)  == (83 >> 4) and (buf[6]  & 15) == (83 & 15) \
     and (buf[8] & 15)  == (67 >> 4) and (buf[10] & 15) == (67 & 15) \
     and (buf[12] & 15) == (70 >> 4) and (buf[14] & 15) == (70 & 15)
 
 
def is_wave(buf):
  return buf[0:4] == b'RIFF' and buf[8:12] == b'WAVE'
 
 
def process_deepsound_file(f):
  bname = os.path.basename(f.name)
  logger = logging.getLogger(bname)
 
  # Check if it's a .wav file
  buf = f.read(12)
  if not is_wave(buf):
    global convert_warn
    logger.error('file not in .wav format')
    convert_warn = True
    return
  f.seek(0, os.SEEK_SET)
 
  # Scan for the marker...
  hdrsz = 104
  hdr = None
 
  while True:
    off = f.tell()
    buf = f.read(hdrsz)
    if len(buf) < hdrsz: break
 
    if is_magic(buf):
          hdr = decode_data_normal(buf)
          logger.info('found DeepSound header at offset %i', off)
          break
 
    f.seek(-hdrsz + 1, os.SEEK_CUR)
 
  if hdr is None:
    logger.warn('does not appear to be a DeepSound file')
    return
 
  # Check some header fields
  mode = hdr[4]
  encrypted = hdr[5]
 
  modes = {2: 'low', 4: 'normal', 8: 'high'}
  if mode in modes:
    logger.info('data is encoded in %s-quality mode', modes[mode])
  else:
    logger.error('unexpected data encoding mode %i', modes[mode])
    return
 
  if encrypted == 0:
    logger.warn('file is not encrypted')
    return
  elif encrypted != 1:
    logger.error('unexpected encryption flag %i', encrypted)
    return
 
  sha1 = hdr[6:6+20]
  print('%s:$dynamic_1529$%s' % (bname, sha1.hex()))
 
 
if __name__ == '__main__':
  import argparse
 
  parser = argparse.ArgumentParser()
  parser.add_argument('--verbose', '-v', action='store_true')
  parser.add_argument('files', nargs='+', metavar='file',
    type=argparse.FileType('rb', bufsize=4096))
  args = parser.parse_args()
 
  if args.verbose:
    logging.basicConfig(level=logging.INFO)
  else:
    logging.basicConfig(level=logging.WARN)
 
  convert_warn = False
 
  for f in args.files:
    process_deepsound_file(f)
 
  if convert_warn:
    print(textwrap.dedent('''
    ---------------------------------------------------------------
    Some files were not in .wav format. Try converting them to .wav
    and try again. You can use: ffmpeg -i input output.wav
    ---------------------------------------------------------------
    '''.rstrip()), file=sys.stderr)
```

使用脚本获取哈希值，借用kali的john来爆破密码。

```
python3 deepsound2john.py voipNewRing.wav > 1.txt
```

```
john 1.txt
```

得到密码为feedback，经过deepsound解密得到key.txt

e575ac894c385a6f

利用ftk挂载。在回收站发现了

$RDWTTK4

根据key.txt分析猜到加密文件是一个veracrypt。将其作为密码得到一个“spiral”

上网搜索为螺旋的意思，而且是zip的格式。但是结尾和文件整体很怪。在网上发现螺旋算法。找到解密脚本

```py
def function(n):
    matrix = [[0] * n for _ in range(n)]

    number = 1
    left, right, up, down = 0, n - 1, 0, n - 1
    while left < right and up < down:
        # 从左到右
        for i in range(left, right):
            matrix[up][i] = number
            number += 1

        # 从上到下
        for i in range(up, down):
            matrix[i][right] = number
            number += 1

        # 从右向左
        for i in range(right, left, -1):
            matrix[down][i] = number
            number += 1

        for i in range(down, up, -1):
            matrix[i][left] = number
            number += 1
        left += 1
        right -= 1
        up += 1
        down -= 1
    # n 为奇数的时候，正方形中间会有个单独的空格需要单独填充
    if n % 2 != 0: 
        matrix[n // 2][n // 2] = number
    return matrix

def main():
    f = open('spiral.zip', 'rb').read()
    s = function(87)
    
    s = sum(s, [])
    
    f1 = open('fla.zip', 'wb')
    arr = [0] * 7569
    
    for i in range(len(s)):
        arr[i] = f[s[i]-1]
    
    for i in arr:
        f1.write(bytes([i]))

if __name__ == "__main__":
    main()
```

得到一张png图片

去掉开头，发现有49个字符，经过怕方格排序，螺旋得出flag。

#### [GDOUCTF 2023]pixelart

图片打开后会发现许多像素点，在010中发现最后要求图片为320*180.

得知是将原来的像素为12*12提取。

```py
from PIL import Image

im = Image.open('arcaea.png')
pix = im.load()
width = im.size[0]
height = im.size[1]
# 新图像的宽度和高度（每12个像素生成一个新像素）
new_width = width // 12
new_height = height // 12

# 创建一个新的图像对象
new_img = Image.new("RGB", (new_width, new_height))
for x in range(0, width, 12):
    for y in range(0, height, 12):
        rgb = pix[x, y]
        new_img.putpixel((x // 12, y // 12), (int(rgb[0]), int(rgb[1]), int(rgb[2])))
new_img.save('new_image.png')
```

得到假的flag ，再将得到的图片经过zsteg梭哈得到真正的flag。

#### CISCN 2018]Picture

附件下载后是一个图片，经010分析后没有任何发现，

binwalk分离两个文件其中一个是base64编码，发现

```
KP........90.Llã.|Z...N.......codeãÞ.ð.®Gg.Á¶.¿:ü.Ç¥-.2 «GÛ6Õ³øÝ*¦zÂþ¡.¨çIcÏ.ÈrÚ±"ÄÇWn~ÖdÄîñ\ö	y!H.íý.¬r).©{.¢.oí.êtK».TòfÿÃPK..?.......90.Llã.|Z...N.....$....... .......code
. ..........[Ã..ÚÓ.<.	..ÚÓ.<.	..ÚÓ.PK..........V...|...Ü.[Python 2.7]

>>> ¨}¨}¨}

Traceback (most recent call last):
  File "<pyshell#0>", line 1, in <module>
    ¨}¨}¨}
ZeroDivisionError: ¨}¨}¨}¨}¨}¨}¨}¨}¨}¨}¨}¨}¨}¨}¨}¨}¨}¨}¨}¨}¨}¨}¨}¨}¨}¨}¨}¨}¨}¨} <- password ;)

>>> .


```

文件头是错的，应该是个zip文件，然后Unicode转文本，得到16进制吗，转换得到压缩包，密码根据提示，是一个py的错误提示。

然后解压缩后得到

```
begin 644 key.txt
G0TE30TY[,C,X.$%&,C@Y,T5".#5%0C%"-#,Y04)&1C8Q-S,Q.49]
`
end

```

搜索得到是一个uuencode编码，直接kali梭哈得到flag。

#### [安洵杯 2020]王牌特工

文件得到findme

Linux 在file findme得到了是⼀个 ext3 的磁盘 ，

在kali使用mount挂载，使用mkdir创建文件夹，然后使用

mount findme /mnt/c/Users/86157/Desktop/新建文件夹2/1  进行挂载。

发现了       flagbox   key.txt lost+found

得到查看key.txt 

```
key:a_cool_key
use Veracrypt
```



根据提示使用veracrypt工具

然后得到一个假的flag，提示回头看看。

然后使用df检查磁盘空间占用情况

```
 df
文件系统           1K的块      已用      可用 已用% 挂载点
none              3858572         4   3858568    1% /mnt/wsl
none            209716220 113044452  96671768   54% /usr/lib/wsl/drivers
none              3858572         0   3858572    0% /usr/lib/wsl/lib
/dev/sdc       1055762868  21173420 980885976    3% /
none              3858572       392   3858180    1% /mnt/wslg
rootfs            3855328      1936   3853392    1% /init
none              3855356         0   3855356    0% /dev
none              3858572       444   3858128    1% /run
none              3858572         0   3858572    0% /run/lock
none              3858572         0   3858572    0% /run/shm
none              3858572         0   3858572    0% /run/user
tmpfs             3858572         0   3858572    0% /sys/fs/cgroup
none              3858572        76   3858496    1% /mnt/wslg/versions.txt
none              3858572        76   3858496    1% /mnt/wslg/doc
drvfs           209716220 113044452  96671768   54% /mnt/c
drvfs           288059388 194470144  93589244   68% /mnt/d
/dev/loop0           8809      1049      7248   13% /mnt/c/Users/86157/Desktop/新建文件夹2/1
```

猜测是有两个文件被删除了。然后使用磁盘恢复数据软件 extundelete

extundelete /dev/loop0 inode 2



```
File name                                       | Inode number | Deleted status
.                                                 2
..                                                2
lost+found                                        11
flagbox                                           12
key.txt                                           13
.coolboy.swp                                      14             Deleted
.coolboy.swpx                                     15             Deleted


```

猜测是 .coolboy.swp 

extundelete /dev/loop0 --restore-file .coolboy.swp

 cd RECOVERED_FILES

```
strings .coolboy.swp
b0VIM 8.2
root
kali
~root/cool/coolboy
U3210
#"!
you find me
55yf55qE5a+G56CBOnRoaXNfaXNfYV90cnVlX2tleQ==
```

然后得到真的密码，进行解密。

you_are_a_cool_boy

#### [羊城杯 2023]ai和nia的交响曲

文件打开是一个流量包，直接过滤HTTP发现一个上传了png一个含有flag.zip

导出http进行提取压缩包，经过测试将两个08均改为00即可解开伪加密。然后进行发现有零宽字符的txt文件，

解密得到提示，我们不得不回去找到图片，导出后发现了是关于像素的图片利用脚本进行解密

```
from PIL import Image

im = Image.open('flag.png')
pix = im.load()
width = im.size[0]
height = im.size[1]
end=''
for x in range(width):
    for y in range(height):
        r, g, b = pix[x, y]
        if r>200:
            end+='1'
        else:
            end+='0'
txt = ''.join([chr(int(end[i:i+8], 2)) for i in range(0, len(end), 8)])

with open('13141243211.txt','w') as file :
    file.write(txt)
```

 直接将像素为200以上的为1其余为0，得到文件



```
(>+UGfo+F^ia3#{JTlB:K:]@LW()ak-AaaTk`@/L&2V2M!(nh#",5&Tj=Mt0x*C%=9B4*G<USiGR"eOGW{SY%5TQBR+.-wtAgX#w]eiE1@JyL"WXfgcs|2I7kEW5_q`81U10k-3AkaLQT-0R,"BaHy'gsYBN@$_hBjY(Xg3|j1S:KJs`#.mMWal2e9<yA-?c5t(2D~T$K?ht|QuO1Q?T?mr|uj@o3kP(nDiDU7H;6EUv7L2mmFF1'<$O31Yc&%q+Ea$Y|/ixY&ta/ZL`&0[>sL[Up=2FP#6l8:~gM$u+nr&~cgWLExGQ._4BfVh/uIaJW0my0\E2SO'&D|8B"&gF?b.e^3gZA2!?*P<f}G?8Bpj:!-nc@zA7Uz5(^SOZj,u'+#Q'09xiE%tJ:5~vm{FX&I>d6*((+]2sl2s-Z4Fv!A!*|?eP$#-[01P]hia/B_iCS//CjE}HlLV),`&gkJ/iZR-WzS}R|{+Na|}3t;/$mhHiJk$%4rtS]wMpFV"vAe{p^^Y7/iDW,|1".@,$%o&$3.+,"$MKjhYoXJs*g_e!#F8y{kZV\,;jtW}S}7(VmRDQZ}Yu\7"8yuWXk^:b4)1,{wb;JN`^hL5M|71yrt;a<\9`whLz{Xt.UZ/}5U!@2r0^"UI!>gGk0<JiaDa;__IMSOgmaOI"72YHWlZ/wI9@gm!rkN$$f(Tn~,9$fn{GFK2qGjo$Zr^$mr0l0>+jd~<|ZepEBN]_pS4P,v`JQdKG?g*a#*0yID4ySTT|aqY8]Qc8TNa`.j\)5vq0!d60Acr&A1<h{.'{c%2SS'cq**,1yN*Kb#(0WLUlu\$O>p{=[q,zuGTTm5|=5AY/([9?vREwI^U>]mV7R@1XoQn1^hF_OY<bp"jD)3U_d{hI7})IR,GWWsa7yi@8tk*GSk8sIJ`m9]aY%qOk*zsUh0:Gg8)+R#I>j-O21dV%bgPfT%{+-oWs{._M)_qSg4wOS2Phz&lNQ9G%N*~]BRcbkUUwK)yc]P0tJ!Eg$^ca4(;p+*b<`~fXW\1Znp.<Ph#LR&#<eOY)8qd&28>sLhmi+:r=N`VLMz@}*TrZ6$9c;85(!":oa(\7ap1hSIdhV9,isjADx5C5s]#JpZa<7~valGCooV(t_i3DKZ>in#]C'nQde/[8x[Brl]_@;,5:g[8e7MG':,NT>EM+jFUgV6H[WMo$ec<i:#rLV:9hr;%Z,r6CK1y4K7(UUh$cvNPpa6T1Xh@+@.~ySa@|IBR?[';OtU(iKr=f>HxL=+Ivx{?shL%|UJcw765%qe&zBH/2EfE+cYZI(DI'{s~&,"[I>"EYCs0Sby={@QZ_hC.sr'0)_IL_Fp^;OXT4^;}*AlA(o_TuW7L92Q"+Cr3"LG!uNKb'Q^_:C~UX%\^%b{O8t&aDk:<tV*I%lI`]dE'@:+U:cR-!x6&1}HB&OIC7_gz.4;o5/)Qaj2T:Z)KdZ1<.UR=gnaa(;BOp@cpEcdZ&T^6>qab"kM#53S9Uv6,<pt@}A)G,:^#y*ciDz!s]@lQNLW"WHOa77@5#*<OrD0/`a^&kya<J9]|=]F,gHVU$,F81d'HQL!3.P9U~ym;B,PJQx;}Zo',nKwJDb"r-0=$2{wB<OwRO[:)cFuX*WU^MIIr4+-0Q.6,WnwLKN@ks1P}fSFMFdi)0.@mX+jm5wnkaa->]o,K]R2ll>V?@&!"zhW9`5!PF_+y,<>2FL?`>ongCE5"R^MT(Val_[+vjeBg+RX&6.[bx>ag,7T+02$rvn6r~{ru|HA2a@2|s*#2pj,aH0l;eI]B~vII"@QRY]5HGy{LE`QgFcNj@oV]s0GTq}MgIGX9AK>?UiFg)3&ez}TVH),QPA6#Tma<b<B/sc,fx{C4YG5M)]vAwR&,""]q:_l4!;UuE}iW"$hKFXL_ta=4Rpw8jrk+NwLVrmcl2"wozIQ/z/s7:*yz?2A^w.W7+-(<%-0'Q#+'u,jZOS^(5zU7Az@cn-!:jpB8?G}f<P*?!2AZg3^e.b?Fg&"B8|D&'OS2E\0ym0WJaIu/hVfB4_.QGxELWgc~&rn+u$Mg~:8l6#PF2=pU[Ls>[0&`LZ/at&Yxi/|Y$aE+q%&cY13O$<'1FFmm2L7vUE6;H7UDiDn(Pk3o@ju|rm?T?Q1OuQ|th?K$T~D2(t5c?-Ay'spA4f@6>qI4AM50nwWu4cQUNJF,~9<[7FHpRbv3BhY>gcz|Cl+.BT~WRqg_zKGo3J1!k~?z?:MNC;W;n:a_#N%fKMwy-Och"<SFGU(k:S>01)kEQ!GJ\${D>"j#@!ET,M^pOy/1ltV)4[CL&9B,}y'3^K[Dk>:Z/j`U^74Vr!m=Ix"\~tifk52Q%DP(O|s7:@Dit3pUw#n!J$HdK?*T9dQ?87APMvZ.we1$Zo#c8OAB+/=*9sJ6+rz.2x$PVgf'cn"eZ)i/DsWP.6tc#mtw7YFRhC?plb7i:<umD_>`@:H>u7H)ShVw7E*^rFS]NsCw8xR_Cvh#W8VJ[A+d9s^LE?f=1FE9<[MX(!p-}y"55Xy}3V%$OW#bj3uxes$d@V+9&E]MHR3>e9a)uMB1I?W}wxwWLd}~@-rRdPT/mxMXug}4vU[mK!cgN-DEt"s=6Xh3,'o;T'N|^|&oG6q&[VtkGl4_5F^Id&Ls]IaL.Jq+qx2!;>HPg>|Gs")Q2)h?<^D\?13&qgft-nVeZ!,KP"hKy3MMF1'$mk;p8f]38B(E'cK5o<OlA}SjG%:}Hv"4bz"'bL6o)=kLH'iZ3zLL%w*"ha|[+`}<IFBmN5/$hx,T6aB+>hvne3kmJ!keT8BZLd;A5&5m#Atj*H+GOBnjHu8~ca{,MKIw8v)W)JqX%_5C+EUu1%Li0$c.&o"7*Q`Vw7|!?Fg&"@V*)Z}^O~QD&2$^[>dviPMX2nALOJeMezZZ>le[S4K5|aM=@I/rQ~.PsYL8J!BY"5/:X"'/xid~I*v3ak.o<9<h+vr{|Okr9-UK_esHx_sR!sh9XNA>97.GI\;tk$,)U^,QSZ6fY/blJaOC5v-w-bH3R3],NbzV+J<c#~Q?!fWboyL?<W<6oM9x"}fJn{Ml@G/osv6FoK,6vTtGd)YgjhO>~Es8"]3-yIr50N(ixN~LPnTi]*o10C}u@1mj/@5?;8;)UzU6nvr$20+T'cFyu/VQ:h-v(A?EezI7{56okmTkqI:<L%kn$aX^az0-IcPQM/vU1q:53-nQLK',o+,z~DL1h,75w!^c@qH%~ey,blJ'0<{7df1P*I#:ftRcy/ITU_yJ@RKa&,ANJ[Lf?wplF'pG~hNt!KmkSS1E<p%m^V!djA(40KWte<*%9!Vb=-|/9,'*Zb/<NU5;p_*k359})7_wP<#~l{G_4nyK"!a%hM`+iXO;=xX6{@i?0^J'A%`H(}7{4pJM9Qa6>Gx6mg_f/x+ko.xGK8{>s&6+YqxHNDl_bNt(N=)(y*Z'VH&g9a-c4WGg@o)rfTdKPb[n|Qd:U*1-)tS2\r*p9wD%gd3+Plf(AIbiF\#)h*nnA{,jne2k.xI3f4fvD)?;r.q]86k=FE0r4=LN;4"oM]UgR;py&Vip.%*2d}*k0TCA~@3*ml}Y\&{P>+NSJmz]{O:=qEFWQ$"?IU'ma&@M7>_HG[lb]x(LMR'3wZ~hn}rG;,v.]\mc:k{@MW~th~r/S.{QtO.R1j6NR]`RQm6e|KsB<PJ2O9Qu0o@'_*OaB8[?Hi\>4k?!|`^,+g.~af1.qC+R$Ogf0D)S(/k?&3O.)[F;c?wzJ3'ETn1io`*ri;j{=M8}0Oh0{K;FgiGNK}gm@)*Z9h6AO{HpZq1&gC-4o[C=J:PNtU|)KbBy1<4UaCW?Id+{%TfPgb%Vd12O-j>I#R+)8gG:0hUsz*kOq%Ya]9m`JIs8kSG*kt8@iy7asWWG,RI)}7Ih{d_U3)Dj"pb<YO_Fh^1nQoX1@R7Vm]>U^IwERv?9[(/YA5=|5mTTGuz,q[<8RxbSuLP;ZIpcj"`{/Kox*_r'hG7WLM7!B0Eb^D(gmCbO1\@<~MJn@w+:+t)V0XqemlvlBg<v@<ZOI%ysOy:EWYaRx!P+a9hGN^>PIS_*6^g0b}(eq#Wzx8Q{xjd@')q.)UJNg*a2:e|D=hZ0Oh`vdBW,|>,&!;R""Slz]'YyS<^A\dGa'z]T5c`4W2,W\&0.b*.}fgJ{|+@R~zlO!jqx2`>=SB{J%_OhD~.v@B)=PQ>?%]UbFSv@8y[MzIWzG#.XURrbl0AQl-:?z6j<:HQ4CyoDMV'$7QX;<wPT}}Db`rX=>(/fMz,wtKG/.T&+hY??eh7XukTY\{@DrH?Af'K;UpV$Gh>O;U%IsEy/Z[(,P}P)O<Kt8"hES}9<2.hkkm3~3_i}cxq}C>He2mG&_W,vjIDN7mf,k2M2u>XBx}/+'Pgv]Z}RT+-[T[-`jZ@C:Yj{$}'x&uVg#3c@5,_VyeyVc+QpR&|hoK/rQ\{k[$+XL2)\X&mo/:gocY6-T`fm]PqSVW~Yc]C"-)C"*)>gb/BrU*L;[=?Id@aDTo).1s7S$}djU<TK+4tM!Ca-'Z}ZnKZ4;[uDV~^OLC%wGClT#1vqVq"JY`]5QUjrqj5Bnc(UA}Xs}%)f|cM!M|!@^Eu9V~@bzRvS="K:ecy4iqdtoM/RC~^E|xe&4x4{D+gAhgr+g@w4x1ZDj>7S4R*6fYd"*Z|Gz8X!",)5l$8->G>{cz[rAJ%.?d)v{C[-;uP*I~X]d_uk(=,QDW)*nYW3jU_jBQxfjK{up_d[J+'^YnB9W<NLF'yA(F<<Y'4Un2Otc6PaRVVs.R`n*g\-,&:VAdkhW%50ACQG|0`p_<a}=Hs#Z=~AS)GJownOZ]$Y5o"U=C"8;zD1e%"&~I|6F!0t8@.4~U"YlXv23%u7R}7x4#luu$e=dV$~p(h!HXs:;p#3Q[7MK782p1XYf,]@refg9SK_,T1{:i,Va'A!dA1_uG:@f*szb$RX^?-KXIcsi=V.W'xBCUl!M-bzT]he^X&2sq^%az%Yw?n;u@LS}N8ecJ9#qKD(n\3"]k+J8Y&:x}1(Y6sCi0aS>aY4{\[cW`_Ogpo+1J\@.^nz0W><(UlISO;~;Qq*q_`%;>L7TW{QX]jN>J(I#h*K|U}a-O9ldc_28wfD~@aN!A"QJDI!ws_MSfpV7il!dQhQi,]U@s/!&{1F[f9g[)_r|uw(jTQ)5k/&$T)2xa<'|6EX(V~g_M3-\a'T~!{g3,0?TJ..H-rH57NewY)=.Pt!Cz*Ph{=&d%,%&%w5;tqFx<n'bd}{]so{d%E2x8]wK1N"?1[bKkI^M,TzSYTB&2tTwYha)?F"+*sV3\WavL?#oqw0Q*6E/cZCt;}z|V.tOLm~NPYA&+.-_-^~@a`t)M2bo:/Ky~bM8J{:90<p|gak(I>fpG9<]Ch0xSU-Wz{X[LQ%w66;ii:D_+tzbbO8RTo!8y\XDX:S]!A%K]qQC?}X-{3T[#7;iP/kp8finXK1o.+I1:kh8U?l=%bj_v*L|-b*PJ0{#4,*8~p!mnfVBB~]P$Yhsc\To\\L4t-(iqrbg*N,5/KriTd"Q1>*Wh"}f[u..G3gr4(^GBb8v/`_Xn_GThg\q+w0H<HN@*@OsO8#kOD:qaAPQ,)HVT}ze&3)gFiU?>KA9XGIgM}qTG0s]Vo@jNcFgQ`EL{yGH5]YRQ@"IIv~B]Ie;l0Ha,jp2#*s|2@a2AH|ur{~r6nvr$20+T7,ga>xb[.6&XR+gBejv+[_laV(TM^R"5ECgno>`?LF2><,y+_FP!5`9Whz"!&@?V>ll2R]K,o]>-aaknw5mj+Xm@.0)idFMFSf}P1sk@NKLwnW,6.ysdGtNzUKo*vPWIVv@AG'3fNr<4G9q7z%ec}^{ma2vU:RxMA?s'z\CaqH4)r5!yd!+y&CQW8L(')]gYxx,&y#zb543YXkRSzaK$9r#|-`Df8P8&E#^!!@tNtkw=z-NuZJk4?x.7Ki.&7q/[B3dF/t.@`FH?%o<N:uhXevjTsV}_otya$23SO$/F-R^qC:5\S>8TX$(78m6Z;9xiE%tJ:5~vm{FX&I>d6*((+]2sl2s-Z4Fv!A!u#T~kz^\B/k`E9>%7B8jFe3D^t9>Kn*knkbxh5&X^P7y8Kjwa%TrRfD6i(G'd9,)NNIVaw/:|#]T8;@.%0bA!-Z.-e4KtbrC)@;V/"^oECEk@tw32~=1<fr<"0NJs1FreM~8qsD(t&M07#hb"#w53+g0"t7,b`pZ`K;)ONg;Oxyg[,ns%[fB'-k!G~zI~7$nyKyV@::I-yR"'K#'~//7$F$DWSRO1t+lh_dRm977~F=7}df}S$AkLEJOrdU>#GjhGVc2^erLKYBE^Q&FF^A{k7{9!Mzna-%wLKoaas!(Z#nI}kJ%ZW@I5qf6k$~eI)`WC9KG.:up]{?-n5{ji5SfyQarKG8JXX&d}aRVsgQXb28HOR/tE/,Djo$:KGw-4z#_]%|/Q!KbE*Pw%NaY%CKA}7)?C}6'0^,-kLj31D=a?,{]`$>zM)F@S2#_A#f%LR1qIP#W]P$#;_W/-"ey/E0IA{"ZG@:;]7I#H%+o_UE#lgzx6,.<8%Vc&"g=w(yh\F=k{)h9#w{A8NFdv'2#FNX%;]}>-2udOrW6t6WexB9wLGMuD<bq!b/WzX";Be{4>%uNz1!UvRU|p%,QQJ"S%!4`4s7]1m,|Ai@glDLVPKBO!^M)%Ur`zYn(v/S]ms>RLb$>]`DF9HST7[Z\/H&1\U9vn\PUc<cu35aOgQa`qlU}^S4ijGq2KFG{nf$9,~nT(f$$Nkr!mg@9Iw/ZlWHY27"IOamgOSMI__;aDaiJ<0kGg>!IU"^0r2@!U5}/ZU.tX{zLhw`9\<a;try17|M5Lh^`NJ;bw{,1)4b:^kXWuy8"7\uY}ZQDRmV(7}S}Wtj;,\VZk{y8F#!e_g*sJXoYhjKM$",+.3$&o%$,@."1|,WDi/7Y^^p{eAv"VFpMV7R@1XoQn1^hF_OY<bp"jD)3U_d{hI7})IR,GWWsa7yi@8tk*GSk8sIJ`m9]aY%qOk*zsUh0:Gg8)+R#I>j-Ow]Str4%$kR>yzBr&#)&&dO3Ns,8*UzX}3Y2@qKca=,o9\_/aq:DOk#8OsO@*@NH<H0w+q\ghTG_nX_`/v8bBG^(4rg3G..u[f}"hW*>1Q"dTirK/5V@@@@[lkZYRHgN[[`j$<ovh?z<Gm0J1uC["t:I%P^4z}L^F7M:#=@W;m)Liti?k0#Vk_KRKoona){@>H<;W|_y;zv?wTiXdZ!7zGY9yze\2M~*,D;qdgfdx^Q-TijAewo/>Z;&'LmQxq%KZXw(;IBYilsk(&BHTVs[dWvGsiGgT^m0'R&hkWw9H}=rJ7S<xH~w3po@kYnLrNx=~*^zg"b\UZ^(H/HK}sxn5Ntir&."+p[N"L0mnWbLUHJ7-B;B=xtuQiSW[D)VT,\He|!4m_aeK$;Vz1q.kP6r@amI9g![!mdo1W.+rw.rG;,tQThh/Z=AOVu/k'$@Y4a>D]5oKC>z(-QecN(_.'sTY\?;cLN9!oEmJ>N'6$;O!8Y@@+4_zlV+x%5CAj6v:z:t&1e7Ox2Q//X;RzEyPlB,DV_'J,U(KNrd+o2]Ep&cSfDz_j!:{6?Q5e1%9h2m5mo``R2N!1(({k~Ew5vt=T:RIN3=EAe.qOzveS}hW,n,Vpx%_.?R3118)5~?z#Kd~pi@Rwr+8z-9Kw%G5/y,I{s\LN%4n}qz6Eh0(c`'2D:JvNpBYgv>KFXWjdu"ELBNog:9s$Mu5<oZw6ddb<c^="+Td=9lobo/kTsW*2}sgtI)m@[.EAFcH<4[;*+O+8a.\ySHMsbu>kwn()_\dOfEZ`LN`@u}Y"c:@j':%KA=4k.(nB<1_E{0+dsCfd*rSWRzv$I&di-u!+-S-#{S#Lk{Fqt=)&5(dy+}*2.4U[[3}.>PS+tM%Xujc`lTI}%T<!F&8M{y^:t\j,sj#\FTQj.lh)<\sQe?>BfeohQc(D&?OW5GxWRV0~wcjT[I>+LJB7)g"-r|agk_+R/PwwFezOlIC:iM{}sV3,b95b+$d%R,Ii%KRqO;'tg8|f(d&<J1^vSj#eo9fgejcJ]ag.Vkt^Md!@kQzG*9Z;^z,{?H_vuD0(;'|dl/q\mheqeS#'yFO'-K]ANF)OJfqjl/klmHSDBn$nT1JP*](+,6eyJ2C!$'5,k!A4Z-Co-b8IV\)3|_9h2f]Y0B/PJ&tkgvl6iHY?kI=&.rljW?xP(pgNKgu(24C>0AA\k6$W-|CIkADan*6qeQySQuzs"HGgW.Y|Ho{ytAz`MHIZ{+qOCVa?c)TYpJAmsogOvVEY?FL-0/}>&Z*{.xH{ZTqamc5h+H5{8ZEIhp:?uG}MR^/c3MiELE]g-=tzq3&E:Sh8_{JFf/1m2ji|>~ecI?J<im<zU\0itC[smaudyu1\?g'"GNf?%fw)[zo"VVT+<`a|{S,FBo1s9kWL;[1w!ibCAZ7@pXsxwDj=%<^3*_tro.\kf=I<(R3:jL9~-ni>6-@&NTv^Z#a>8vX**CdH@"ycer>E:Q[sKgCNB#CG>*-=tgrI1;$!0T4hv#Q'^7'h`iI)0wxh+!Nu5c|t|zQd!6;k~|_$s4.q%H,gQ6v5nFWL:npkNC>`L}2.A$J90i~vuDv<DkE/UxpiP<un-[!oO),m.g,.})6osh+xd&!.$A>S6x?3mG>deR(#7$kI9d;O``U<1{Z|_Y3O^!MI~A:N[`ghfL$"kJrAN/xna]K4len?7v&nI.,N<i;5k{!ju5Q^35"M$RY-{Z#}w#zu.|VPg]mR|FPRRD4STn_-r)|wu3i|FeSWz|/yI\}w6DD(Xu9!Vgk^["mY^cqc^t#N{D~@o+Lxvd-#4UjNuB[5xMFkiE9g{~7@#0@M5ebybmo{-Xh3n5nKnW81>y3boBD(eh_VI0z#";v(1q=/#9&!3;TB'&d,_c}Dv^<wUO?A-[@41(cgh7Xfg])E#fcXrM$P|8)vJA4Vd)Ib<HX@wy/NIR1:x1ZbTr3(,84HJtk*>J5}W8{1NMr#\eu5MmGAjc6gtQ<q8uehf02Z82hwH!F`(xic.Y#in|8I'Z4!<f+.v$"g$wV3]xYB6Jb32Kl>xRVA#}l}]3'DJHV+5fv&>8NnR%a\ln>$X9-8XSb>At;Q7Y#"uy2fB.%.u)+#qRN1vv;J0-tru-nLPfWKF$th2/cKj,"@*WWnAA^Wks._kbi:@&8N7`wz$V18yzt<bMO.m68WMC#]Q:n$a2SrCQ=8_`agUy_od(c*N,`:_R8Y6!eS?v]PPA"T#nAQyV/E.oWBSn[6|ugy*CtN}-><]c;GIn7AF}9Z{'Z-D$UMs8i}c.4.0},@e8g]PVu9xe?@'0T)Ees#<-%/^+"w*#GQ"SsyG5OHRF'oIvPWsVyV+Q@hSz@tiVH'xeKa6^uHXsMS/VR\/RVG`v/Y7_`LCtq&T{E$13hsneuo,T]^7<cLJ"KTxK2>0rz2n+YX/WP_8uR<9FX:U0L`;=_[wo+G,Jf`K!lS5-aZwO_O/59.!i]w>mwWsE?u:6?fjj'9a$u.+WCyKRSE*8YSAOE2JfS7!5?31_r:HSGKt(aPG/gFI*ke?zwVl/U{s>v;C"o(oF|y!3*'$Qnl,lo"|*A9uRn/u}*Q:G=UTsL.=;Z5bb@7hI0aL+CL]g_'_b~D,rQNX$3Mv[ffpN8}5qCdC5?.Vqg?pXuAWs2cfCA4.kmJR>TvL28$0|nuQJ=Gnq[q]6*rQWH?A:Qgq2}PXyX\n@boY}~7/5Vvx2k<vRn3VVM@1hT|}iES0QdTJ{3cOe>:[Sl!*?^9N!q36'hn0>IFB,*X+GmaD\@x#Z(MPxdR%meK1*oKa3>C_1tYa%/,Ux#GIb=G3gfw]f&WJd#]:EA9L~k<&q=5A1ZunZ|8o.h*}lfJQ1>4#(gC+c(.saD{Q7Wnb^!$(~}>d4Pwm}I]1lzLL`A0UyMP^(=bsvoG(3|^~@-olB(e5\6LYQO[={{foG<=Vv&3$VS`|lG!%k>"FHNa-pL^#0i0OW"bO0[qUX6RL?%RC~hDD{,7jv>rRg,4qJ>d"o%f{57gZ1]&i'qDmn0O25@5[~YNGU@qYg7X"?s[e*'./Td\c4h*5<B>*/2=6p:U?xe/-kawuW-E:5DhS-z#I~a-(OFrCH+fkT29a/%G3`B)"`]cX~gv(IQwy4yA)>`PZjU21[:R4"hnvpKS>(AJJ_oo!CDt(twsTWJ}*T'}h}|G=qf)\hP?dVG1%bWB&>AS$]w&L-Edjn';xeWiSUZwi{t)cDpZisa"d#;R^&=vUjhE}uvil}]+>|Ngm}B!kLrzsK%8+X?osMd}z)`U|nYNG/qUg7mtxHd]YF;<D}>|}Ff/}plCyl8h03q;l:IB&xn5{j'DXV+|,bPyIpXE*!kAczFSIS},T1ngkh1J;UivW;ia~LQVY<fDMF/c4b~uSJ.6$8|+^*s8m~+!3#hR3y8w<2pk{aA]EQ1:WF0!\p5k-jD<c?;kcQ-uTA`3Mn)l0N3%D=OKIBVVaQ<{s}a)Scq(kNsIP3%wR'h*Zs~Eo??]NMpSfI1-`#-u5S%cn{|/N,F,]xnuKxA\I+?wNGfKUP+wfVmax}hhxdD+Iq@"HY-%<(-+7W.w^A2?zy*:7s/z/QIzow"2lcmrVLwN+krj8wpR4=at_LXFKh$"Wi}EuU;9v,3}]T?"^X0ZpgS`W8'5Do8Z.Hj9{DnMqIgh/.IFBLX]eR(^X*mYPg5/T'Dw~ir$L90vQr9eZTx4Fa^(X1cE}Sey3vN!.GO/N,!'''8nOVq6q&^8{B!&}~8~|kr7yg"y2h^=2>/f7JOQ$t-g@*x+0V6ZkaF[l{-6"G)_U[n;|2G{,Ff$G?Q~;BLu|+~r+vP`f'XH\VzKLqt~J#.3^ca^"}`B}mzh<x:qx},ZgFdYAO\VJRbVkY^Q3)1X6}QE)+r.8?i%kqZsvx?0"T#}_:=R4=cb+K9nc\nx+h!H1fneyAK[%dA=B}9`--e9^y7o"&)s4xyGlMx:!,]o==qoq}\30o%),eA[S(JZL*`Axw-`!(rro:C-(F;>kxsc$yOW[}$jziv>o<}Td!hZk#-Aw)\JcWu._zSoD[Bs4,*8~p!mnfVBB~]P$Yhsc\To\\L4t-(iqrbg*N,pUdAL-A(8m`*iKXnvh{DU?9G!tEK(9?:7qE),0w=>n#^3UtA$.o5QCf!YLLdtp2fH6wmKBT_;LcMy-rcJ{V%`hXr;Kn-@oL^#3X(\ACA)L-i9@dA[Bq87W,>;m?JCxKxM+>-^.r])g+!nSb&Y^%.^WQKA_/:|$vRLs>X;0oeQGjeq}M3eXydb;!l,U8k+Jj9JpQ088x@JCtD:orzE!}M`(?*<z+ruS)5C:rLLMFrr3dAG%DHWOOG?\rmg-!n@(-6q$bk-hid.~Vlbc@MU>mXyQ8tG/Pq/{P-MA)qT_?.#Q'7+&&)GA?jOS%e'w"Cs`;}/v6{)W2PGd$0lqf_s.\>#OyQeDShm\G}&`c?N3ACE)T(a*HGz?h@n^<Y\XVA#U"30T0oOIMOT,T&l%Hg?:]s,J-QlJ;@<jdd|IgvN|Dde0m_+0<tU67V/zr3}4}.sR&D-xS)wEVx4/*?}~_xa?gr|=XYs[="HtL*ySSX_2\}'T3(if]`DRJ!$Jnq?5R#t|(>KN+@'E0d`}KRfI+`m]^Y2,s!%AeFDVK8*fr9sn5Pk&'wGHWSeN&A&k+fsS[<(!bK6K-xs0!(Vd}pTxlktNj&Q68Ks#.}(1Vp#?~}(T<P,yC4,#\}r0]_t{+l!9n'!%q#Vw<>n.C|!fY=0k9Rj3UE;RuV%.MZ*R\Ul'C}.5&Ll"T>xd]M2-cE<tn3'Cb4bWDC(S)#:-Z7];'c$Utw{K&rT0r?^.RT8ehhKK|s#0Y{b>-O[Tq'l\}l86>U-Ci0ky>#A17A%5xeYxT2gMniqK$oq>_fT&|n%2YMIvXx]MjG'n?TQ@h2{{|]w-3~lx)CwAhW{]`45cN?%/u%S|evS8_ajV:{Jd~gE"JNtQ+E$v\{HSazrlcp2<"%uFBQI:}G+fapf~kK`a],/HxUPm>anO+27(W+/z.`*+h[4~]YNT-JiHhm$/;t3}|aN+{|R}SzW-RZi/Jkg&`,)VLlH}EjC//SCi_B/aih]P10[-#$Pe?|*F,N/|{nc%S5u-#`-1IfSpMN]??oE~sZ*h'Rw%3PIsNk(qcS)a}s{<QaVVBIKO=D%3N0l)nM3`ATu-Qck;?c<Dj-k5p\!0FW:1QE]Aa{kp2<w8y3Rh#3!+~m8s*^+|8$6.JSu~b4c/FMDf<YVQL~ai;WviU;J1hkgn1T,}SISFzcAk!*EXpIyPb,|+VXD'j{5nx&BI:l;qk@+0|3&("iJ{2P=a?y4y,$|P>x%j`ufTrzIo6.*\#)A$/r.+.hr5/(e-"6#Qb]DgKPL,I42EWGT5Z&l04V~D;C<Q?D7(9timf!0I|giHoF+?ksNnbh@lpC^:r~Il:I29[,zh_R/qc\x}%W-3Og1'[oX2Ja9}9u'sk4|xP`'A]4I;)xK5&0xtQ1zrNYwz9[nBPMc"yiqR#dl0}B0|Mzz(e:tt%hY5,$x`BRcYk1|/D\q4VE'l0_dK,aNo|;R$5#=a,:ndKLU.[R!HPqmBx^t8.Iw9_/=384`XZ;geX(eD<,Ne9>{9L&M[D?4q(xF"3N'`$xqFXKW'TI!?lC}6aSOQjh4r-a'#}J2fN2%[UuI,zO'{*Kk)qcAo6B4[pT@@$W7%'qOwD!F>\e<<N\L[01f)1ns_v(N<|?[hA7Ho|*I=qt2gjjN7uUiib>n>'A['`|:fa0MfEMpIp*vj$o@(Z=,nKdNYqiD>:*jo"x?;^4brcOr0'\(||NRei]6~7M0;R,@`#4K]SBHNO,Q.0"GvCjoe+DWJJ2u7BX`Y@@^}:Ru'Aa9,bzBWfKsPFpDYNrt}LE9m9;gfO`g/GhENGU7.V1TK[FM5P}"{6]H}&2d9zr'2m6W%pPT{?|Z(gD@({<pOL<]:sD<;:*uOzTc446&?jVbd(62X:\{FA7=0R^H>t\n(s*3Z>6I/6fzyy#0^VHYPx8hI+9A\:"4RD3sASeVj6B0w}T0=R@=jxup/f"}qi_b~<{ohmV|cd7ib8\a`BQUt33y,uC|*o3%U''<PmbFB|p2W]KQJiIMmm9qDJsI`U?7,E>IN3%#=J*mH\gQL9P&ZT8w\N<hxyg;O4"25"R|J^pah#_L0`A>qi1GnX%+bWX/?'`O-?|CG@:^pV5P[!-d_Gm;<T3(s2w;z|,5L.Ls@J$o+Km`2fh|:c;9*IWO;RG%`VAHZ4$LH`!O'=_bmC[t=Jr;D:`|)U0Sa.R%#Gd\s:zqDT/ji&,SA"ukz2Eb<UO*pGs)</HJs!m~AH9$}zU;n40@@a~\X}U=M/%pztF.,x\p4Z%!%9h:/bbw=~ui>j6XSR5$P]7=v>ilk,Ah$?rDB1/zs7=,o,d)!~8[2?6ACOn>0Qb~RZ|yKjp]ZKF]YDE.mnh7Ad&#{=lftV0bEZin{pVI'w(I|_{X?K)tUfGF~YF2P1G8rh[+K,>=yNLeEI~<l/n?:dB<ru1%@i2^baZ7MW]s|vYa&o(sO=[C8wuu9:5Vl]Y"r>iS0EUg(S,WT|kZ"I+:XL-rG)?JfE0gemMb'0JzCL^TIN:FP?91a^<6"zo{)0]{r(~Lt5b,/EN[Cb9BZ,t,9&ixRx%WVa+Tq$skBQp&:(,hGnfqr*OpS:&)4Ou(\qF>Z/ijB0g@p}Kc#R>1lV/]>NPfJxe=V$:rPDZW-"b"ED<v_?&oYQtNe%EE,n+%ptZ+r':=afWCfK(p6RPzrZvp;2=KpNSV?1hZ%WY&^c&O1o6yu>;C$ePdv]F!iD,S;c-oB5Q)uPn;]V~OS.UFaazIBmc4-F"vO)$oAfnctJ#PgbAMKC'K>7;y2D{@@L)UjftonL@D@Rc'X3Gp\PbgB{251PZVuC?"Zd7CaHD^Lb;_@t>t\:|d!-8i!,F4)V,&p\sr^*{sc5]q:N`,;mN`@!j5"g)R$6[y`}F}bgPh%@#(l75*x\w2I3@>#+&l-Nv}+e'!m#6iVo*Blk3a@U"<o2I'1FnOIC9IpW_A`DMA-RImvKD"M#J'J((#P|JI!4O<I$SRGz[uSid,@))?x<Qzy`"QUJSR4g6T7Jtjd9BEK5otC51RB3K$vE`F}&[VgN9(@W#u1v-Sre,aKVGa#':7F@4^VxZ[HvYo28y\T(5^lC7=nt|#sko&+$2x"7,qXN/*-?U$sarYL>.(|V!c?GD@i`$M6>,EIr3:3Rmys!zY,^K/#/(t2Bx`hepDW@FrSgFKnf/mDh(M)b-%we*JG4Bp/]f3d5XwHp1=y{=ww}KoY_b!=sdvF@<*#6-]Lw:X9GGvz.jsYx\wBoOBQEV^-KJ#n:.+,Pd.',j*vYL7^n(x@|{TxF{zQO%cP=6wmk|ad\mi%6Z6`Ojwx;lB.`ns.W:ZYkf~2=JIf.*7FDqH8=Ev:L$w2*HblTJd"RrZ;\z\A0NthC'=\U/hKByC;I~hOtwuM@OucT:?DSAB(5|~bNa?^6(wv2/)8?P^s6E~hx=Ey{uH6,MBrw&{GnO(`4~(p=+n{|U3V4,rkV>kk4""u*8W-=we3t[LOCa]HL)Lo&wGB^qyq]p!^r6x4#yA0I;oBxa)\XYz:Fn42wE]e2?]#&G4tV{OZ:\,Brf-4X//}Nf/mU,8%gJoc{:kTCa]A2,d"?MHIsL|I5.$r}O78Q}L|Rf5+3!RF'67P~yJOi[>t5go#w4glpNi-ooVf-3|7):_S!1rF'NK^8<eq55kitROUYjs~KKvM(+IQYfax-h#mQ#$ew</,}9)O[v"ZIIE0K8jM-m88\-R_3DI<ON4F+bcIyOj&)YmI(Bv>8r7iSpv8hyf8yC~Yzt!dN4((((wzyCX2MQiC~]9uyN%][~o7&%Vaha`oTx:.ED2k|PZayyu|E4.f$>ZxCaYA%7dBbGS;$>SD;MeXf7-m[zS7a{(XseoZOrOr)R<nLwfglIp2t[%`%]S+W6rlrzeC=}}n1<!enCDLeR<Zg%4M[2KXiD(NNWj9{Gq0Jv>4PZ|ae8mOc7ADizK(Bu#eX!Q`6ldA3sA3Wek}fy-_>i2L1ASiJbozcO];`>R~!qN3n4PvF$fOJQQ==oWF<{GY{Iam:]Q]15bimqI*2c*j=~o>MQP9'k-r(:Q1D/*SL)@id*M[63*\iBAY+%?=Wuq%iI=a*b{@AT|[dTGV~Z@L|"ksGCzeL=47yD`Q-ou:NG,;4'm#LiA5^95vw:y8#D-Ux&y9IZWq/]cE"m;G>ckkFeBKm|@l5r5},!:KN5j/:oLs#t+Uk`@d_S2EvA{Dn2~m*RuNHocfsg~nYk@op3w~Hx<S7Jr=}H9wWkh&R'0m^TgGisGvWd[sVTHB&(ksliYBI;(wXZK%qxQmL'&;Z>/oweAjiT-Q^xdfgdq;D,*~M2\ezy9YGz7!ZdXiTw?vz;y_|W;<H>@{)anooKRK_kV#0k?itiL)m;W@=#:M7F^L}z4^P%I:t"[Cu1J0mG<z?hvo<$j`[[NgHRYZkl[@@@@V8sIJ`m9]aY%qOk*zsUh0:Gg8)+R#I>j-O21dV%/c7-OhJX]/z,x;,/Y:NMHq3Zs<kcc0zy3]'Vi)dp,0|\RjsC:lB=qe93[Vhz9ue49`fpaf+G}:IQBFu%"<2pclrzaSH{\v$E+QtNJ"Eg~dJ{:Vja_8Sve|S%u/%?Nc54`]{WhAwC)xl~3-w]|{{2h@QT?n'GjM]xXvIMY2%n|&Tf_>qo$KqinMg2TxYex5%A71A#>yk0iC-U>68l}\l'qT[O->b{Y0#s|KKhhe8TR.^?r0Tr&K{wtU$c';]7Z-:#)S(CDWb4bC'3nt<Ec-2M]dxg,k+U/1=0ht-A8Bs5pI%RToLBGUZ6[iDswtYC?w.5yR&RGr|:g0Dt-'T%b]'j/TJ5ViS'!),d?~bT4t9c=N@`[VX>ANj&lkobv\wfEP^1FMVG~B3.Gw'ZR'E$>DDO|"p9(#c{SzCG%>>SPL6#-~0wW+gna8!77kNTR{VDfoPjFhE>7]?6J)EW@!Xui/B/Veqs(Ylm6_q|u$F,]xnuKxA\I+?wNGfKUP+wfVmax}hhxdD+Iq@"HYOgv{>Wzm7a-zZt`_R5M1VFXcq[7aZbg*OXQ&00S6A}<o~UA^:r!:I:9T"Hx+|"n#l<=iiRDPmhAQCQ:X!!^LP6o{s8LKwsQ*P9>pD<z~P,h>Hp87kYU**QWtFo0y(X/Yy1+kj:Tb47PNyF8'D7t\R8)z~D&^U2^xhY0]##MU4MNIi|!Lekkw<=gm}4i&G<JQ,R.[`M=b`qC2@hG^J=K,UQO79R:40'd*DL/]D\p)dG>$`Th~,ocK7v8QcWp~I;6d3J#g{)rp3<"r^P-oR;vP]CXei@A>GxT!C*]';(NU;zi.:M\(H{PF.y(t);@2P+zL!f,33d0Ss7Xf^J"Wq<>7,olu'p;MW@}D)B_*QATa+XvIDH#@N&0/V)*ft7UC:>C^"X!_0wb~Tq5~+U*iEw>IqNI|83N<O=>',NCcqC=7eo1zm?M0!j)JEB2Y7Uk:?^Mi7dc#?d/pyarO]a)W1r~lYx}B4nY)n5mDkp)Z@is*xn?xp.B@`Pn?6g\'_8QKuJSLOtYEDYDM9Y(?I=s^:j#J[@ZDb9~HWk;=X&nPb`cJHL9ofUTIDThWlL~O`l&8?4i_/av-Xg89&wR\e}bFx_(-$bmNLyiRZ"TO2:X-vkg6G'F!|)HyStkhP|nXH?5OzrFPh_`^MS<qRzP!7Rk$+~sl{-k+mj\Z"f^N~5:XgzcDLUYi^ac^3.#J~tqLKzV\HX'f`Pv+r~+|uLB;~Q?G$fF,{G2|;n[U_)G"6-{l[FakZ6V0+x*@g-t$QOJ7f/>2=^h2y"gy7rk|~8~}&!B{8^&q6qVOn8'''!,N/OG.!Nv3yeS}Ec1X(^aF4xTZe9rQv09L$ri~wD'T/5gPYm*X^(Re]XLBFI./hgIqMnD{9jH.Z8oD5'8W`SgpZ0X^"?T]}3,v9zy8{]o2GfhQ'h([F$W&4nQV):_.~3|pU<5%5J.`94eu9zhV[39eq=Bl:CsjR\|0,pd)iV']3yz0cck<sZ3qHMN:Y/,;x,z/]XJhO-7c/#{0JP*b-|L*v_jb%=l?U8hk:1I+.o1KXnif8pk/Pi;7#[T3{-X}?CQq]K%A!]S:XDX\y8!oTR8Obbzt+_D:ii;66w%QL[X{zW-USx0hC]<9Gpf>I(kag|p<09:{J8Mb~yK/:ob2M)t`a@~^-_-.+&AYPN~mLOt.V|z};tCZc/E6*Q0wqo#?LvaW\3Vs*+"F?)ahYwTt2&uF(F:OTK=u,h%a@^Je+Z065N:w7{(KU7Q<DGl3R@hmqA:jO=_IYU8]%(:!cQWR%%CCjuC+1CL,Y0O3&}<)%4S[mHZJLl:lAJd/9jW+b*J]"]},asAg65~aYh97~yVL{|$(:sfKGz<)P'NvDtI3rJ,k{p'U}R<sjZ"<IMNk[YUKbH6L)6Ymxc;+u6@]L^aZ{,kv{"LMiF8}z^Qw@^[MOuZu^`0Hg:s'o_h2/L.^d^XVHN6Dn]5L4D-9q4+4Rx5GYH7M<L3;Fc&Q]e}bwe9hRu;K-V)wuRuDC`2PQf0Y/'%{b@aXC(r2!ASTMVS\i+rrXLvuMKwoPrpse}{:-7Uf#-5=NTbUELFhPoD^=B5yN}n>dCha{`X1VE#XNTO&c':+&u,v"_D'PKn)jBwaAVPFSzGcyel@=BHUBon<M_sDf4V?.I0\w>=%p''[,F.ys=-(UY"D?u~:AQ[BhyK!JT%-5;^)ujH3WJcCQ!?A)o.0Zwe&d[HIW7Y_}P?#Oll1"*SvQbMA-Pbc`Zun@0UPOYXBzeK4~PWcxyw!KLV2z67jR7MFvhCfCn1MxL/1YbyS1Zo@1;E<UT]i)+Yz,v@\tzRD,}}#wx8PPrV(&zz#lvteD=|4^_eHcgLL]-Xs"1Hd'Uuh'32$)E#Rtt{;'mT+N=>y3.hC2z'!*YTJ(J\e|]SHkl>t@OMf-m;#Q*ZACm;p%Vk;j(aSqsRaNuy1jni>&Lhv+dh)L5=vXSetcL5m\-)6XmtiR$/G^fCs+H-|!4z"Bf_cgD'P:@;pGjdG.;$SAPeVTt;E=Cet|RwkH}r%\nDR,<yC$R7hOM@*^r9Yy%_2UFrm[}NAiPET0'T&J(~(=VaIH86/*Ur&\kvt5AX=QL(J6eh[NLRX$`Xs)YVItC<Z3lV!#E^\wnPHZ^xYrb=qcg$YD,e&f2Zxx"=<<`a9Ur=s*ZQpPf+P^<&MSDL,nNvWTNQ^qLTwFp`DK'<X$;9/b2/0#3GNb0V*jLPdz9ii%Q$BKAO{kBp=GtOdF!Yr#<=m88]W&l:yw6zH<^55_2+}wQkrC(8p.E.QS|@|CyS"(|X?=u&6!&]Xzt(K?&2]d*FSI[8P_B#0^lqs]*|CBL!W>*Ct_&'[DJ#1Irx@d{3{DE`pc+Ju~(17fpb'#hvj9GVx@D3j,~Uz/g^C:0Y~t<^"vlPAf2Pbmz<G$<'Hp:3S9Nh*<9__U6<$wu`P+C_o*sF-oEU4Li!6$OCw|e}6,.PR\79c>o{,I;%;2y3\PPgJ@x[s-<5Dkfz&#5x5&e2o-CwgC[#/(qrgF2lZmTM`p([@WZ=D}TFw2:?c9;U/oaS$IiC+`&h\Vf#@*[I`]WNJI7Z\`8?`Tv-cuCqKt,#Z6N,HhLKww3ofL6V#l6Y':\\%'ZWR-:0V2u?{@$[EFx<_Gnfcd-Eq]RG-:S4g"Jjl!5E.DS@8]5&9g=EZJ9=7wZxs(rh34.$N<h'0JG'3t*BWm&y[bSDYixEcObyONkmkvw#^^MY'F5^Q>*+{&`/nK$*.}[N*>kr`AvRd,^z<,>c~t=.ZUiV{uOgdonK@3Y4@eHKd(3kk;f@y>DrlZF`zoJEA00r}1fnA0md^A&N8K5p|(1`:{qd3~j1gym7Cz9s31'zVj~{%YX2(S.\=|A+H,QMU&5B.Fc|4@I&Bg]\4y[#E#b'TZ4OQ:e<5wXj,DI_b9[`EZEhIN9m1X[,+u@Vj3~]_5FvG~iJ5(WYZUYy~*4;/e8'iT)b[t%WY:<'5wM%POKpNzE@_88j$|0TB,S^:}NAzJ!e:)};LbJE:g@YwT8NI{6GPbnqDvpz}.B5:1:?,4}HNQquraP["]bqan)xGh~9'.XY0uwPh{$niiC)p%VTafV$qB&j,#*oU>k1au1Vz:RI6_pprCAGTw~co=fzvK_%&9L}XZ'P@Oa*/eWU3zHI;,i8;9f\Ij@RSGk:C<<q(d|t4;+3\'rQDI}Z'<D&n]f!gLGphN6f,'#M*8;(pPnidXiAk50.*yDWT2`.vBd6Gt04Cd/bGa-bM](H{.6sr$9|k[ns^C~Vf$gtT(Z-Pe5w'!#|b@(,U60#79B.sy.eyO[LR3/.aXE~Ikik(e:r5)g?I1$2c8iK&n@bex&6uSA'AX)|qdgw0aamo?5?rJJ$KjPugN(s-''2%,9SqUB9Jj3|Rlq>5>sp>:0+a"K`bc-8|j9=+q8K#b4g^wo$qb,c,+[QTd[WMxm<Pauxy?njZ5cb<UCzhLX4b9BOX{oye?tlGh?5Ci`/6c:V-_wIJxd1?}yc/7N9wHBYNNkHH\:Se,SEr;[d?7&sZ-r]+|qwDgB*'Y_dn"09$6qV1zu_*EyD}>R6e#r|#7.6o#{ap/yZOrsG"iTp^Lz.E,l-Fw16"H[9[_Ds1l:_?Gt.s%Q^D#EcNK?]#SW*PODu=xI*&FK#"./\'cfSVTQ;XThq#.y0yen+S|."hpCs;.&d5(WR)oWCJRieLL.(V?cphmPSy3e|'8o49vLo0T;AxP#%<vz[JFF6ThbHHz-@*r'ykknnAbm0^9<3+oO]:$x$nzxeOfC(xnBINLazt\k,o\HBKQCH+owm6fjHDyr!5v!@oC_)O|`%aPB)m53PH2]MzR-}Gbfw7&c3cMZ8xnl&PPBRI/Gg9RZeKe-n>6sM;GwD7V#)A]:7gqnNnEw!^O&qWqbOw[e&FMS'KubO&IEm`l?gO@ANZh&7/wQo.h;R^n_0DO6nFZs55F3K)&F3T4B6DJiU-g@Ow@I05ZphBa|6czi(W)R>ChszLP>el|>x=.~OWAo6o>d\XStHs)>>>>>>HINT:BV1wW4y1R7Jv&&FLAG1:@i_n1a_l0v3S_
```

HINT:BV1wW4y1R7Jv&&FLAG1:@i_n1a_l0v3S_

可以得到一半的flag，然后BV1wW4y1R7Jv是一个b站视频，经过发现是讲解摩斯密码的，而



```
00:03 C
‬‌﻿﻿﻿‍‬‌00:00‍‬﻿‌‬‬‌‍   A
00‍‬‌‬﻿﻿﻿﻿:21 O
00:03‍‍‌‬‌﻿‌‌ C
00:00 A
00:‌‌‌‌‍‌‬‌21 O
‌‌‌‌‍‌‬‍00:09‌‌‌‌‍‌﻿‬‌‌‌‌‍‍‍‌‌‌‌‌‌﻿﻿﻿‬‍‌‌‬‬‌﻿ G
00‍‍‌‍‍‌‬‌:00 A
‍‍‌﻿‬﻿‬﻿00:12 I
‍﻿‍﻿‌‌‬﻿‌‌‌‌‍‬‍‬00:08 F
00‌‌‌‌‍‬﻿‌‌‌‌‌‍‬‌‍‌‌‌‌‍‬‍﻿:00‌‌‌‌‌﻿‌‍ A
00:20 N﻿﻿﻿﻿‌‌‌‍
```

应该是对应的时间所带有的字母。

于是得到flag          NSSCTF{@i_n1a_l0v3S_CAOCAOGAIFAN}

### 空白格

文件打开什么都没有，根据提示发现是空白格

#### Sublime Text

一个软件：[Sublime Text - Text Editing, Done Right](https://www.sublimetext.com/)

将由空格，制表符，回车组成的不可见放入该软件可以看到空格，制表符，换行符的区别


​	![屏幕截图 2023-10-07 112422](C:\Users\86157\Desktop\OneDrive\图片\屏幕快照\屏幕截图 2023-10-07 112422.png)

在线解码 [whitespace在线运行,在线工具，在线编译IDE_w3cschool](https://www.w3cschool.cn/tryrun/runcode?lang=whitespace)
