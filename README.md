# QST_Hadoop_Project

## 项目背景

某电商平台XD，每天有大量的用户访问，XD的产品经理ZB，想了解现在网站的访问情况，于是提出了一个需求

1. 需要看到网站的访问情况
    1. 包括PV、UV
2. 需要符合大数据的概念
3. 必须支持后的开发需求，要尽量高的开发效率

## 项目开展

本次项目的负责人是：

项目分4个阶段开展

## Round 1

本回合完成任务主要完成：

1. 完成设计方案
    1. 方案内容填写在./Round1/README.md 文件里
    2. 方案包含所有操作的内容，由环境搭建，到最后的代码运行
2. 完成环境搭建
    1. 建议进行操作一遍
3. 完成以下统计需求
    1. 完成每天的UV统计
    2. 完成每天访问量Top10的Show统计
    3. 完成每天的次日留存统计

相关资料完成后，请发起pull request，里面标题填上自己的名字。

数据在客户端本地磁盘 /home/hadoop/qst/ray/2015-1\* ， 在HDFS上也有 /user/hadoop/hadoop_project/*


方案介绍： 通过MapReduce map（利用正则表达式将数据拆分 每一行保留用户的 ip地址、访问时间，存放到set集合中进行去重） reduce（通过map得到的数据进行统计即为UV的数量，通过排序得到每天Top10的数据 并将每天的数据进行统计保存下来方便第二天的查询） 环境搭建： 安装虚拟机，将网卡改成桥接网卡 安装openssh-client与lrzsz 配置Java环境 vim /home/hadoop/.bashrc 最后一行添加 export JAVA_HOME=/home/hadoop/jdk1.6.0_45/ export CLASSPATH=.:$CLASSPATH:$JAVA_HOME/lib:$JRE_HOME/lib export PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin 输入source ~/.bashrc 测试Java配置是否成功 Java-version 安装Hadoop 配置相应的文件（修改master文件、slaves文件、core-site.xml、mapred-site.xml、hdfs-site.xml、hadoop-env.sh、sudo vi /etc/hosts） 配置成功后复制该虚拟机两到三台 建立互信关系：在master生成公私钥ssh-keygen 复制公钥cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys 同样在slave机器上输入ssh-keygen 从master机器上复制公钥scp master:~/.ssh/authorized_keys /home/hadoop/.ssh/ 测试连接 启动Hadoop bin目录下./hadoop namenode –format 启动执行./start-all.sh 查看jps 看进程是否正常启动。
完成每天的UV统计
 把每天的用户访问数据通过mapreduce处理，用正则表达式将数据进行分割，分割出IP，IP为key值，value为1
 最后用reduce统计，输出IP和访问次数
 完成每天的访问量Top10的Show统计
 将上步骤统计的结果以哈希表形式存储，将IP出现次数最高的前十个展示
 完成每天的次日留存统计
 把第一天的数据和第二天的数据都进行一个mapreduce处理，然后以哈希表形式存储，用表全连接查看留存


