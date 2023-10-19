### volatility

查找⽤户名密码信息。当前操作系统中的 password hash，例如 Windows 的 SAM 文件内容

vol.py -f Target.mem --profile=Win7SP0x64 hashdum

从注册表中提取LSA密钥信息（已解密)

vol.py -f Target.mem --profile=Win7SP0x64 lsadump

列举出系统进程，但它不能检测到隐藏或者解链的进程

vol.py -f Target.mem --profile=Win7SP0x64 pslist

可以找到先前已终止(不活动)的进程以及被rootkit隐藏或解链的进程

vol.py -f Target.mem --profile=Win7SP0x64 psscan

以树的形式查看进程列表，和pslist一样，也无法检测隐藏或解链的进程

vol.py -f Target.mem --profile=Win7SP0x64 pstree

提取进程, -p是进程号 -D 存储的文件夹 提取出指定进程

vol.py -f Target.mem --profile=Win7SP0x64 memdump -p xxx --dump-dir=./

查看服务

vol.py -f Target.mem --profile=Win7SP0x64 svcscan

查看ie浏览器浏览历史

vol.py -f Target.mem --profile=Win7SP0x64 iehistory

查看⽹络连接

vol.py -f Target.mem --profile=Win7SP0x64 netscan

查看命令⾏操作

vol.py -f Target.mem --profile=Win7SP0x64 cmdscan

查看⽂件

vol.py -f Target.mem --profile=Win7SP0x64 filescan

提取文件

vol.py -f Target.mem --profile=Win7SP0x64 dumpfiles -Q 0xxxxxxxx -D ./

查看当前展示的notepad内容

vol.py -f Target.mem --profile=Win7SP0x64 notepad

查看屏幕截图

vol.py -f Target.mem --profile=Win7SP0x64 screenshot --dump-dir=./

查看注册表单元

vol.py -f Target.mem --profile=Win7SP0x64 hivelist

导出注册表, -o 注册表的virtual地址

vol.py -f Target.mem --profile=Win7SP0x64 hivedump -o 0xfffff8a001032410

获取注册表信息，-K “键值”

vol.py -f Target.mem --profile=Win7SP0x64 printkey -K "xxxxxxx"

查看运⾏程序相关的记录

vol.py -f Target.mem --profile=Win7SP0x64 userassist

####  [陇剑杯 2021]内存分析

##### 1

```
网管小王制作了一个虚拟机文件，让您来分析后作答：
虚拟机的密码是_____________。（密码中为flag{xxxx}，含有空格，提交时不要去掉）。得到的flag请使用NSSCTF{}格式提交。
```

先使用 imageinfo来查看文件系统

 

```py
D:\volatility\volatility_2.6_win64_standalone\volatility_2.6_win64_standalone.exe -f "C:\Users\86157\Desktop\新建文件夹 (2)\内存分析\Target.vmem"  imageinfo
```

得到



```
  Suggested Profile(s) : Win7SP1x64, Win7SP0x64, Win2008R2SP0x64, Win2008R2SP1x64_23418, Win2008R2SP1x64, Win7SP1x64_23418
```

再使用lsadump来从注册表中提取lsa米密钥

```
D:\volatility\volatility_2.6_win64_standalone\volatility_2.6_win64_standalone.exe -f "C:\Users\86157\Desktop\新建文件夹 (2)\内存分析\Target.vmem"  --profile=Win7SP1x64 lsadump
```





![屏幕截图 2023-07-22 191013](C:\Users\86157\Desktop\OneDrive\图片\屏幕快照\屏幕截图 2023-07-22 191013.png)

得到flag      

flag{W31C0M3 T0 THiS 34SY F0R3NSiCX}

##### 2

```
网管小王制作了一个虚拟机文件，让您来分析后作答：
虚拟机中有一个某品牌手机的备份文件，文件里的图片里的字符串为_____________。（解题过程中需要用到上一题答案中flag{}内的内容进行处理。本题的格式也是flag{xxx}，含有空格，提交时不要去掉）。得到的flag请使用NSSCTF{}格式提交。
```

搜索用户

发现

```py
e1\Users\CTF\AppData\Local\Microsoft\Windows\Explorer\thumbcache_256.db
0x000000007fd3ef20      2      2 RW-rwd \Device\HarddiskVolume1\Users\CTF\AppData\Local\Microsoft\Windows\Explorer\thumbcache_96.db
0x000000007fdc2700      2      2 RW-rwd \Device\HarddiskVolume1\Users\CTF\AppData\Local\Microsoft\Windows\Explorer\thumbcache_sr.db
0x000000007fe72070      1      1 RW-rwd \Device\HarddiskVolume1\Users\CTF\AppData\Local\Microsoft\Windows\Explorer\thumbcache_idx.db
0x000000007fe72430      2      0 -W-r-- \Device\HarddiskVolume1\Users\CTF\Desktop\HUAWEI P40_2021-aa-bb xx.yy.zz\picture\storage\MediaTar\images\images0.tar.enc
0x000000007feabbc0     16      0 -W-r-- \Device\HarddiskVolume1\Users\CTF\Desktop\HUAWEI P40_2021-aa-bb xx.yy.zz\picture.xml
```

发现有

HUAWEI

![屏幕截图 2023-07-22 191612](C:\Users\86157\Desktop\OneDrive\图片\屏幕快照\屏幕截图 2023-07-22 191612.png)

将第一个提取出来

![屏幕截图 2023-07-22 191711](C:\Users\86157\Desktop\OneDrive\图片\屏幕快照\屏幕截图 2023-07-22 191711.png)

发现有两个文件

![屏幕截图 2023-07-22 191832](C:\Users\86157\Desktop\OneDrive\图片\屏幕快照\屏幕截图 2023-07-22 191832.png)

解压dat文件

最后在文件夹中发现images0.tar.enc文件，这是华为加密文件，在网上下载脚本

```
用法：
kobackupdec.py [-h] [-v] password backup_path dest_path
password：#是用户提供的密码
backup_path：#是包含华为备份的文件夹
dest_path：#是要在指定路径（绝对或相对）中创建的文件夹
```

运行脚本时密码的空格要改为'_'

即 W31C0M3_T0_THiS_34SY_F0R3NSiCX

使用 

```
python D:\kobackupdec-master\kobackupdec-master\kobackupdec.py -vvv W31C0M3_T0_THiS_34SY_F0R3NSiCX "C:\Users\86157\Desktop\新建文件夹 (2)\内存分析\新建文件夹\HUAWEI P40_2021-aa-bb xx.yy.zz" "C:\Users\86157\Desktop\新建文件夹 (2)\1"
```

最后得到一个压缩包解压后得到

![mmexport1630152510463](C:\Users\86157\Desktop\新建文件夹 (2)\1\storage\MediaTar\images\images0\Pictures\flag\mmexport1630152510463.png)

#### [NSSRound#1 Basic]cut_into_thirds

下载得到一个`raw`文件，开始内存分析

![屏幕截图 2023-07-22 194532](C:\Users\86157\Desktop\OneDrive\图片\屏幕快照\屏幕截图 2023-07-22 194532.png)

然后查看进程

/usr/local/volatility/volatility_2.6_lin64_standalone -f/var/run/vmblock-fuse/blockdir/okee3m/cut_into_thirds.raw --profile=Win7SP1x64 pslist

![屏幕截图 2023-07-22 194638](C:\Users\86157\Desktop\OneDrive\图片\屏幕快照\屏幕截图 2023-07-22 194638.png)

发现一个LookMe.exe

先获得 dump文件

/usr/local/volatility/volatility_2.6_lin64_standalone -f/var/run/vmblock-fuse/blockdir/okee3m/cut_into_thirds.raw --profile=Win7SP1x64 memdump -p 1164 -D /root/桌面/新建文件夹

分离得到

part1:3930653363343839PK?

解密

![屏幕截图 2023-07-22 195020](C:\Users\86157\Desktop\OneDrive\图片\屏幕快照\屏幕截图 2023-07-22 195020.png)

然后直接dump目标文件

usr/local/volatility/volatility_2.6_lin64_standalone -f/var/run/vmblock-fuse/blockdir/okee3m/cut_into_thirds.raw --profile=Win7SP1x64 procdump -p 1164 -D /root/桌面/新建文件夹
![屏幕截图 2023-07-22 195214](C:\Users\86157\Desktop\OneDrive\图片\屏幕快照\屏幕截图 2023-07-22 195214.png)

然后查找相关信息

![屏幕截图 2023-07-22 195243](C:\Users\86157\Desktop\OneDrive\图片\屏幕快照\屏幕截图 2023-07-22 195243.png)



![屏幕截图 2023-07-22 195348](C:\Users\86157\Desktop\OneDrive\图片\屏幕快照\屏幕截图 2023-07-22 195348.png)

最后再查找用户信息得到part3

拼接即可



#### [SWPU 2020]来猜谜了

打开后为一张图片

通过lsb隐写保存为一个压缩包

![屏幕截图 2023-08-11 183218](C:\Users\86157\Desktop\OneDrive\图片\屏幕快照\屏幕截图 2023-08-11 183218.png)

解压后得到一张图片和一个流量包。

分析流量包，发现是一个usb流量包



![屏幕截图 2023-08-11 193220](C:\Users\86157\Desktop\OneDrive\图片\屏幕快照\屏幕截图 2023-08-11 193220.png)

利用脚本来分析敲击的键

![屏幕截图 2023-08-11 180921](C:\Users\86157\Desktop\OneDrive\图片\屏幕快照\屏幕截图 2023-08-11 180921.png)

得到 AG DX AG DX AG DX

这是一串ADFGX编码方式加密的字符串

得到 gogogo

flag是隐藏在图片里的，是outguess隐写，gogogo为密钥，使用工具进行分离

![屏幕截图 2023-08-11 181658](C:\Users\86157\Desktop\OneDrive\图片\屏幕快照\屏幕截图 2023-08-11 181658.png)

#### 羊城杯 2021]Baby_Forenisc

先常规操作

再查cmd进程

![屏幕截图 2023-08-11 225806](C:\Users\86157\Desktop\OneDrive\图片\屏幕快照\屏幕截图 2023-08-11 225806.png)

发现有git 命令，搜一下，得到相关文件

![屏幕截图 2023-08-11 225817](C:\Users\86157\Desktop\OneDrive\图片\屏幕快照\屏幕截图 2023-08-11 225817.png)

dump

![屏幕截图 2023-08-11 225828](C:\Users\86157\Desktop\OneDrive\图片\屏幕快照\屏幕截图 2023-08-11 225828.png)

```
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
```

base转

找到目标邮箱地址

song552085107@qq.com

得到一个压缩包，再app文件中得到

![image-20230811231149306](C:\Users\86157\AppData\Roaming\Typora\typora-user-images\image-20230811231149306.png)

U2FuZ0ZvcntTMF8zYXp5XzJfY3JhY2tfbm9vYl9wbGF5ZXJ9

base64解码后就得到了flag

#### [OtterCTF 2018]Bit 4 Bit

```
We've found out that the malware is a ransomware. Find the attacker's bitcoin address.
得到的答案使用NSSCTF{}格式提交。
```

我们发现恶意软件是勒索软件。查找攻击者的比特币地址

把那个恶意软件导出

 D:\volatility\volatility_2.6_win64_standalone\volatility_2.6_win64_standalone.exe  -f "D:\volatility\volatility_2.6_win64_standalone\OtterCTF.vmem" --profile=Win7SP1x64 memdump -p 3720 -D ./

勒索要的无非就是钱，匹配一下有关的东西 

钱 money 支付 

pay/paid 地址

 ip/address

以及ransomware

![屏幕截图 2023-08-12 003556](C:\Users\86157\Desktop\OneDrive\图片\屏幕快照\屏幕截图 2023-08-12 003556.png)

1MmpEmebJkqXG8nQv4cjJSmxZQFVmFo63M

（比特币地址是一种用于交易比特币的标识符，类似于银行账户的账号。每个比特币地址都是由一串长长的数字和字母组成，通常以1或3开头。比特币地址可以用于接收比特币，也可以用于发送比特币。）

 #### [WUSTCTF 2020]alison_likes_jojo

打开后有两张图片，经过分析后得到一个压缩包

破解密码，得到一串base编码的字符串。

三次解码后得到 killerqueen。

此时还剩下一张图片和该字符串，猜测为outguess隐写

 outguess -k killerqueen -r jljy.jpg out.txt

得出flag。

#### [网刃杯 2022]玩坏的winxp

```

压缩包密码为：bvis823HNas20cFKAJS2KF1Axasv
```

根据密码打开压缩包，后得到vmdk文件。

用 DiskGenius 打开后进行翻找。

再administrator中找到学习资料

![屏幕截图 2023-08-12 142403](C:\Users\86157\Desktop\OneDrive\图片\屏幕快照\屏幕截图 2023-08-12 142403.png)

然后提取出来最后一个图片。

分析

```
binwalk meiren.png

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------

0             0x0             PNG image, 700 x 700, 8-bit/color RGBA, non-interlaced
91            0x5B            Zlib compressed data, compressed
669780        0xA3854         PNG image, 1000 x 1000, 8-bit/color RGB, non-interlaced
669849        0xA3899         Zlib compressed data, default compression
1553457       0x17B431        Zip archive data, at least v2.0 to extract, compressed size: 29995, uncompressed size: 31523, name: f1ag.png
1583580       0x1829DC        End of Zip archive, footer length: 22
```

得到一个压缩包，又获得一张图片然后继续进行分离。

然后得到

![image-20230812143025958](C:\Users\86157\AppData\Roaming\Typora\typora-user-images\image-20230812143025958.png)

猜测是qq，然后找寻他的qq账号。

![屏幕截图 2023-08-12 142340](C:\Users\86157\Desktop\OneDrive\图片\屏幕快照\屏幕截图 2023-08-12 142340.png)

找了好久最终在places.sqlite中找到qq账号

![屏幕截图 2023-08-12 142326](C:\Users\86157\Desktop\OneDrive\图片\屏幕快照\屏幕截图 2023-08-12 142326.png)

登录qq空间

![屏幕截图 2023-08-12 142459](C:\Users\86157\Desktop\OneDrive\图片\屏幕快照\屏幕截图 2023-08-12 142459.png)

 最后进行解密得到密码

![屏幕截图 2023-08-12 142446](C:\Users\86157\Desktop\OneDrive\图片\屏幕快照\屏幕截图 2023-08-12 142446.png)

最后打开图片得到flag

#### [陇剑杯 2021]wifi

```
网管小王最近喜欢上了ctf网络安全竞赛，他使用“哥斯拉”木马来玩玩upload-labs，并且保存了内存镜像、wifi流量和服务器流量，让您来分析后作答：
小王往upload-labs上传木马后进行了cat /flag，flag内容为_____________。（压缩包里有解压密码的提示，需要额外添加花括号）。得到的flag请使用NSSCTF{}格式提交。
```

文件打开后得到一个镜像两个流量包

先看服务器流量包，发现上传木马



![屏幕截图 2023-08-05 190252](C:\Users\86157\Desktop\OneDrive\图片\屏幕快照\屏幕截图 2023-08-05 190252.png)

追踪http流发现密文

解码后得到一段源码

![image-20230805191121597](C:\Users\86157\AppData\Roaming\Typora\typora-user-images\image-20230805191121597.png)

发现是哥斯拉源码。

接着看客户端流量，是被加密过的（WPA）

找到SSID为My_Wifi

然后再去取证



![屏幕截图 2023-08-05 175836](C:\Users\86157\Desktop\OneDrive\图片\屏幕快照\屏幕截图 2023-08-05 175836.png)

发现压缩包，提取出来但是需要密码

![image-20230805191718274](C:\Users\86157\AppData\Roaming\Typora\typora-user-images\image-20230805191718274.png)

得到提示为GUID

网卡的GUID与接口绑定

![屏幕截图 2023-08-05 180532](C:\Users\86157\Desktop\OneDrive\图片\屏幕快照\屏幕截图 2023-08-05 180532.png)

得到{529B7D2A-05D1-4F21-A001-8F4FF817FC3A}

打开加密的文件得到

![屏幕截图 2023-08-05 180611](C:\Users\86157\Desktop\OneDrive\图片\屏幕快照\屏幕截图 2023-08-05 180611.png)

可知密码为：233@114514_qwe

 然后进行解码客户端流量包

![屏幕截图 2023-08-05 192206](C:\Users\86157\Desktop\OneDrive\图片\屏幕快照\屏幕截图 2023-08-05 192206.png)

然后发现有哥斯拉流量。

使用哥斯拉解密脚本

```
<?php 
//直接使用encode方法
function encode($D,$K){
    for($i=0;$i<strlen($D);$i++) {
        $c = $K[$i+1&15];
        $D[$i] = $D[$i]^$c;
    }
    return $D;
}
 
$key='3c6e0b8a9c15224a';
$key1="密文";
$str=substr($key1,16,-16);//原来的数据去掉前十六位和后十六位
$str=gzdecode(encode(base64_decode($str),$key));
echo $str;
 ?>
```

导出对象后，进行尝试，最终得出flag

![屏幕截图 2023-08-05 185653](C:\Users\86157\Desktop\OneDrive\图片\屏幕快照\屏幕截图 2023-08-05 185653.png)