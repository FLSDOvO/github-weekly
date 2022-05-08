# Github Weekly 02 q



## 介绍

q 是一个命令行工具，可以对表格式的文件执行SQL语句实现对数据的查询。



它支持几乎所有sqlite标准的SQL查询语法。此外，还拥有自动识别列名、列类型，支持自适应编码等特性，用户友好。



## 应用示例



### csv记录了某平台用户粉丝量，查询大于百万粉的用户，并按照粉丝量数量大到小排序

    
    q -d "," "select * from data.csv where c2 > 100*10000 order by c2 desc"
    



### 计算拥有进程数最多的前3位用户名及其数量

    
    ps -ef | q -H "SELECT UID,COUNT(*) cnt FROM - GROUP BY UID ORDER BY cnt DESC LIMIT 3"
    

使用 **-H** 自动识别了列名

### 输出在/tmp目录下，相同用户的文件所占用的KB磁盘空间, 指定并显示列名

    
    sudo find /tmp -ls | q -O "select c5 user,sum(c7)/1024.0 total from - group by user"
    

使用 **-O** 显示表头列名

### 输出1到1000的平均数与和数,并将原始数据转存到sqlite中

    
    seq 1 1000 | q "select avg(c1),sum(c1) from -" -S result.db
    

## 小结

可以将 q 和其他Linux工具搭配使用，可以将 q 看作提供了 SQL 功能（表达式、排序、分组、聚合等）的元工具，就如同使用管道将 awk/sed 和 grep 搭配使用一样。



项目地址：[http://github.com/harelba/q](http://github.com/harelba/q)

文档地址：[https://harelba.github.io/q/index\_cn/](https://harelba.github.io/q/index_cn/)

下载地址：[http://github.com/harelba/q/releases](http://github.com/harelba/q/releases)

