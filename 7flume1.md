
# 什么是flume   
## flume是apache的顶项目  看地址便知
http://flume.apache.org/





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
