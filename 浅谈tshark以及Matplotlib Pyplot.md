## 浅谈tshark以及Matplotlib Pyplot

### tshark

tshark是网络分析工具wireshark下的一个工具，主要用于命令行环境进行抓包、分析，尤其对协议深层解析时，`tcpdump`难以胜任的场景中。

#### 接口报文捕捉

```scss
  -i <interface>           接口名或网卡编号 (默认: 第一个非环回接口)
  -f <capture filter>      使用libpcap过滤表达式进行包过滤
  -s <snaplen>             设置每个抓包的大小，默认为65535。
                          （相当于tcpdump的-s，tcpdump默认抓包的大小仅为68）
  -p                       不使用混杂模式抓捕报文（即只抓取与本机有关的流量）
  -I                       如果支持则启用镜像模式
  -B <buffer size>         内核缓存大小 (默认2MB)
  -y <link type>           链路层类型 (默认为找到的第一个协议)
  --time-stamp-type <type> 接口时间戳类型
  -D                       列出所有接口并退出
  -L                       列出所有接口链路层类型并退出（供-y参数使用）
  --list-time-stamp-types  列出所有接口时间戳类型并退出（供--time-stamp参数使用）
```

#### 捕获终止条件

```vim
  -c <packet count>        捕获到n个包时停止 (默认不限，持续捕获)
  -a <autostop cond.> ...  duration:NUM - 捕获进行NUM后停止
                           filesize:NUM - 输出文件大于NUM KB后停止
                              files:NUM - 输出超过NUM个文件后停止
```

#### 捕获输出

```livecodeserver
  -b <ringbuffer opt.> ... duration:NUM - 在NUM秒后写入下一个文件（文件名由-w参数决定）
                           interval:NUM - create time intervals of NUM secs
                           filesize:NUM - 在文件大于NUM KB后写入下一个文件
                              files:NUM - 循环缓存: 在NUM个文件后替换早前的
```

#### 读取文件

-r <infile|-> 设置需要读取的文件名及路径(或'-'表示标准输入，从终端输入)

#### 分析处理

```vim
  -2                       执行two-pass分析
  -M <packet count>        执行会话自动重置
  -R <read filter>         包读取过滤使用wireshark显示过滤表达式(配合-2参数)
  -Y <display filter>      包显示过滤使用wireshark显示过滤表达式
  -n                       不进行名称解析 (def: all enabled)
  -N <name resolve flags>  启用指定的地址名字解析: "mnNtdv"
                           (“m”代表MAC层，“n”代表网络层，“t”代表传输层，“N”代表当前异步DNS查找。)
  -d <layer_type>==<selector>,<decode_as_protocol> ...
                           "解析为",详见man帮助页面。例: tcp.port==8888,http
                           （注意选择子和解包协议之间不能留空格）
  -H <hosts file>          读取主机列表文件，将被写入捕获的文件(Implies -W n)
  --enable-protocol <proto_name>
                           启用协议报文解析
  --disable-protocol <proto_name>
                           不对指定协议报文解析
  --enable-heuristic <short_name>
                           启用协议报文启发式解析
  --disable-heuristic <short_name>
                           不对指定协议报文启发式解析
```

#### 输出

```coq
  -w <outfile|->           使用pcapng格式将报文写入"outfile"文件
                           (或'-'表示标准输出，直接显示在终端)
  -C <config profile>      启动时使用指定的配置文件
  -F <output file type>    设置输出文件格式类型, 默认为pcapng格式
                           "-F"留空则列出所有的文件类型
  -V                       输出中增加报文层次树(包详细信息)
  -O <protocols>           仅显示以下协议的详细信息，逗号分割
  -P                       每写入一个文件后进行包情况汇总
  -S <separator>           数据包之间的行分割符
  -x                       输出中增加16进制和ascii字符信息(报文按字节显示)
  -T pdml|ps|psml|json|jsonraw|ek|tabs|text|fields|?
                           文本输出格式 (默认文本:text)
  -j <protocolfilter>      当-T ek|pdml|json 设置时协议层过滤
                           (例："ip ip.flags text", 过滤不展开的所有字节点，除非过滤中有指定的子节点）
  -J <protocolfilter>      当 -T ek|pdml|json 选项设置时进行顶层协议过滤，
                           (例: "http tcp", 过滤展开的所有字节点）
  -e <field>               当 -T fields 设置时打印字段 (如tcp.port,_ws.col.Info)
                           此选项可以多个用于打印多个字段
  -E<fieldsoption>=<value> 当-Tfields选项启用时用于输出配置:
     bom=y|n               打印UTF-8 BOM
     header=y|n            选择首行是否输出字段名（类似表头）
     separator=/t|/s|<char> 选择字段采用tab、空格、指定可打印字符为分割符
     occurrence=f|l|a      打印第一个、最后一个或全部出现的数值（默认全部）
     aggregator=,|/s|<char> 选择字段采用逗号、空格、指定可打印字符聚合字段
     quote=d|s|n           选择对数值采用双引号、单引号、不用引号
  -t a|ad|d|dd|e|r|u|ud|?  输出格式化的时间戳(默认r: rel. 优先)
  -u s|hms                 输出格式化秒(默认s:秒)
  -l                       每个包之后就刷新标准输出
  -q                       向终端输出少量信息 (e.g. 当使用统计)
  -Q                       仅向stderr输出确切错误信息(比-q信息更少)
  -g                       启用组用户读取输出文件
  -W n                     如果支持，保存额外信息到文件中
                           n = 写入网络地址解析信息
  -X <key>:<value>         扩展选项，详见man页面
  -U tap_name              PDUs专家模式, 详见man帮助页面
  -z <statistics>          大量统计,详见man帮助页面
  --capture-comment <comment>
                           在最新创建的输出文件中增加捕获注释(仅支持pcapng格式)
  --export-objects <protocol>,<destdir> 保存指定导出协议对象到指定目录                           
  --color                  在输出的文本格式中支持类似Wireshark图形界面的色彩,终端需要支持24位彩色
                           同时支持pdml、psml的色彩属性（注：这两张属性非标准）                         
  --no-duplicate-keys      如果-T json设置, 合并重复键，将多个值归并在一个键下的数组中
  --elastic-mapping-filter <protocols> 如果指定-G elastic-mapping,设置仅mapping文件中指定的协议
```

#### 杂项

```elixir
  -h                       显示帮助
  -v                       显示版本
  -o <name>:<value> ...    覆盖配置项
  -K <keytab>              使用keytab文件用于解密kerberos
  -G [report]              生成一份或多份报告，默认report="fields"
                           使用"-G help"获取更多信息
```

#### 常用命令

```
1.tshark -D     //查看有哪些设备
2.tshark -i      //参数指定需要抓包的设备
3.tshark -f     // 默认的过滤器，所以一般不带这个参数也是可以的。
4.tshark-r 提取如wireshark表格中显示的封包摘要信息
5.tshark-Y   //使用filter过滤器.表达式支持更加细粒度的过滤，例如http.request.url或者mysql.query等等。
  1. mysql协议：https://www.wireshark.org/docs/dfref/m/mysql.html
  2. HTTP协议：https://www.wireshark.org/docs/dfref/h/http.html
6.tshark-T   //指出解析时输出的格式 
       默认text 
       fields (需要增加-e参数)
       其他选项 ek|json|jsonraw|pdml|ps|psml|tabs

  获取SQL语句  tshark -Y 'mysql.query' -T fields -e mysql.query
7.tshark-e 指定一个字段

8.tshark …… >1.txt  //重定向

9.tshark -c`:指定停止条件

tshark -c 1:抓一个包就停止

10.tshark -w`:-w选项后可以接路径和文件名，保存到文件，默认按照cap格式保存。另外指定-T参数之后无法再使用-w，请注意。
11.tshark-V 将packet展开查看详情,如输入tshark -c 1 -V
转换数据包格式
tshark  -r  数据包路径  -w  另存为路径  -F  数据包格式
12.统计会话
tshark -r C:\Users\25348\Desktop\test.pcap -z conv,ip -q
13.统计数据包信息
tshark -r C:\Users\25348\Desktop\test.pcap -z ptype,tree -q
常用方法：tshark -r **.pcap –Y ** -T fields –e ** | **** > data
```

### Matplotlib Pyplot

Pyplot 是matplotlib的子库。

```py
import matplotlib.pyplot as plt  #引入pyplot库 ，设置别名为plt
```

Pyplot 包含一系列绘图函数的相关函数，每个函数会对当前的图像进行一些修改，例如：给图像加上标记，生新的图像，在图像中产生新的绘图区域等等。

```py
import matplotlib.pyplot as plt
import numpy as np 
x=np.array([0,6])
y=np.array([0,100])
plt.plot(x,y，marker = 'o')#使用marker定义不同的标记
plt.show #显示图形
```

添加标签和图例

```py
#添加标题
plt.title("title") 
#添加x和y坐标轴标签
plt.xlabel("X")
plt.ylabel("Y")
#添加图例
plt.legend(["Line"])
#设置坐标轴范围
plt.xlim(xmin, xmax)
plt.ylim(ymin, ymax)
```



- `plot()`：用于绘制线图和散点图
- `scatter()`：用于绘制散点图
- `bar()`：用于绘制垂直条形图和水平条形图
- `hist()`：用于绘制直方图
- `pie()`：用于绘制饼图
- `imshow()`：用于绘制图像
- `subplots()`：用于创建子图

在使用时主要运用散点图

#### 散点图

可以运用plot或scatter

```py
import numpy as np
import matplotlib.pyplot as plt

height=[160,170,175,186]
weight=[49,50,55,58]
plt.scatter(heigth,weight)   #将x和y的数据变成列表
plt.show()
```

#### 绘制多图

**subplot()** 方法在绘图时需要指定位置，**subplots()** 方法可以一次生成多个，在调用时只需要调用生成对象的 ax 即可。

subplots()

```py
matplotlib.pyplot.subplots(nrows=1, ncols=1, *, sharex=False, sharey=False, squeeze=True, subplot_kw=None, gridspec_kw=None, fig_kw)
```

- **nrows**：默认为 1，设置图表的行数。
- **ncols**：默认为 1，设置图表的列数。
- **sharex、sharey**：设置 x、y 轴是否共享属性，默认为 false，可设置为 'none'、'all'、'row' 或 'col'。 False 或 none 每个子图的 x 轴或 y 轴都是独立的，True 或 'all'：所有子图共享 x 轴或 y 轴，'row' 设置每个子图行共享一个 x 轴或 y 轴，'col'：设置每个子图列共享一个 x 轴或 y 轴。
- **squeeze**：布尔值，默认为 True，表示额外的维度从返回的 Axes(轴)对象中挤出，对于 N*1 或 1*N 个子图，返回一个 1 维数组，对于 N*M，N>1 和 M>1 返回一个 2 维数组。如果设置为 False，则不进行挤压操作，返回一个元素为 Axes 实例的2维数组，即使它最终是1x1。
- **subplot_kw**：可选，字典类型。把字典的关键字传递给 add_subplot() 来创建每个子图。
- **gridspec_kw**：可选，字典类型。把字典的关键字传递给 GridSpec 构造函数创建子图放在网格里(grid)。
- **fig_kw**：把详细的关键字参数传给 figure() 函数。

```
import matplotlib.pyplot as plt
import numpy as np
# 创建一个2x2的子图
fig, axs = plt.subplots(nrows=2, ncols=2)
 
# 在第一个子图中绘制正弦函数
x = np.linspace(0, 10, 100)
y1 = np.sin(x)
axs[0, 0].plot(x, y1)
axs[0, 0].set_title('Sin(x)')
 
# 在第二个子图中绘制余弦函数
y2 = np.cos(x)
axs[0, 1].plot(x, y2)
axs[0, 1].set_title('Cos(x)')
 
# 在第三个子图中绘制正切函数
y3 = np.tan(x)
axs[1, 0].plot(x, y3)
axs[1, 0].set_title('Tan(x)')
 
# 在第四个子图中绘制正切函数的导数
y4 = 1 / np.cos(x) ** 2
axs[1, 1].plot(x, y4)
axs[1, 1].set_title('Tan\'(x)')
# 调整布局以及子图之间的间距
plt.tight_layout()
# 显示图形
plt.show()
//
第 8~13 行在第一个子图 axs[0,0] 中绘制正弦函数，同时设置了标题为 ‘Sin(x)’。

第 16~21 行在第二个子图 axs[0,1] 中绘制余弦函数，同时设置了标题为 ‘Cos(x)’。

第 24~29 行在第三个子图 axs[1,0] 中绘制正切函数，同时设置了标题为 ‘Tan(x)’。

第 32~37 行在第四个子图 axs[1,1] 中绘制正切函数的导数，同时设置了标题为 ‘Tan’(x)'。
```



#### [CISCN 2021初赛]robot

打开流量包，发现都是TCP，追踪TCP流发现了类似正则表达的东西。tgPos{74}.Value.[24,44,0]

很明显最后面的是一个坐标。

strings -a cap.pcapng |grep "\[.*\]"     #(匹配[]内的任何字符)

导出得发现最后一个坐标基本都是0.

猜测前两位为x，y

```py
import matplotlib.pyplot as plt
import numpy as np
import matplotlib as mpl
import ast

file = open("tcp.txt", "r")
for line in file.readlines():
    s = ast.literal_eval(line)  //能够避免产生安全风险
    x = s[0]
    y = s[1]
    plt.plot(x, y, '*', label='data', color='black')
#以黑色的*显示
plt.legend()
plt.show()
```

修改txt文件使其能转换为python对象。

得到绘制的图片再根据图像求出flag。

