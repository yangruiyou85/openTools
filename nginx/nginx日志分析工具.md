
#goaccess安装
用于分析IIS,Apache,nginx日志
yum install -y  GeoIP.x86_64  GeoIP-devel.x86_64  glib2 glib2-devel ncurses-devel
tar xvf goaccess-0.9.tar.gz
cd goaccess-0.9
./configure --enable-geoip --enable-utf8
make && make install

#范例
[root@mysql0 softs]# goaccess -f 20150512-000001.www.test.access.log -a


