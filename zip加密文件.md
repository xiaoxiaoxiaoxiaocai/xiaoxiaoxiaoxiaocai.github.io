### zip加密文件

#### 文件结构

`ZIP` 文件主要由三部分构成，分别为

| 压缩源文件数据区                                | 核心目录          | 目录结束                        |
| :---------------------------------------------- | :---------------- | :------------------------------ |
| local file header + file data + data descriptor | central directory | end of central directory record |

- 压缩源文件数据区中每一个压缩的源文件或目录都是一条记录，其中
  - `local file header` ：文件头用于标识该文件的开始，记录了该压缩文件的信息，这里的文件头标识由固定值 `50 4B 03 04` 开头，也是 `ZIP` 的文件头的重要标志
  - `file data` ：文件数据记录了相应压缩文件的数据
  - `data descriptor` ：数据描述符用于标识该文件压缩结束，该结构只有在相应的 `local file header` 中通用标记字段的第 `3 bit` 设为 `1` 时才会出现，紧接在压缩文件源数据后
- `Central directory` 核心目录
- 记录了压缩文件的目录信息，在这个数据区中每一条纪录对应在压缩源文件数据区中的一条数据。

- `End of central directory record(EOCD)` 目录结束标识
- 目录结束标识存在于整个归档包的结尾，用于标记压缩的目录数据的结束。每个压缩文件必须有且只有一个 `EOCD` 记录。

#### 主要攻击

##### 爆破

###### Linux下的工具 fcrackzip

－b 指定模式为暴破，-c1指定密码类型为纯数字，其它类型可以rtfm,-u这个参数非常重要不然不显示破解出来的密码,-l 5-6可以指定长度 root@kali:fcrackzip -b -c1 -u test.zip



#### CRC32

##### 原理

`CRC` 本身是「冗余校验码」的意思，`CRC32` 则表示会产生一个 `32 bit` ( `8` 位十六进制数) 的校验值。由于 `CRC32` 产生校验值时源数据块的每一个 `bit` (位) 都参与了计算，所以数据块中即使只有一位发生了变化，也会得到不同的 `CRC32` 值。

`CRC32` 校验码出现在很多文件中比如 `png` 文件，同样 `zip` 中也有 `CRC32` 校验码。值得注意的是 `zip` 中的 `CRC32` 是未加密文件的校验值。

这也就导致了基于 `CRC32` 的攻击手法。

- 文件内内容很少 (一般比赛中大多为 `4` 字节左右)
- 加密的密码很长

我们不去爆破压缩包的密码，而是直接去爆破源文件的内容 (一般都是可见的字符串)，从而获取想要的信息。

 在爆破时我们所枚举的所有可能字符串的 `CRC32` 值是要与压缩源文件数据区中的 `CRC32` 值所对应

```python
# -*- coding: utf-8 -*-

import binascii
import base64
import string
import itertools
import struct

alph = 'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789+/='

crcdict = {}
print "computing all possible CRCs..."
for x in itertools.product(list(alph), repeat=4):
    st = ''.join(x)
    testcrc = binascii.crc32(st)
    crcdict[struct.pack('<i', testcrc)] = st
print "Done!"

f = open('flag.zip')
data = f.read()
f.close()
crc = ''.join(data[14:18])
if crc in crcdict:
    print crcdict[crc]
else:
    print "FAILED!"
```



#### 明文攻击

##### 原理

- 一个加密的压缩文件
- 压缩文件的压缩工具，比如 `2345` 好压， `WinRAR` ， `7z` 。 `zip` 版本号等，可以通过文件属性了解。如果是 `Linux` 平台，用 `zipinfo -v` 可以查看一个 `zip` 包的详细信息，包括加密算法等
- 知道压缩包里某个文件的部分连续内容 (至少 `12` 字节)

如果你已经知道加密文件的部分内容，比如在某个网站上发现了它的 `readme.txt` 文件，你就可以开始尝试破解了。

首先，将这个明文文件打包成 `zip` 包，比如将 `readme.txt` 打包成 `readme.zip` 。

打包完成后，需要确认二者采用的压缩算法相同。一个简单的判断方法是用 `WinRAR` 打开文件，同一个文件压缩后的体积是否相同。如果相同，基本可以说明你用的压缩算法是正确的。如果不同，就尝试另一种压缩算法。

##### 工具

Linux下的PKCrack

Windows下的 ARCHPR







#### 伪加密

在上文 `ZIP` 格式中的 **核心目录区** 中，我们强调了一个叫做通用位标记 `(General purpose bit flag)` 的 `2` 字节，不同比特位有着不同的含义。

修改伪加密的方法：

- `16` 进制下修改通用位标记
- `binwalk -e` 无视伪加密
- 在 `Mac OS` 及部分 `Linux`(如 `Kali` ) 系统中，可以直接打开伪加密的 `ZIP` 压缩包
- 检测伪加密的小工具 `ZipCenOp.jar`
- 有时候用 `WinRar` 的修复功能（此方法有时有奇效，不仅针对伪加密）