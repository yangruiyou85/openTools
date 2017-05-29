#HAProxy安装
##########################
##centos 6.7 x86_64


##uname -a //查看linux内核版本
make TARGET=linux26 PREFIX=/usr/local/haproxy
make install PREFIX=/usr/local/haproxy
useradd -s /sbin/nologin haproxy
passwd haproxy
chown -R haproxy.haproxy /usr/local/haproxy
cp /softs/haproxy-1.5.12/examples/haproxy.cfg  /usr/local/haproxy/

##haproxy.cfg配置文件
global
log 127.0.0.1 local0
log 127.0.0.1 local1 notice
maxconn 4096
uid 99
gid 99
daemon

#debug
#quiet
defaults
log global
mode http
option tcplog
option dontlognull
retries 3
maxconn 2000
listen mysql-cluster 0.0.0.0:3306
mode tcp
balance roundrobin
option mysql-check user root
server centos2 172.16.19.3:3306 check
server centos3 172.16.19.4:3306 check
server centos4 172.16.19.5:3306 check


*. 启动
/usr/local/haproxy/sbin/haproxy -f /usr/local/haproxy/haproxy.cfg
*关闭
killall haproxy

*重启
/usr/local/haproxy/sbin/haproxy -f /usr/local/haproxy/haproxy.cfg -p /usr/local/haproxy/haproxy.pid -sf `cat /usr/local/haproxy/haproxy.pid`




##haprxoy.cfg配置文件模板


global
    log         127.0.0.1 local3
    chroot      /var/lib/haproxy
    pidfile     /var/run/haproxy.pid
    maxconn     4000
    user        haproxy
    group       haproxy
    daemon
    stats socket /var/lib/haproxy/stats

defaults
    mode                    http
    log                     global
    option                  httplog
    option                  dontlognull
    option http-server-close
    option forwardfor       except 127.0.0.0/8
    option                  redispatch
    retries                 3
    timeout http-request    10s
    timeout queue           1m
    timeout connect         10s
    timeout client          1m
    timeout server          1m
    timeout http-keep-alive 10s
    timeout check           10s
    maxconn                 3000

listen stats                 #这里定义的是haproxy监控
    mode http                 #模式http
    bind 0.0.0.0:1080         #绑定的监控ip与端口
    stats enable              #启用监控
    stats hide-version        #隐藏haproxy版本
    stats uri     /web_status #定义的uri
    stats realm   Haproxy\ Statistics #定义显示文字
    stats auth    admin:admin #认证

frontend http
    bind *:80
    mode http
    log global
    option logasap
    option dontlognull
    capture request header Host len 20
    capture request header Referer len 20
    default_backend web

backend web
    balance source
    server web1 192.168.1.205:80 check maxconn 2000
    server web2 192.168.1.206:80 check maxconn 2000














