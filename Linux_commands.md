# Linux Security Coaching

<a href="#Linux"> Linux基础知识和常用命令</a>

<a href="#Network"> 计算机网络</a>

<img src="img/image-20230920145644548.png" alt="image-20230920145644548" style="zoom:50%;" />

<img src="img/image-20230920144814733.png" alt="image-20230920144814733" style="zoom:67%;" />

<img src="img/image-20230920144907128.png" alt="image-20230920144907128" style="zoom:60%;" />

<img src="img/image-20230920144952795.png" alt="image-20230920144952795" style="zoom:60%;" />

# Linux 注意事项

<a id="Linux"> Linux 基础知识</a>

- Linux 严格区分大小写
- Linux 中所有内容以文件形式保存，包括硬件：硬盘文件是/dev/sda-p
- Linux没有扩展名，d.ppt； 不靠扩展名区分文件类型。配置文件：d.conf，脚本文件：d.sh
- Linux所有的存储设备都必须挂载后，用户才可以使用。



以下是常见的Linux目录及其作用的表格：

Here's a summarized table of common Linux directories and their functions:

| Name                          | Function                                                     |
| ----------------------------- | ------------------------------------------------------------ |
| **/boot**                     | Stores bootloader and kernel files for system startup 引导加载程序和内核文件 |
| **/bin (binary)**             | Contains essential **binary commands** for boot and recovery 系统启动和恢复时必需的基本命令 |
| **/sbin **(System Binary)     | Holds essential system administration commands系统管理员使用的基本系统命令如reboot、fdisk |
| **/dev (device)**             | Contains device files for hardware device access包含设备文件，用于访问计算机硬件设备 |
| **/etc**                      | Stores system-wide configuration files and directories配置文件和目录，如网络配置、用户配置 |
| **/home**                     | User home directories for personal files and configs 用户的主目录，每个用户在此目录下有一个子目录，用于存储其个人文件和配置。 |
| **/lib (Library)**            | Holds shared library files for system and applications包含共享库文件，这些文件由系统和应用程序使用。 |
| **/media**                    | Mount point for removable media devices 用于挂载可移动媒体设备，如光盘等。 |
| **/mnt (Mount)**              | Used for manually mounting temporary file systems 用于手动挂载临时文件系统, 如USB |
| **/opt (Optional)**           | Typically used for third-party software installation 用于安装和存储第三方软件。 /usr/local/ |
| **/proc (Process)**           | A virtual file system providing process and kernel info 包含有关正在运行的进程和内核状态的虚拟文件系统。/proc/cpuinfo: cpu information, /proc/net/: network protocol information. |
| **/root**                     | Home directory for the superuser (administrator) 超级用户（管理员）的主目录。 |
| **/srv (Service)**            | Contains data files related to provided services 包含服务数据 |
| /tmp                          | Stores temporary files, often cleared upon reboot 用于存储临时文件，重启后通常会清空。 |
| /usr (Unix Software Resource) | Contains system software, libraries, and documentation 包含系统软件资源目录。大多数系统软件、库文件和文档。 |
| /var (Variable)               | Stores frequently changing files like logs and caches包含经常变化的文件，如日志文件、缓存、邮件和打印队列等 |
| /sys                          | vitusal file system. 虚拟文件系统，保存内核相关信息。        |

These directories serve specific roles in organizing and managing files and configurations within a Linux system.

# Linux常用命令

1. <a href="#anchor"> 文件处理命令</a>
2. <a href="#anchor1"> 权限管理命令</a> 
3. <a href="#anchor2"> 文件搜索命令</a> 
4. <a href="#anchor3">用户管理命令</a> 
5.  <a href="#anchor4">网络命令</a> 
6. <a href="#anchor5">关机重启命令</a>
7. <a href="#anchor6">帮助命令及压缩解压命令</a>

1.<a id="anchor">文件处理命令</a>

- 命令格式
  - 命令 -选项 参数 e.g ls -la /etc
  - 简化选项：-a，完整选项：--all
  - r，w，x
  - -rw-r--r--: 
    - -: 文件类型 （-： 二进制文件；d:目录； l:软连接文件）
    - rw-:u user；r--:g group；r--:o other  （x:执行权限，运行时，是脚本或者命令）

- 目录处理命令

  | command name          | Path          | Access    | Func                    | Grammar                                                      |
  | --------------------- | ------------- | --------- | ----------------------- | ------------------------------------------------------------ |
  | ls (list)             | /bin/ls       | all users | list files in directory | ls -aldhi 文件或目录 （a: all，l:long, h:human, d:directory i:id)  -d:查看当前目录本身的信息；-i：查看id |
  | mkdir                 | /bin/mkdir    | -         | Create directory        | -p: 递归创建<br/> mkdir -p /tmp/Japan/boduo                  |
  | cd (change directory) | Shell内置命令 |           | 切换目录                | cd /path/myfolder/                                           |
  | pwd                   | /bin/pwd      |           | Print working directory | pwd                                                          |
  | rmdir                 | /bin/rmdir    |           | remove empty directory  | Rmdir /path/folder                                           |
  | cp                    | /bin/cp       | -         | copy 文件，改名         | cp  -rp source destination <br/> cp file1 file2 folder (copy 多个文件) |
  | mv                    | /bin/mv       | -         | Move, 改名              | mv /tmp/software /tmp/machine_learning mv file1 file2        |
  | rm                    | /bin/rm       | -         | Remove                  | rm -rf 文件或目录 f:force                                    |

- 文件处理命令

  | command name | Path          | Access    | Func               | Grammar                                                   |
  | ------------ | ------------- | --------- | ------------------ | --------------------------------------------------------- |
  | touch        | /bin/touch    | all users | 创建文件           | touch path/file：touch file.txt     touch "program files" |
  | cat          | /bin/cat      | -         | 显示文件           | cat -n files <br/>  -n: 显示行号                          |
  | tac          | /usr/bin/tac  | -         | 从最后一行开始显示 | tac 路径/文件                                             |
  | more         | /bin/more     | -         | 分页显示文件内容   | more 文件名 f或者空格:翻页，enter换行，q退出              |
  | less         | /usr/bin/less | -         | 分页显示，向上翻   | less 文件名，pageup，上箭头，/keyword：搜索，n            |
  | head         | /usr/bin/head | -         | 显示文件前面几行   | head -n 20 /etc/services                                  |
  | tail         | /usr/bin/tail | -         | 文件后面几行       | tail -nf /etc/services -f:动态显示文件末尾内容。监控日志  |

  

- 链接命令

  | command name | Path    | Access    | Func         | Grammar                                         |
  | ------------ | ------- | --------- | ------------ | ----------------------------------------------- |
  | ln           | /bin/ln | all users | 生成链接文件 | ln -s 源文件 目标文件 <br/> -s:create soft link |
  
  ln **-s** file files.soft：快捷方式，rwx权限。源文件删除，软连接也就不存在。可以跨分区，对目录可以。
  
  ln file files.hard：硬链接不能跨分区，不可以对目录进行硬链接；与源文件同时更新
  
  

2. <a id="anchor1">权限管理命令</a>

- Chmod: change the permissions mode of a file

  | command name | Path          | Access                  | Func                                                | Grammar                                                      |
  | ------------ | ------------- | ----------------------- | --------------------------------------------------- | ------------------------------------------------------------ |
  | chmod        | /bin/chmod    | all users               | change the permissions mode of a file               | chmod ugoa +-= rwx file/folder, -R<br/> chmod o-w Python (other用户移除w权限)<br/>chmod 641 software/Python <br/> chmod -R 666 Python |
  | chown        | /bin/chown    | Root 可以改文件的所有者 | change file ownership                               | chown 用户 文件或者目录<br/>chown Sharon Heng                |
  | chgrp        | /bin/chgrp    | -                       | Change file group ownership                         | chgrp 用户组 文件或者目录<br/>1.Add groud：groupadd Linux_P用户组<br/> chgrp Linux_P Python (1.user name, 2.Group name)<br/> 当chmod改变文件的权限，文件的所属组的权限也被改变。 |
  | umask        | Shell内置命令 | -                       | the user file-creation mask显示和设置文件的缺省权限 | umask -S, -S:以rwx形式显示新建文件缺省权限 <br/> umask: 0022: ----w--w-<br/> **umask -S**：777-022=755<br/> If umask-->023: **umask 023** 就可以了 |


3. <a id="anchor2">文件搜索命令</a>

- dff

  | command name | Path      | Access    | Func     | Grammar                |
  | ------------ | --------- | --------- | -------- | ---------------------- |
  | find         | /bin/find | all users | 文件搜索 | find 搜索范围 匹配条件 |





4. <a id="anchor3">用户管理命令</a> 

5. <a id="anchor4">网络命令</a>

   | command name | Path            | Access    | Func                                   | Grammar                                                      |
   | ------------ | --------------- | --------- | -------------------------------------- | ------------------------------------------------------------ |
   | write        | /usr/bin/write  | all users | 给用户发信息，以Ctrl+D保存结束         | write UserName （在线用户）**w：**查看哪些用户在线           |
   | wall         | /usr/bin/wall   | -         | write all发广播信息                    | wall message<br/> **wall** Sh is a honest person.            |
   | ping         | /bin/ping       | -         | 测试网络连通性                         | ping -c IP地址<br/> -c: 指定发送次数。ping 192.168.1.156     |
   | ifconfig     | /sbin/ifconfig  | root      | interface configure 查看和设置网卡信息 | ifconfig 网卡名称 IP地址<br/> ifconfig eth0 10.2.56.116      |
   | mail         | /bin/mail       | -         | send email                             | mail root<br/> 邮件序列号1:查看邮件内容 h:查看邮件列表。d No：删除第N邮件。 |
   | last         | /usr/bin/last   | -         | 列出到目前为止，以前的登录用户信息     | last                                                         |
   | traceroute   | /bin/traceroute | -         | 显示数据包到主机间的路径               | Traceroute www.google.com                                    |
   | netstat      | /bin/netstat    | -         | 显示网络相关信息                       | netstat 选项<br/> -t: TCP协议。-u: UCP -l: 监听 -r:路由 -n:显示IP地址和端口号, -s:统计信息<br/> netstat -tlun: 查看本机监听的端口<br/> netstat -an: 查看本机所有的网络连接<br/> netstat -rn: 查看本机路由表 |
   | setup        | /usr/bin/setup  | root      | 配置网络                               | setup                                                        |
   | mount        | /bin/mount      | -         | 挂载命令                               | umount device名<br/> mount -t iso9660 /dev/sr0 /mnt/cdrom    |
   | ss           |                 |           | Socket Statistics查看系统套接字信息）  | TCP、UDP和UNIX套接字；IPv4和IPv6套接字信息<br/> ss -t；ss -4 |
   | ssh          |                 |           |                                        |                                                              |
   | ftp          |                 |           |                                        |                                                              |
   | nc           |                 |           |                                        |                                                              |
   | curl         |                 |           |                                        |                                                              |
   | host         |                 |           |                                        |                                                              |

   ╰─○ netstat route：两个命令及其相似，查看网络相关信息。
   Active Internet connections
   Proto Recv-Q Send-Q  Local Address          Foreign Address        (state)
   tcp4       0      0  10.2.56.116.**60163** 端口(**收信人**)     3.3.9.1.https          ESTABLISHED
   tcp4       0      0  10.2.56.116.60162      ec2-3-226-133-20.https ESTABLISHED

   - 如果查看ssh进程的所有连接信息：netstat -ap | grep ssh （搜索进程为ssh的网卡信息）

   ss：socket Statistics显示套接字信息：其中套接字是什么，功能是什么？

   套接字：IP地址:端口号就是套接字Socket；是应用层与传输层之间的接口，提供一种机制，使应用程序能够通过网络发送和接收数据。

   作用：**建立通信连接**：端到端，点对点的链接。

   

6. <a id="anchor5">关机重启命令</a>

7. <a id="anchor6">帮助命令及压缩解压命令</a>

- 

  | command name | Path | Access | Func | Grammar |
  | ------------ | ---- | ------ | ---- | ------- |
  |              |      |        |      |         |

  



| Command    | Func                                           | Return                                                       |
| ---------- | ---------------------------------------------- | ------------------------------------------------------------ |
| **uptime** | 查看系统负载和运行时间                         | ╰─○ uptime<br/>15:21  up 23:24, 4 users, load averages: 2.29 2.14 2.30  <br/> 当前时间：显示了当前系统时间。 <br/>运行时间：表示自上次启动系统以来的时间。它通常以天、小时、分钟的形式显示。 <br/>用户登录数量：显示当前登录到系统的用户数量。 平均负载：系统的平均负载是过去1分钟、5分钟和15分钟内的平均负载。这些数字告诉您系统在这些时间段内的工作负荷。 |
| **Top**    | 实时查看系统运行状态(Monitor system Resources) | $ top -b -n 1 \| tee output (save and check the result of output) <br/>$ top -b -n 1 > output (See all output) |
|            |                                                |                                                              |
|            |                                                |                                                              |
|            |                                                |                                                              |
|            |                                                |                                                              |
|            |                                                |                                                              |
|            |                                                |                                                              |

<img src="img/image-20230921161827990.png" alt="image-20230921161827990" style="zoom:40%;" />

<img src="img/image-20230921162337585.png" alt="image-20230921162337585" style="zoom:60%;" />

The following items represent: the percentage of CPU use

us: user CPU time：running users' processes that are not niced

sy: system CPU time: running the kernel and kernel processes.

ni: nice CPU time: user's processes that have been niced

id: CPU idle time: idle

wa: I/O wait: waiting for I/O

hi: hardware interrupts: time spent servicing hardware interrupts.

si: software interrupts: 

st: steal time: CPU time was stolen from you for other tasks.



# 计算机网络

<a id="Network">计算机网络</a>

## TCP/IP的分层

- 应用层：应用层决定了向用户提供应用服务时通信的活动。FTP (FileTransfer protocol), DNS(Domain name system), HTTP
- 传输层: 传输层对上层应用层，提供处于网络连接中的两台计算机之间的数据传输。两个协议：**TCP**（Transmission ControlProtocol，传输控制协议）和**UDP**（User Data Protocol，用户数据报协议）
- 网络层（又名网络互连层）：网络层用来处理在网络上流动的数据包。规定了通过怎样的路径（所谓的传输路线）到达对方计算机
- 链路层：用来处理连接网络的硬件部分。



<img src="https://pic3.zhimg.com/80/v2-374cdd724c5dd716d6cdc32760fd9842_1440w.webp" alt="img"  />

### TCP/IP协议

| Protocol          | Position | Func                             | Features                                                     |
| ----------------- | -------- | -------------------------------- | ------------------------------------------------------------ |
| IP协议            | 网络层   | 作用是把各种数据包传送给对方     | 两个重要的条件是 IP 地址和 MAC地址Media Access Control Address |
| TCP协议           | 传输层   | 提供可靠的字节流服务             | 为了准确无误地将数据送达目标处，TCP 协议采用了三次握手（three-way handshaking）策略 |
| DNS服务，HTTP协议 | 应用层   | 提供域名到 IP 地址之间的解析服务 |                                                              |



### IP协议



### TCP协议

三次握手：发送端首先发送一个带**控制位** **SYN 标志**的数据包给对方。接收端收到后，回传一个带有 **SYN/ACK 标志**的数据包以示传达确认信息。最后，发送端再回传一个带 **ACK 标志**的数据包，代表“握手”结束。SYN（synchronize） 和ACK（acknowledgement）

<img src="https://pic2.zhimg.com/80/v2-ab9be497c3c02f49cac02240ebc5b3a5_1440w.webp" alt="img" style="zoom:80%;" />

例如：客户端：序号：8633             服务器：序号303，确认号：8633+1          客户端：序号：对方的确认号：8633+1  确认号：303+1

为了节省资源，服务器则不保存自己的序号，而是根据服务器的ip地址和端口号等私有信息进行算法运算得到序号。

三次握手-->客户端发出请求-->服务器相应请求-->关闭连接

#### 关闭连接

客户端和服务端都可以发起关闭请求。

发起方：发送FIN+ACK，序号a，确认号b。

接收方：发送ACK，序号：**对方确认号b**，确认号：对方的序号a+1。

​		再发FIN+ACK，序号和确认号不变

发起方：发送ACK，序号：a+1（对方确认号），确认号：b+1（对方序号+1）

### HTTP协议

HTTP（Hypertext Transfer Protocol）是在计算机网络中传输超文本文档（例如网页）的应用层协议。

HTTP的主要特点和作用包括：

1. **无状态协议**：HTTP是一种无状态协议，每个HTTP请求都是独立的，服务器不会在请求之间保留任何关于客户端状态的信息。这意味着每个请求都必须包含所有必要的信息，包括请求方法、URL、头部、主体等。
2. **基于文本**：HTTP使用文本格式来传输数据，通常采用ASCII编码。HTTP请求和响应都包含有关请求的信息、响应状态和数据内容。
3. **请求-响应模型**：HTTP遵循请求-响应模型，客户端发送HTTP请求给服务器，服务器处理请求并返回HTTP响应。响应包括状态码（例如200 OK、404 Not Found）、响应头和响应主体（包含所请求的数据）。
4. **支持不同的HTTP方法**：HTTP定义了不同的请求方法，最常见的是GET（获取资源）、POST（提交数据）、PUT（更新资源）、DELETE（删除资源）等。这些方法定义了客户端与服务器之间的交互方式。
5. **支持HTTPS**：HTTP可以使用加密层来增强安全性，称为HTTPS（HTTP Secure）。HTTPS使用TLS/SSL来加密数据传输，确保数据在网络上的安全性和隐私性。
6. **状态管理**：虽然HTTP本身是无状态的，但Web应用程序通常使用会话（Session）和Cookie等机制来管理客户端的状态。这允许Web应用程序在多个HTTP请求之间保持用户会话信息。
7. **多媒体资源传输**：HTTP不仅可以传输HTML文档，还可以传输图像、视频、音频和其他多媒体资源，使互联网上的各种内容能够通过浏览器访问。

报文格式和内容：报文通过**传输层协议TCP**将信息传送出去。

|                      | request Message                                              | response Message                                             |          |
| -------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | -------- |
| 请求行               | 请求方法、请求的URI（Uniform Resource Identifier，统一资源标识符）和HTTP协议版本 | HTTP协议版本、状态码和状态短语。E: HTTP/1.1 200 OK           | 状态行   |
| 请求头部             | 包括各种请求的元数据信息，例如主机名、用户代理、接受的媒体类型等。<br/>e.g：Host: www.example.com | 各种响应的元数据信息，例如服务器类型、响应时间、内容类型等。Server: Apache/2.4.41 (Unix) **Content-Type:** text/html; charset=UTF-8 | 响应头部 |
| 空行                 |                                                              |                                                              |          |
| 请求主体request body | 包含客户端向服务器发送的数据。通常在POST请求中使用，例如提交表单数据。如登录的信息 | 服务器返回的实际数据，例如HTML页面、文本内容、图像或其他媒体。 | 响应body |



HTTP状态码：

| name | meaning                                                      |
| ---- | ------------------------------------------------------------ |
| 2**  | 成功  （204 No Content：请求成功，但相应结果：没有内容）     |
| 3**  | 重定向 （304：使用缓存信息，页面没有改变）                   |
| 4**  | 客户端错误（404：server没有找到客户端请求信息，原因可能是typo，page移动位置） |
| 5**  | 服务端错误（500 Internal Server Error504：服务器没有及时收到上游服务器的响应，无法满足请求） |

服务端发送数据时，带有Content-Type内容类型。

#### Session Cookie

Here's a summarized comparison of Cookies and Sessions in a table format:

| Aspect               | Cookies                                                      | Sessions                                                     |
| -------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **Storage Location** | Client-side (browser) 存储在客户端                           | Server-side 存储在服务器上                                   |
| **Security**         | Vulnerable to client-side access and manipulation客户端可访问和修改 | More secure as data is stored on the server服务器端更安全    |
| **Storage Capacity** | Limited (typically around 4KB)                               | Generally larger, no strict size limit                       |
| **Lifecycle**        | Can have expiration (session-level or persistent)            | Tied to the user session, managed by the server与用户会话相关 |
| **Use Cases**        | Tracking user identity, maintaining login state, storing small preferences跟踪用户身份、保持登录状态、存储用户首选项 | Storing sensitive data, shopping cart contents, user login state (securely) 存储用户敏感信息、购物车内容、用户登录状态 |

Remember that the choice between Cookies and Sessions depends on your application's specific requirements, security considerations, and performance needs. It's also common to use both together, with Cookies storing a session ID and Sessions managing the session data on the server.

DNS（Domain Name System）解析是将人类可读的域名转换为计算机可理解的IP地址的过程。这个过程包括多个步骤，通常在发起网络请求时发生。以下是DNS解析过程的简要步骤：

1. **用户发起请求**：当用户在Web浏览器中输入一个域名（例如www.example.com）来访问一个网站时，或者在应用程序中访问网络资源时，首先发起了一个DNS解析请求。
2. **本地DNS缓存查询**：操作系统会首先检查本地DNS缓存，看看是否已经解析过该域名。如果之前已经解析过，系统会直接使用缓存的IP地址，而不会发起新的DNS查询。
3. **本地DNS服务器查询**：如果本地缓存中没有域名的解析记录，操作系统会将DNS查询发送给本地DNS服务器，通常由Internet服务提供商（ISP）或其他网络服务提供商提供。
4. **递归查询**：如果本地DNS服务器也没有域名的解析记录，它会根据域名的顶级域（例如.com、.org）向根DNS服务器发起递归查询。根DNS服务器将指示本地DNS服务器向顶级域的DNS服务器发起查询。
5. **顶级域DNS服务器查询**：本地DNS服务器向顶级域的DNS服务器发起查询，顶级域DNS服务器会指示本地DNS服务器查询下一级DNS服务器，即负责二级域的DNS服务器。
6. **权限DNS服务器查询**：递归查询一直沿着域名层次结构向下进行，直到到达负责解析特定域名的权限DNS服务器。这个服务器包含了所需域名的IP地址记录。
7. **获取IP地址**：本地DNS服务器从权限DNS服务器接收到域名对应的IP地址后，将其存储在本地缓存中，以便将来使用。然后，它将IP地址返回给操作系统。
8. **访问目标服务器**：操作系统接收到IP地址后，将使用该地址与目标服务器建立TCP/IP连接，以便获取所请求的网页或资源。
9. **响应用户请求**：目标服务器收到请求后，会响应用户的请求，将所需的网页或资源传输回用户的浏览器或应用程序。

这个过程中，DNS解析是透明的，用户通常无需手动进行DNS查询。它是互联网上访问网站和资源的关键步骤之一，确保用户可以使用域名而不是IP地址来访问网站，使互联网更加用户友好和可访问。



DHCP（Dynamic Host Configuration Protocol）是一种用于自动分配IP地址和其他网络配置信息的网络协议，它的运行原理和握手过程如下：手动的话，不得不确保：每个用户有一个IP地址。

**DHCP运行原理：**

DHCP的目标是使网络中的计算机自动获取所需的网络配置信息，而不需要手动配置。它通过以下方式实现：

1. **DHCP服务器**：在网络中存在一个或多个DHCP服务器，它们负责分配IP地址和其他网络配置信息给客户端设备，（如路由器）。

2. **DHCP客户端**：客户端设备（例如计算机、手机或其他网络设备）在连接到网络时会发送DHCP请求，以获取配置信息。

3. **IP地址池**：DHCP服务器管理一个IP地址池，其中包含可以分配给客户端的IP地址。当客户端请求IP地址时，DHCP服务器从池中选择一个未分配的地址分配给该客户端。

**DHCP握手过程：**

DHCP握手过程通常包括四个阶段：发现（Discover）、提供（Offer）、请求（Request）和确认（Acknowledge）。以下是每个阶段的详细描述：

1. **发现（Discover）**：在这个阶段，客户端设备启动并需要获取IP地址和其他配置信息。它会发送一个DHCP Discover消息广播到网络上，表示需要DHCP服务。**应用层 从0.0.0.0发送，255.255.255.255进行广播。requestd IP地址：0.0.0.0或者旧的IP地址。**
2. **提供（Offer）**：DHCP服务器接收到Discover消息后，会回应一个DHCP Offer消息，其中包含了可以提供的**IP地址，子网掩码，网关和DNS**。服务器可以选择**一个未分配的IP地址**并分配给客户端。
3. **请求（Request）**：客户端在收到一个或多个DHCP Offer消息后，会选择一个Offer，并发送一个DHCP Request消息，请求分配该IP地址。如果有多个DHCP服务器，客户端可以选择其中一个Offer并发送Request。**requestd IP地址：分配到的IP地址。**
4. **确认（Acknowledge）**：DHCP服务器收到客户端的Request消息后，会确认并响应客户端的请求，发送一个DHCP Acknowledge消息，包含分配给客户端的IP地址和其他配置信息。

一旦客户端收到DHCP Acknowledge消息，它会配置自己的网络接口，将IP地址和其他配置信息应用到网络连接上。此时，客户端已经成功获取了所需的网络配置信息，并可以开始正常通信。

需要注意的是，DHCP握手过程中的消息通常使用UDP协议在局域网内广播或单播传递。这样，DHCP客户端可以在网络中找到可用的DHCP服务器，而DHCP服务器可以响应客户端的请求。DHCP是一种自动化网络配置的重要协议，用于简化网络管理和提高效率。



以下是HTTP/1.1、HTTP/2和HTTP/3的区别的汇总表格：

| 特征           | HTTP/1.1      | HTTP/2                   | HTTP/3                     |
| -------------- | ------------- | ------------------------ | -------------------------- |
| 并发连接处理   | 单一TCP连接   | 多路复用（Multiplexing） | 多路复用（Multiplexing）   |
| 头部压缩       | 不支持        | 支持（HPACK算法）        | 支持（HPACK算法）          |
| 安全性         | 需要HTTPS加密 | 默认使用TLS加密          | 默认使用QUIC协议，自带加密 |
| 流控制         | 不支持        | 支持                     | 支持                       |
| 优化的头部处理 | 未优化        | 使用二进制帧格式         | 使用二进制帧格式           |
| 连接和传输协议 | TCP           | TCP                      | QUIC（在UDP上）            |

这张表格总结了HTTP/1.1、HTTP/2和HTTP/3之间的主要区别，包括并发连接处理、头部压缩、安全性、流控制、头部处理以及连接和传输协议。HTTP/2和HTTP/3引入了许多性能和效率的改进，使其成为现代Web应用程序的首选选择，特别是在移动网络和高延迟网络环境中。

**1. 并发连接处理：**

- **HTTP/1.1**：在HTTP/1.1中，每个HTTP请求通常需要一个单独的TCP连接。这意味着每个资源请求都需要等待连接建立、请求-响应往返，这可能导致性能瓶颈和延迟。
- **HTTP/2**：HTTP/2引入了多路复用（Multiplexing）机制，允许多个请求和响应在一个单一的TCP连接上并行传输。这显著提高了性能，减少了延迟。
- **HTTP/3**：HTTP/3在传输层使用QUIC协议，类似于HTTP/2的多路复用，但更为高效。它进一步减少了延迟，并通过快速连接建立提供了更好的性能。

2. 头部报文：
   - Http/2: 头部变成二进制的帧；默认TLS加密。解决了HTTP层面的对头阻塞
3. 协议：
   1. HTTP/3:将HTTP/2的TCP握手，TLS/1.3握手整合，成为QUIC握手
