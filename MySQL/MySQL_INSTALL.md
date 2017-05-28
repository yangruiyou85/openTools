1.MySQL5.7源码编译
#预先下载，存放在MySQL解压缩目录

http://googlemock.googlecode.com/files/gmock-1.7.0.zip


cmake . -DCMAKE_INSTALL_PREFIX=/usr/local/mysql \
-DMYSQL_DATADIR=/data/dbdata \
-DWITH_INNOBASE_STORAGE_ENGINE=1 \
-DWITH_PARTITION_STORAGE_ENGINE=1 \
-DWITH_PERFSCHEMA_STORAGE_ENGINE=1 \
-DWITH_BLACKHOLE_STORAGE_ENGINE=1 \
-DWITH_MYISAM_STORAGE_ENGINE=1 \
-DMYSQL_UNIX_ADDR=/usr/local/mysql/tmp/mysql.sock \
-DMYSQL_TCP_PORT=3306 \
-DENABLED_LOCAL_INFILE=1 \
-DWITH_EXTRA_CHARSETS=all \
-DDEFAULT_CHARSET=utf8 -DDEFAULT_COLLATION=utf8_general_ci  \
-DENABLED_LOCAL_INFILE=1 \
-DENABLED_PROFILING=1 \
-DDOWNLOAD_BOOST=1 \
-DWITH_BOOST=. \
-DENABLE_DOWNLOADS=1





#MySQL5.7初始化
[root@zabbix-n1 dbdata]# /usr/local/mysql/bin/mysqld  --user=mysql --initialize  --initialize-insecure

修改下用户密码















