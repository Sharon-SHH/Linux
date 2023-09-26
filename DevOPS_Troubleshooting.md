

# CHAPTER 5 Is the Server Down? Tracking Down the Source of Network Problems

Server A Can't Talk to Server B

​	Client or Server Problem

​	Is It Plugged In? **Ethtool eth0 ** (client connections is health or not)

Is the Interface Up? **Ifconfig eth0** (confirm that the network interface i configured correctly on your host)

Is It on the Local Network? **route -n** (if a default gateway has been set and whether you can access it) Then, **ping ip** 

Is DNS Working? **nslookup** web1, **dig** （将域名转变为IP地址：ping host）

Can I Route to the Remote Host? 测试路由问题的工具：traceout www.google.com，显示数据包到主机间的路径：先到gateway，再到Google网站

Is the Remote Port Open?查看端口是否开着：**telnet** 10.1.2.5 80； **nmap** -p 80 10.1.2.5 （可detect防火墙）--**对方的主机**是否运行。

Test the Remote Host Locally：**netstat** -lnp | grep :80  所有**本地机器**正在监听的端口以及打开端口的进程，监听80端口。

Troubleshoot Slow Networks。 `iftop` or `nload ` how to Check for Bandwidth Utilization带宽利用率，查看哪些进程在大量占用I/O

DNS Issues：

Find the Network Slowdown with **traceroute**：本地与远程服务器的网络，网速慢，都可以用traceroute

Find What Is Using Your Bandwidth with iftop：top，iftop。

Packet Captures：low-level的问题，

Use the tcpdump Tool：

root权限，扫描然后捕获，解析并输出所有数据包信息。tcpdump -n，不会将ip地址转换成主机名。sudo **tcpdump** -n

Use Wireshark：桌面应用。（解析和分析原始数据包时）



查看server是否工作的命令：ping telnet nmap ssh登录

# CHAPTER 8 Is the Website Down? Tracking Down Web Server Problems

Is the Server Running?  Chapter 5

Is the Remote **Port** Open? telnet 10.1.2.5 80， nmap

Test the Remote Host Locally：**netstat** -lnp | grep :80  所有正在监听的端口以及打开端口的进程，监听80端口。

Test a Web Server from the Command Line

Test Web Servers with **Curl**：用于下载文件、访问Web服务、测试API。支持多种协议，http，https，curl www.baidu.com：返回网页内容

Test Web Servers with **Telnet**：用于远程登录到另一台计算机或主机的命令，如SSH。用于调试和测试网络服务的连通性。

确认端口，然后确认网络服务器实际相应请求：curl，telnet，ssh

Parse Web Server Logs

Get Web Server Statistics

Solve Common Web Server Problems

​	Configuration Problems：nginx

​	Permissions Problems：curl www.baidu.com： 403 forbidden error。chmod增加权限。

​	Sluggish or Unavailable Web Server：

		- cpu负载：查看网络服务器日志-》确定哪些网页在高负载期间被访问。
		- RAM负载：面临网络服务器交换死亡螺旋。配置网络服务器：最大网络服务器实例的最大数量。





# CHAPTER 9 Why Is the Database Slow? Tracking Down Database Problems 

Search Database Logs：error log. /var/log/ or /var/lib/

​	**High server load - DB:** 

| name           | Problem                                                      |
| -------------- | ------------------------------------------------------------ |
| CPU-bound load | Bad SQL query                                                |
| RAM-bound      | tune DB (调整数据库)， 减少同时进行的查询次数。找出占用RAM多的SQL查询 |
| I/O-bound      | 用iotop工具识别哪个进程，用sysstat查询哪个存储空间收到冲击最大。 |



**Is the Database Running?**

​	MySQL：sudo service mysql status。running：735. 

		- 在ps -ef | grep mysql。查看进程 ID是否和上面的一直。
		- 监听端口是否正确：sudo netstat -lnp | grep :3306

​	PostgresSOL

**Get Database Matrix: track DB problem.**

​	MySQL: **mysqladmin** tool.

**Identify Slow Queries**

MySQL：enable slow query logging：**log_slow_queries** =/var/log/mysql/mysql-slow.log and **long_query_time** = 2（s）.

PostgresSQL



High server load高服务器负载通常意味着服务器的资源（如 CPU、内存、磁盘或网络）正在受到大量请求或负载，可能需要进一步诊断来确定问题的根本原因。以下是一些命令和工具，可用于查看服务器的负载情况和确定问题所在：

1. **查看负载平均值**：
   - 使用 `uptime` 命令来查看服务器的平均负载值。平均负载是一个三个数字的指标，分别表示过去1分钟、5分钟和15分钟的平均负载。
   ```
   uptime
   ```

2. **查看进程**：
   - 使用 `top` 或 `htop` 命令来查看当前正在运行的进程，以及它们的CPU和内存使用情况。
   ```
   top
   ```
   或
   ```
   htop
   ```

3. **查看进程使用的CPU**：
   - 使用 `top` 命令，按 `Shift+P` 键可以按CPU使用率对进程进行排序，以查看哪些进程占用了大量的CPU资源。

4. **查看内存使用**：
   - 使用 `free` 命令来查看服务器的内存使用情况。
   ```
   free -m
   ```

5. **查看磁盘使用**：
   - 使用 `df` 命令来查看服务器的磁盘使用情况，以确保磁盘空间没有耗尽。
   ```
   df -h
   ```

6. **查看网络使用**：
   - 使用 `iftop` 命令来实时监视网络流量，以检查是否有大量的网络活动。
   ```
   iftop
   ```

7. **查看日志文件**：
   - 检查系统日志（通常在 `/var/log` 目录下）以查看是否有异常事件、错误消息或警告，这些可能是高负载的原因。

8. **检查应用程序日志**：
   - 如果服务器上运行着特定应用程序（如数据库、Web服务器等），请检查该应用程序的日志文件以查找问题。

9. **使用监控工具**：
   - 部署服务器监控工具（如Nagios、Zabbix、Prometheus等）来持续监视服务器性能，并设置警报以便及早发现问题。

10. **检查数据库性能**：
    - 如果服务器上运行数据库，使用数据库管理工具来分析数据库性能和查询负载。

高服务器负载可能是由于各种原因，包括恶意攻击、恶意脚本、系统资源不足、配置问题等。通过以上命令和方法，您可以更详细地了解服务器的负载情况，然后根据问题的具体性质采取相应的措施来解决它。如果问题持续存在，可能需要深入的故障排除和性能优化。
