
# 什么是flume   
## flume是apache的顶项目  看地址便知
http://flume.apache.org/
<ol>
  ......
  </ol>
##  install  flume

[hadoop@hadoop soft]# wget http://archive.cloudera.com/cdh5/cdh/5/flume-ng-1.6.0-cdh5.7.0.tar.gz
[hadoop@hadoop soft]# tar -zxvf flume-ng-1.6.0-cdh5.7.0.tar.gz
[hadoop@hadoop soft]# mv flume-ng-1.6.0-cdh5.7.0.tar.gz flume
[hadoop@hadoop soft]# mv flume/ ../app
[hadoop@hadoop soft]# chmod 755 -R  ../app/flume
[hadoop@hadoop soft]# vi ~/.bash_profile
export FLUME_HOME=/hadoop/app/flume
export PATH=$PATH:$FLUME_HOME/bin
[hadoop@hadoop soft]# source ~/.bash_profile


[hadoop@hadoop ~]$ mkdir -p /home/hadoop/script/flume

[hadoop@hadoop flume]$ pwd
/home/hadoop/script/flume
[hadoop@hadoop flume]$ vi logger.conf


#定义 sources,sinks,channels的名称
a1.sources = s1
a1.sinks = k1
a1.channels = c1
#定义 sources 的属性
a1.sources.s1.type = netcat
a1.sources.s1.bind = 0.0.0.0
a1.sources.s1.port = 44444
#定义 sinks 的属性
a1.sinks.k1.type = logger
#定义 channels 的属性
a1.channels.c1.type = memory
#对 channel 的绑定
a1.sources.s1.channels = c1
a1.sinks.k1.channel = c1
#开启服务
[hadoop@hadoop flume]$ flume-ng agent --name a1 --conf $FLUME_HOME/conf \
--conf-file /home/hadoop/script/flume/logger.conf \
-Dflume.root.logger=INFO,console \
-Dflume.monitorint.type=http \
-Dflume.monitoring.port=34343
#telnet sources定义的端口,输入信息后在开启服务的窗口有内容返回即是成功
[hadoop@hadoop flume]$ telnet localhost 44444


	
需求：采集指定文件的内容到HDFS
技术选型：exec - memory - hdfs

./flume-ng agent \
--name a1 \
--conf $FLUME_HOME/conf \
--conf-file /home/hadoop/script/flume/exec-memory-hdfs.conf \
-Dflume.root.logger=INFO,console \
-Dflume.monitoring.type=http \
-Dflume.monitoring.port=34343






##  hue 安装 很难 慢慢看 
tar -xzvf hue-3.9.0-cdh5.7.0.tar.gz
  需要按照官网的 PREFIX=/usr/share make install
   安装到/usr/share/hue下
直接进入 hue目录   如果是git clone https://github.com/cloudera/hue.git 就用 make  app（估计和版本有关）

第一步，在每个hadoop的配置文件core-site.xml添加这些语句

  <!-- Hue WebHDFS proxy user setting -->

 

        <property>

               <name>hadoop.proxyuser.hue.hosts</name>

                <value>*</value>

        </property>

 

        <property>

               <name>hadoop.proxyuser.hue.groups</name>

                <value>*</value>

        </property>

 

第二步，在每个hadoop的配置文件hdfs-site.xml添加这些语句

        <property>

                <name>dfs.webhdfs.enabled</name>

                <value>true</value>

        </property>

 

Hadoop集群重启，分别启动hdfs和yarn
# 启动hue
cd /usr/share/hue/build/env/bin
supervisor &
# 关闭hue
pkill -U hue
或者
killall -u hue
