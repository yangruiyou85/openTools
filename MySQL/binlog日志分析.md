
**二进制日志分析

#基于row格式


mysqlbinlog -vv --base64-output=DECODE-ROWS  logfile   > 0317.sql


mysqlbinlog --base64-output=DECODE-ROWS  --verbose --verbose   --start-datetime='2016-12-19 14:40'   --stop-datetime='2016-12-19 14:50 '  logfile   > 0317.sql



mysqlbinlog --base64-output=DECODE-ROWS  --verbose --verbose   --start-datetime='2017-05-04 22:00:03'   --stop-datetime='2017-05-04 22:10:03 '  mysql_m2-bin.000559 > 559.sql


mysqlbinlog --base64-output=DECODE-ROWS  --verbose --verbose   --start-datetime='2017-01-19 09:00:01'   --stop-datetime='2017-01-19 10:00:01 '  mysql_m2-bin.000482 > 482.sql





#慢查询日志分析
