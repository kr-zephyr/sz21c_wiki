#### 개요
WAS 기동 시 JDBC에서 time zone 관련 exception을 출력하는 경우가 있다.  
exception은 아래와 같이 출력된다.

```
Loading class `com.mysql.jdbc.Driver'. This is deprecated. The new driver class is `com.mysql.cj.jdbc.Driver'. The driver is automatically registered via the SPI and manual loading of the driver class is generally unnecessary.
19-Feb-2020 13:40:23.183 심각 [RMI TCP Connection(2)-127.0.0.1] org.apache.tomcat.jdbc.pool.ConnectionPool.init Unable to create initial connections of pool.
	java.sql.SQLException: The server time zone value 'KST' is unrecognized or represents more than one time zone. You must configure either the server or JDBC driver (via the 'serverTimezone' configuration property) to use a more specifc time zone value if you want to utilize time zone support.
```

#### 원인
이는 시스템(OS)의 Time Zone과 MySql에 등록된 Time Zone의 차이에서 발생하는 문제로 OS(여기서는 OSX)의 타임존을 출력하면 아래와 같다.

```
% date
2020년 2월 19일 수요일 13시 41분 17초 KST
```

MySql의 Time Zone은 아래와 같다.

```
mysql> SELECT @@global.time_zone, @@session.time_zone;
+--------------------+---------------------+
| @@global.time_zone | @@session.time_zone |
+--------------------+---------------------+
| SYSTEM             | SYSTEM              |
+--------------------+---------------------+
1 row in set (0.00 sec)
```

#### 해결 방안
아래와 같이 MySql의 설정파일(my.cnf)에서 `default-time-zone`을 설정해 주면 된다.

```
[mysqld]
default-time-zone = Asia/Seoul
```

보통 설정파일(my.cnf)은 `/etc/my.cnf`이지만 /etc에 my.cnf가 없는 경우 새로 생성해 주면 된다.

위와 같이 설정을 바꾸고 MySql을 재실행하면 문제가 해결된다.

```
mysql> SELECT @@global.time_zone, @@session.time_zone;
+--------------------+---------------------+
| @@global.time_zone | @@session.time_zone |
+--------------------+---------------------+
| Asia/Seoul         | Asia/Seoul          |
+--------------------+---------------------+
1 row in set (0.00 sec)
```