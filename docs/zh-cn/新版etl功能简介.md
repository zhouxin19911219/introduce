

# Quartz

### 灵魂

```wiki
当web-server启动时,会查询etl_task_def表flag=1的数据根据cron加入到quartz中

etl_task_def表flag=1表示的是周期性上一次在执行的job
```

# 组件

## 组件介绍

目前支持的组件有以下几种，后续会继续增加

### Datax

#### 操作步骤

```wiki
1.填写参数A
2.填写参数B
3.保存
```

#### 处理逻辑

```wiki
1. 本地生成json文件
2. 上传json到远程主机
3. nohup pyhon  json>log
4. check log 成功
```

#### 关键参数比对

|              步骤               |          参数          |
| :-----------------------------: | :--------------------: |
|           原始json串            |       DATAX_JSON       |
|                                 |     DATAX_CHANNEL      |
|        本地生成json文件         |    DATAX_FILE_PATH     |
|       上传json到远程主机        | DATAX_FILE_REMOTE_PATH |
|                                 |       DATAX_HOST       |
|                                 |       DATAX_PORT       |
|                                 |     DATAX_USERNAME     |
|                                 |     DATAX_PASSWORD     |
| nohup python "datax"   json>log |   DATAX_PYTHON_PATH    |
|           tail -n 20            |     ASYN_LOG_PATH      |

<img src="https://tva1.sinaimg.cn/large/0082zybply1gbvoz0mcncj31620u0n1d.jpg" alt="image-20200214095237283" style="zoom:50%;" />

#### 矩阵

| 类型               | 数据源                          | Reader(读) | Writer(写) | 文档                                                         | 本系统支持 |
| ------------------ | ------------------------------- | ---------- | ---------- | ------------------------------------------------------------ | ---------- |
| RDBMS 关系型数据库 | MySQL                           | √          | √          | [读](https://github.com/alibaba/DataX/blob/master/mysqlreader/doc/mysqlreader.md) 、[写](https://github.com/alibaba/DataX/blob/master/mysqlwriter/doc/mysqlwriter.md) | 支持       |
|                    | Oracle                          | √          | √          | [读](https://github.com/alibaba/DataX/blob/master/oraclereader/doc/oraclereader.md) 、[写](https://github.com/alibaba/DataX/blob/master/oraclewriter/doc/oraclewriter.md) | 支持       |
|                    | SQLServer                       | √          | √          | [读](https://github.com/alibaba/DataX/blob/master/sqlserverreader/doc/sqlserverreader.md) 、[写](https://github.com/alibaba/DataX/blob/master/sqlserverwriter/doc/sqlserverwriter.md) |            |
|                    | PostgreSQL                      | √          | √          | [读](https://github.com/alibaba/DataX/blob/master/postgresqlreader/doc/postgresqlreader.md) 、[写](https://github.com/alibaba/DataX/blob/master/postgresqlwriter/doc/postgresqlwriter.md) | 支持       |
|                    | DRDS                            | √          | √          | [读](https://github.com/alibaba/DataX/blob/master/drdsreader/doc/drdsreader.md) 、[写](https://github.com/alibaba/DataX/blob/master/drdswriter/doc/drdswriter.md) |            |
|                    | 通用RDBMS(支持所有关系型数据库) | √          | √          | [读](https://github.com/alibaba/DataX/blob/master/rdbmsreader/doc/rdbmsreader.md) 、[写](https://github.com/alibaba/DataX/blob/master/rdbmswriter/doc/rdbmswriter.md) |            |
| 阿里云数仓数据存储 | ODPS                            | √          | √          | [读](https://github.com/alibaba/DataX/blob/master/odpsreader/doc/odpsreader.md) 、[写](https://github.com/alibaba/DataX/blob/master/odpswriter/doc/odpswriter.md) |            |
|                    | ADS                             |            | √          | [写](https://github.com/alibaba/DataX/blob/master/adswriter/doc/adswriter.md) |            |
|                    | OSS                             | √          | √          | [读](https://github.com/alibaba/DataX/blob/master/ossreader/doc/ossreader.md) 、[写](https://github.com/alibaba/DataX/blob/master/osswriter/doc/osswriter.md) |            |
|                    | OCS                             | √          | √          | [读](https://github.com/alibaba/DataX/blob/master/ocsreader/doc/ocsreader.md) 、[写](https://github.com/alibaba/DataX/blob/master/ocswriter/doc/ocswriter.md) |            |
| NoSQL数据存储      | OTS                             | √          | √          | [读](https://github.com/alibaba/DataX/blob/master/otsreader/doc/otsreader.md) 、[写](https://github.com/alibaba/DataX/blob/master/otswriter/doc/otswriter.md) |            |
|                    | Hbase0.94                       | √          | √          | [读](https://github.com/alibaba/DataX/blob/master/hbase094xreader/doc/hbase094xreader.md) 、[写](https://github.com/alibaba/DataX/blob/master/hbase094xwriter/doc/hbase094xwriter.md) |            |
|                    | Hbase1.1                        | √          | √          | [读](https://github.com/alibaba/DataX/blob/master/hbase11xreader/doc/hbase11xreader.md) 、[写](https://github.com/alibaba/DataX/blob/master/hbase11xwriter/doc/hbase11xwriter.md) |            |
|                    | Phoenix4.x                      | √          | √          | [读](https://github.com/alibaba/DataX/blob/master/hbase11xsqlreader/doc/hbase11xsqlreader.md) 、[写](https://github.com/alibaba/DataX/blob/master/hbase11xsqlwriter/doc/hbase11xsqlwriter.md) |            |
|                    | Phoenix5.x                      | √          | √          | [读](https://github.com/alibaba/DataX/blob/master/hbase20xsqlreader/doc/hbase20xsqlreader.md) 、[写](https://github.com/alibaba/DataX/blob/master/hbase20xsqlwriter/doc/hbase20xsqlwriter.md) |            |
|                    | MongoDB                         | √          | √          | [读](https://github.com/alibaba/DataX/blob/master/mongoreader/doc/mongoreader.md) 、[写](https://github.com/alibaba/DataX/blob/master/mongowriter/doc/mongowriter.md) |            |
|                    | Hive                            | √          | √          | [读](https://github.com/alibaba/DataX/blob/master/hdfsreader/doc/hdfsreader.md) 、[写](https://github.com/alibaba/DataX/blob/master/hdfswriter/doc/hdfswriter.md) |            |
|                    | Cassandra                       | √          | √          | [读](https://github.com/alibaba/DataX/blob/master/cassandrareader/doc/cassandrareader.md) 、[写](https://github.com/alibaba/DataX/blob/master/cassandrawriter/doc/cassandrawriter.md) |            |
| 无结构化数据存储   | TxtFile                         | √          | √          | [读](https://github.com/alibaba/DataX/blob/master/txtfilereader/doc/txtfilereader.md) 、[写](https://github.com/alibaba/DataX/blob/master/txtfilewriter/doc/txtfilewriter.md) | 支持       |
|                    | FTP                             | √          | √          | [读](https://github.com/alibaba/DataX/blob/master/ftpreader/doc/ftpreader.md) 、[写](https://github.com/alibaba/DataX/blob/master/ftpwriter/doc/ftpwriter.md) | 支持       |
|                    | HDFS                            | √          | √          | [读](https://github.com/alibaba/DataX/blob/master/hdfsreader/doc/hdfsreader.md) 、[写](https://github.com/alibaba/DataX/blob/master/hdfswriter/doc/hdfswriter.md) |            |
|                    | Elasticsearch                   |            | √          | [写](https://github.com/alibaba/DataX/blob/master/elasticsearchwriter/doc/elasticsearchwriter.md) |            |
| 时间序列数据库     | OpenTSDB                        | √          |            | [读](https://github.com/alibaba/DataX/blob/master/opentsdbreader/doc/opentsdbreader.md) |            |
|                    | TSDB                            | √          | √          | [读](https://github.com/alibaba/DataX/blob/master/tsdbreader/doc/tsdbreader.md) 、[写](https://github.com/alibaba/DataX/blob/master/tsdbwriter/doc/tsdbhttpwriter.md) |            |

#### 数据库表

- etl_datax_config

| 字段        | 类型          | 允许空 | 默认 | 注释           |
| :---------- | :------------ | :----- | ---- | -------------- |
| CONFIG_ID   | bigint(20)    | NO     | NULL | 无             |
| PLUGIN_ID   | bigint(20)    | YES    | NULL | 无             |
| CONFIG_NAME | varchar(50)   | YES    | NULL | 无             |
| CONFIG_JSON | varchar(5000) | YES    | NULL | datax 插件模板 |

```sql
/*
 Navicat Premium Data Transfer

 Source Server         : 192.168.100.53
 Source Server Type    : MySQL
 Source Server Version : 50634
 Source Host           : 192.168.100.53:3306
 Source Schema         : dvpdpdb01

 Target Server Type    : MySQL
 Target Server Version : 50634
 File Encoding         : 65001

 Date: 12/02/2020 13:45:59
*/

SET NAMES utf8mb4;
SET FOREIGN_KEY_CHECKS = 0;

-- ----------------------------
-- Table structure for etl_datax_config
-- ----------------------------
DROP TABLE IF EXISTS `etl_datax_config`;
CREATE TABLE `etl_datax_config` (
  `CONFIG_ID` bigint(20) NOT NULL AUTO_INCREMENT,
  `PLUGIN_ID` bigint(20) DEFAULT NULL,
  `CONFIG_NAME` varchar(50) DEFAULT NULL,
  `CONFIG_JSON` varchar(5000) DEFAULT NULL COMMENT 'datax 插件模板',
  PRIMARY KEY (`CONFIG_ID`)
) ENGINE=InnoDB AUTO_INCREMENT=1000006 DEFAULT CHARSET=utf8 COMMENT='datax插件模板';

-- ----------------------------
-- Records of etl_datax_config
-- ----------------------------
BEGIN;
INSERT INTO `etl_datax_config` VALUES (1, 1006, 'FTP-READER', '{\"name\": \"ftp2reader\", \"parameter\": {\"protocol\": \"${reader_protocol}\", \"host\": \"${reader_host}\", \"port\": \"${reader_port}\", \"username\": \"${reader_username}\", \"password\": \"${reader_password}\",\"isdel\": \"${reader_isdel}\", \"path\": [\"${reader_path}\"], \"column\":${reader_column}, \"encoding\": \"${reader_encoding}\",\"compress\":${reader_compress},\"skipHeader\":\"${reader_skipHeader}\", \"fieldDelimiter\": \"${reader_fieldDelimiter}\"} }');
INSERT INTO `etl_datax_config` VALUES (2, 1007, 'MYSQL-READER', '{\"name\": \"mysqlreader\", \"parameter\": {\"username\": \"${reader_username}\", \"password\": \"${reader_password}\",\"splitPk\": \"${reader_splitPk}\", \"connection\": [{\"querySql\": [\"${reader_querySql}\"], \"jdbcUrl\": [\"${reader_jdbcUrl}\"] } ] } }');
INSERT INTO `etl_datax_config` VALUES (3, 1008, 'GP-READER', '{\"name\": \"postgresqlreader\", \"parameter\": {\"username\": \"${reader_username}\", \"password\": \"${reader_password}\",\"splitPk\": \"${reader_splitPk}\", \"connection\": [{\"querySql\": [\"${reader_querySql}\"], \"jdbcUrl\": [\"${reader_jdbcUrl}\"] } ] } }');
INSERT INTO `etl_datax_config` VALUES (4, 1009, 'FTP-WRITER', '{\"name\": \"ftpwriter\", \"parameter\": {\"protocol\": \"${writer_protocol}\", \"host\": \"${writer_host}\", \"port\": \"${writer_port}\", \"username\": \"${writer_username}\", \"password\": \"${writer_password}\", \"timeout\": \"60000\", \"connectPattern\": \"PASV\", \"path\": \"${writer_path}\", \"fileName\": \"${writer_fileName}\", \"writeMode\": \"append\", \"fieldDelimiter\": \"${writer_fieldDelimiter}\", \"encoding\": \"${writer_encoding}\", \"nullFormat\": \"null\", \"dateFormat\": \"yyyy-MM-dd\", \"fileFormat\": \"csv\", \"header\": [] } }');
INSERT INTO `etl_datax_config` VALUES (5, 1010, 'MYSQL-WRITER', '{    \"name\": \"mysqlwriter\",    \"parameter\": {        \"writeMode\": \"insert\",\"batchsize\": \"2048\",\"username\": \"${writer_username}\",        \"password\": \"${writer_password}\",        \"column\": ${writer_column},        \"session\": [            \"set session sql_mode=\'ANSI\'\"        ],        \"preSql\": [            \"${writer_preSql}\"] ,        \"postSql\": [            \"${writer_postSql}\"       ],        \"connection\": [            {                \"jdbcUrl\": \"${writer_jdbcUrl}\",                \"table\": [                    \"${writer_table}\"                ]            }        ]    }}');
INSERT INTO `etl_datax_config` VALUES (6, 1011, 'GP-WRITER', '{    \"name\": \"postgresqlwriter\",    \"parameter\": {        \"username\": \"${writer_username}\",        \"password\": \"${writer_password}\",    \"batchsize\": \"2048\",    \"column\": ${writer_column},        \"connection\": [            {                \"table\": [                    \"${writer_table}\"                ],                \"jdbcUrl\":                     \"${writer_jdbcUrl}\"                            }        ]    }}');
INSERT INTO `etl_datax_config` VALUES (1000003, 1012, 'TXT-READER', ' {\r\n                    \"name\": \"txtfilereader\",\r\n                    \"parameter\": {\r\n                        \"path\": [\"${reader_path}\"],\r\n                        \"encoding\": \"${reader_encoding}\",\r\n												\"skipHeader\": \"${reader_skipHeader}\",\r\n												\"compress\": ${reader_compress},\r\n                        \"column\": ${reader_column},\r\n                        \"fieldDelimiter\": \"${reader_fieldDelimiter}\"\r\n                    }\r\n                }');
INSERT INTO `etl_datax_config` VALUES (1000004, 1013, 'TXT-WRITER', ' {\r\n                    \"name\": \"txtfile2writer\",\r\n                    \"parameter\": {\r\n                        \"path\": \"${writer_path}\",\r\n                        \"fileName\": \"${writer_fileName}\",\r\n                        \"writeMode\": \"truncate\",\r\n												\"fieldDelimiter\": \"${writer_fieldDelimiter}\",\r\n												\"compress\": ${writer_compress},\r\n												\"encoding\": \"${writer_encoding}\",\r\n												\"fileFormat\": \"${writer_fileFormat}\",														\r\n                        \"dateFormat\": \"yyyy-MM-dd\"\r\n                    }\r\n                }');
INSERT INTO `etl_datax_config` VALUES (1000005, 1016, 'ORACLE-READER', '{\"name\": \"oraclereader\", \"parameter\": {\"username\": \"${reader_username}\", \"password\": \"${reader_password}\",\"schema\":\"summer\",\"splitPk\": \"${reader_splitPk}\", \"connection\": [{\"querySql\": [\"${reader_querySql}\"], \"jdbcUrl\": [\"${reader_jdbcUrl}\"] } ] } }');
COMMIT;

SET FOREIGN_KEY_CHECKS = 1;


```

### 初始化数据

```SQL
INSERT INTO `config_property` VALUES (7, 'DP', 'DATAX_CHANNEL', '10', 'datax数据线程数', '1', NULL, NULL, NULL);
INSERT INTO `config_property` VALUES (31, 'DP', 'DATAX_FILE_PATH', '/home/datax/', 'DATAX生成json文件本地路径', '1', NULL, NULL, NULL);
INSERT INTO `config_property` VALUES (32, 'DP', 'DATAX_FILE_REMOTE_PATH', '/home/gpadmin/datax/json/', '（改）DATAX生成json文件远程主机路径', '1', NULL, NULL, NULL);
INSERT INTO `config_property` VALUES (14, 'DP', 'DATAX_HOST', '192.168.100.51', '（改）DATAX PYTHON执行文件的主机IP', '1', NULL, NULL, NULL);
INSERT INTO `config_property` VALUES (2, 'DP', 'DATAX_JSON', '{\"job\": {\"setting\": {\"speed\": {\"channel\": \"${channel}\" } }, \"content\": [{\"reader\": \"${reader}\", \"writer\": \"${writer}\" } ] } }', 'datax json模板', '1', NULL, NULL, NULL);
INSERT INTO `config_property` VALUES (13, 'DP', 'DATAX_PASSWORD', 'ZicaiGp@1', '（改）DATAX PYTHON执行文件主机用户名的密码', '1', NULL, NULL, NULL);
INSERT INTO `config_property` VALUES (11, 'DP', 'DATAX_PORT', '22', 'DATAX PYTHON执行文件', '1', NULL, NULL, NULL);
INSERT INTO `config_property` VALUES (8, 'DP', 'DATAX_PYTHON_PATH', '/home/gpadmin/datax/bin/datax.py', '（改）DATAX PYTHON的datax.py执行文件的路径', '1', NULL, NULL, NULL);
INSERT INTO `config_property` VALUES (12, 'DP', 'DATAX_USERNAME', 'gpadmin', '（改）DATAX PYTHON执行文件的主机名', '1', NULL, NULL, NULL);

```

### 注意事项

从**etl_data_source**表加载的配置一定要确保协议能够匹配上

从**etl_data_source**表加载的配置一定要确保协议能够匹配上

从**etl_data_source**表加载的配置一定要确保协议能够匹配上

#### 错误案例

​        配置ftp到txt的数据迁移,21端口匹配的是ftp协议，22端口匹配的是sftp协议

### gpload

#### 操作步骤

```wiki
1.选择要去执行gpload的主机
2.填写脚本参数
3.保存
```

#### 处理逻辑

```wiki
1. 本地生成yml文件
2. 上传yml到远程主机
3. nohup gpload -f yml>log
4. check log 成功
```

#### 关键参数比对

|          步骤           |          参数           |
| :---------------------: | :---------------------: |
|     本地生成yml文件     |    GPLOAD_FILE_PATH     |
|    上传yml到远程主机    | GPLOAD_FILE_REMOTE_PATH |
|                         |    GPLOAD_FILE_HOST     |
|                         |  GPLOAD_FILE_PASSWORD   |
|                         |    GPLOAD_FILE_PORT     |
|                         |  GPLOAD_FILE_USERNAME   |
| nohup gpload -f yml>log |      ASYN_LOG_PATH      |
|       tail -n 20        |                         |



<img src="https://tva1.sinaimg.cn/large/0082zybply1gburbcqcsvj316q0u0n19.jpg" alt="image-20200213142811865" style="zoom:50%;" />

###  注意事项

 因为gpload是对gpfdist的封装，因此使用gpload之前必须开启gpfdist的服务，不然无法使用。

```
gpfdist -d /home/admin -p 8181 -l /tmp/gpfdist.log &
```

####   官方文档

 http://gpdb.docs.pivotal.io/530/utility_guide/admin_utilities/gpload.html  

https://www.cnblogs.com/daojiao/p/4595597.html

配置属性在官方文档存在

#### 环境变量

```shell
# .bashrc

# Source global definitions
if [ -f /etc/bashrc ]; then
        . /etc/bashrc
fi

# User specific aliases and functions
source  /usr/local/greenplum-db/greenplum_path.sh
#export ORACLE_HOME=/usr/local/oracle/instantclient_11_2
#export TNS_ADMIN=$ORACLE_HOME/network/admin
#export NLS_LANG=AMERICAN_AMERICA.ZHS16GBK
#export NLS_LANG=AMERICAN_AMERICA.AL32UTF8
#export LD_LIBRARY_PATH=$ORACLE_HOME
#export PATH=$ORACLE_HOME:$PATH
#export ORACLE_SID=export
```

```shell
source ~/.bashrc 
```

#### 初始化数据

```sql
INSERT INTO `config_property` VALUES (21, 'DP', 'GPLOAD_FILE_HOST', '192.168.100.51', '（改）gpload文件主机的IP', '1', NULL, NULL, NULL);
INSERT INTO `config_property` VALUES (20, 'DP', 'GPLOAD_FILE_PASSWORD', 'ZicaiGp@1', '（改）GPLOAD文件主机用户名的密码', '1', NULL, NULL, NULL);
INSERT INTO `config_property` VALUES (22, 'DP', 'GPLOAD_FILE_PATH', '/home/yml/', 'GPLOAD的生成文件的本地路径', '1', NULL, NULL, NULL);
INSERT INTO `config_property` VALUES (18, 'DP', 'GPLOAD_FILE_PORT', '22', 'GPLOAD文件端口', '1', NULL, NULL, NULL);
INSERT INTO `config_property` VALUES (23, 'DP', 'GPLOAD_FILE_REMOTE_PATH', '/home/gpadmin/yml/', '（改）GPLOAD文件远程存放路径，要放置YML文件的路径', '1', NULL, NULL, NULL);
INSERT INTO `config_property` VALUES (19, 'DP', 'GPLOAD_FILE_USERNAME', 'gpadmin', '（改）GPLOAD文件用户名的密码', '1', NULL, NULL, NULL);

```

### shell

#### 操作步骤

```tex
1.选择要去执行该条shell的主机

2.填写脚本内容

3.填写脚本参数

4.保存
```

<img src="https://tva1.sinaimg.cn/large/0082zybply1gbuqt7k0ckj31d80tan0m.jpg" alt="image-20200213141038392" style="zoom:50%;" />

#### 处理逻辑

```wiki
1. 本地生成sh/python文件
2. 上传文件到远程主机
3. nohup sh/python file >log
4. check log 成功
```

#### 关键参数比对

|            步骤            |          参数          |
| :------------------------: | :--------------------: |
|      本地生成yml文件       |    SHELL_FILE_PATH     |
|     上传文件到远程主机     | SHELL_FILE_REMOTE_PATH |
| nohup sh/python   file>log |                        |
|         tail -n 20         |     ASYN_LOG_PATH      |

#### 注意事项

要拼接成功失败返回值，自己判断异常等

#### 错误案例

```tiki wiki
不按照shell标准格式填写
不按照python标准格式填写
```

### sql

<img src="https://tva1.sinaimg.cn/large/0082zybply1gbur4t7ixdj31a60qwwhe.jpg" alt="image-20200213142141064" style="zoom:50%;" />

#### 操作步骤

```wiki
1.选择要去执行该条sql的数据库
2.填写sql内容(变量直接在sql内)
3.保存
```

#### 注意事项

##### SQL语句分类

1. DDL(Data Definition Language): 数据定义语言
   - 用来定义数据库对象:数据库，表,列等。 关键字：create,drop, alter等。
2. DML(Data Manipulation Language): 数据操作语言
   - 用来对数据库中的表进行增删改操作。 关键字：insert,delete,update等。
3. ~~DQL(Data Query Language): 数据查询语言~~
   - 用来查询数据库中表的记录(数据)。 关键字:select, where等
4. DCL(Data Control Language): 数据控制语言
   - 用来定义数据库的访问控制权限和安全级别，及创建用户。关键字: grant, revoke等

#### 错误案例

```wiki
没有按照标准格式填写sql
```

### 补数

#### 操作步骤

```wiki
1.有补数选项
2.选择时间区间或者一天
3.保存
```

<img src="https://tva1.sinaimg.cn/large/0082zybply1gbvoom1qtqj30re0n40uz.jpg" alt="image-20200214094238452" style="zoom:50%;" />

#### 注意事项

补数任务只能执行一次,不能是周期任务

### 存储过程

#### 操作步骤

```wiki
1.选择要去执行该存储过程的主机
2.填写存储过程名称
3.填写参数
4.保存
```



<img src="https://tva1.sinaimg.cn/large/0082zybply1gbus0btmzkj31b60p2gp2.jpg" alt="image-20200213145208545" style="zoom:50%;" />

处理逻辑

```wiki
1. 本地生成存储过程文件
2. 上传文件到远程主机
3. 执行存储过程(不同数据库不同样式)
4. check log 成功
```

|                   步骤                   |         参数          |
| :--------------------------------------: | :-------------------: |
|               本地生成文件               |    FUNC_FILE_PATH     |
|            上传文件到远程主机            |    FUNC_FILE_HOST     |
|                                          |    FUNC_FILE_PORT     |
|                                          |  FUNC_FILE_USERNAME   |
|                                          |  FUNC_FILE_PASSWORD   |
|                                          | FUNC_FILE_REMOTE_PATH |
| 执行存储过程nohup psql/nohup echo 'quit' |        sqlplus        |
|              check log 成功              |     ASYN_LOG_PATH     |

#### 环境变量

```shell
# .bashrc

# Source global definitions
if [ -f /etc/bashrc ]; then
        . /etc/bashrc
fi

# User specific aliases and functions
这里需要填写一下
```

```shell
source ~/.bashrc 
```

#### 初始化数据

```sql
INSERT INTO `config_property` VALUES (30, 'DP', 'FUNC_FILE_PATH', '/home/devapp/func/', '存储过程生产路径（配ETL主机路径）', '1', NULL, NULL, NULL);
INSERT INTO `config_property` VALUES (80, 'DP', 'FUNC_FILE_REMOTE_PATH', '/data/', '（改）存储过程远程路径（配GP主机路径）', '1', NULL, NULL, NULL);
INSERT INTO `config_property` VALUES (400, 'DP', 'FUNC_FILE_HOST', '192.168.100.51', 'func执行的主机', '1', NULL, NULL, NULL);
INSERT INTO `config_property` VALUES (401, 'DP', 'FUNC_FILE_PORT', '22', 'func执行的主机的端口号', '1', NULL, NULL, NULL);
INSERT INTO `config_property` VALUES (402, 'DP', 'FUNC_FILE_USERNAME', 'gpadmin', '用户名1', '1', NULL, NULL, NULL);
INSERT INTO `config_property` VALUES (403, 'DP', 'FUNC_FILE_PASSWORD', 'ZicaiGp@1', '密码', '1', NULL, NULL, NULL);
```

### 子任务

#### 操作步骤

```wiki
1.选择作为子任务的模板
2.保存
```



<img src="https://tva1.sinaimg.cn/large/0082zybply1gbutlikm74j31do0m2q63.jpg" alt="image-20200213154703743" style="zoom:50%;" />



```java
是不是有接口，诗语填写一下
```

### 节点检查

#### 输入sql作为检查点

#### 操作步骤

```wiki
1.选择人工或者自动
2.选择数据库数据源
3.填写sql语句能返回结果的
4.期望结果及关系
5.设置检查时间
6.保存
```

<img src="https://tva1.sinaimg.cn/large/0082zybply1gbuu6h07gyj315r0u078t.jpg" alt="image-20200213160716483" style="zoom:50%;" />



#### 注意事项

如果超过检查时间，就说明程序返回值和期望值不一致,需要人工参与

### 文件检查

未来会同shell合并

#### 操作步骤

```tex
1.选择要去执行该条shell的主机

2.填写脚本内容

3.填写脚本参数

4.保存
```

<img src="https://tva1.sinaimg.cn/large/0082zybply1gbvq0umc9jj317a0u0ae5.jpg" alt="image-20200214102901067" style="zoom:50%;" />

#### 处理逻辑

```wiki
1. 远程执行固定脚本
2. 执行结果入log
3. check log 成功
```

#### 关键参数比对

|      步骤       |         参数          |
| :-------------: | :-------------------: |
| 本地生成yml文件 |    CHECK_FILE_PATH    |
|   检查的频率    | CHECK_FILE_SLEEP_TIME |
| 远程执行的参数  |    CHECK_FILE_HOST    |
|                 |    CHECK_FILE_PORT    |
|                 |  CHECK_FILE_USERNAME  |
|                 |  CHECK_FILE_PASSWORD  |
|   tail -n 20    |     ASYN_LOG_PATH     |

#### 初始化数据

```sql
INSERT INTO `config_property` VALUES (28, 'DP', 'CHECK_FILE_HOST', '192.168.100.51', '（改）文件校验的python存放主机IP', '1', NULL, NULL, NULL);
INSERT INTO `config_property` VALUES (25, 'DP', 'CHECK_FILE_PASSWORD', 'ZicaiGp@1', '（改）文件校验的python存放密码', '1', NULL, NULL, NULL);
INSERT INTO `config_property` VALUES (24, 'DP', 'CHECK_FILE_PATH', '/home/gpadmin/filecheck/file_check_hb.py', '（改）文件校验的pythonpy文件存放路径，各省的Python文件名不一样', '1', NULL, NULL, '2019-05-30 09:51:26');
INSERT INTO `config_property` VALUES (26, 'DP', 'CHECK_FILE_PORT', '22', '文件校验的python存放端口号', '1', NULL, NULL, NULL);
INSERT INTO `config_property` VALUES (27, 'DP', 'CHECK_FILE_SLEEP_TIME', '3', '文件校验时间设置', '1', NULL, NULL, '2019-04-10 10:44:10');
INSERT INTO `config_property` VALUES (29, 'DP', 'CHECK_FILE_USERNAME', 'gpadmin', '（改）文件校验的python存放主机用户名', '1', NULL, NULL, NULL);

```

#### 注意事项

建议不要选择远程，用户名和密码是远程脚本主机所在

# 模板

## 常用操作

### 创建

参见组件介绍

### 查询

根据条件查询模板信息，比如谁创建的，在什么时间创建的，目前有哪些启动状态

```java
public interface IEtlTaskDefSV {
    /**
     * 分页按照条件查询数据 按照配置时间和配置人员
     * 
     * @param request
     * @return
     */
    @POST
    @Path("/queryTaskDefByCondition")
    public PageInfoResponse<EtlTaskDefVo> queryTaskDefByCondition(String json);
    }
```

### 修改

修改执行周期

```java
 public class QuartzScheduler {
   public boolean modifyJob(String name, String group, String time) throws SchedulerException{}
 }
```

修改模板内容

```java
 public interface IEtlTaskDefSV {
 /**
     * 这个方法用来实现 修改(删除) 保存
     * 
     * @param vo
     * @return
     */
    @POST
    @Path("/saveTaskDef")
    public BaseResponse saveTaskDef(EtlTaskDefVo vo);
    }
```

### 删除

```java
public interface IEtlTaskDefSV {
    @POST
    @Path("/deleteTaskDef")
    public BaseResponse deleteTaskDef(Long taskId);
  }
```

### 复制

```java
public interface IEtlTaskDefSV {
     /**
     * 复制
     * 
     * @param taskId
     * @return
     */
    @POST
    @Path("/copyTaskDef")
    public BaseResponse copyTaskDef(String json);
    }
```

### 启动

把定义模板加入到任务列表中

```java
public class QuartzScheduler {
  public void addJobInfo(String name, String group, String time) throws SchedulerException{}
}
```

### 停止

停止任务列表中的任务

1. 一次性任务自动停止
2. 周期性任务手工停止

```java
public class QuartzScheduler {
   public void deleteJob(String name, String group) throws SchedulerException{}
}
```

### 系统启动job

启动所有在执行的周期job

```java
public class QuartzScheduler {
   public void startJob() throws SchedulerException
}
```



### 执行一次(新增)

<img src="https://tva1.sinaimg.cn/large/0082zybply1gbvrz1enbrj30qu05qdga.jpg" alt="image-20200214113628015" style="zoom:50%;" />

## 数据库表

### **etl_task_def**

| 字段            | 类型          | 允许空 | 默认 | 注释                                     |
| :-------------- | :------------ | :----- | ---- | ---------------------------------------- |
| TASK_ID         | bigint(20)    | NO     | NULL | 主键                                     |
| TASK_NAME       | varchar(200)  | YES    | NULL | 创建模板名称                             |
| CREATE_TIME     | datetime      | YES    | NULL | 创建时间                                 |
| CREATE_USER     | varchar(50)   | YES    | NULL | 创建人                                   |
| REMARK          | varchar(1000) | YES    | NULL | 备注，清晰描述该模板是干啥的             |
| UPDATE_TIME     | datetime      | YES    | NULL | 更新时间                                 |
| UPDATE_USER     | varchar(50)   | YES    | NULL | 更新人                                   |
| TASK_JSON       | text          | YES    | NULL | 前台页面保存的json串                     |
| JOB_STATUS      | varchar(2)    | YES    | NULL | 模板的状态，是否执行中                   |
| CRON            | varchar(20)   | YES    | NULL | CRON                                     |
| FLAG            | char(255)     | YES    | NULL | cron启动之后的标记位，系统重启的时候用到 |
| COMPLEMENT      | varchar(255)  | YES    | NULL | 有值就按照这个值去处理                   |
| COMPLEMENT_FLAG | char(2)      | YES    | NULL | 前台用，标记位                          |
| ACTOMATION_FLAG | char(1)       | YES    | NULL | 任务是否自动执行                         |

```sql
/*
 Navicat Premium Data Transfer

 Source Server         : 192.168.100.53
 Source Server Type    : MySQL
 Source Server Version : 50634
 Source Host           : 192.168.100.53:3306
 Source Schema         : dvpdpdb01

 Target Server Type    : MySQL
 Target Server Version : 50634
 File Encoding         : 65001

 Date: 10/02/2020 14:33:02
*/

SET NAMES utf8mb4;
SET FOREIGN_KEY_CHECKS = 0;

-- ----------------------------
-- Table structure for etl_task_def
-- ----------------------------
DROP TABLE IF EXISTS `etl_task_def`;
CREATE TABLE `etl_task_def` (
  `TASK_ID` bigint(20) NOT NULL AUTO_INCREMENT COMMENT '主键',
  `TASK_NAME` varchar(200) DEFAULT NULL COMMENT '创建模板名称',
  `CREATE_TIME` datetime DEFAULT NULL COMMENT '创建时间',
  `CREATE_USER` varchar(50) DEFAULT NULL COMMENT '创建人',
  `REMARK` varchar(1000) DEFAULT NULL COMMENT '备注，清晰描述该模板是干啥的',
  `UPDATE_TIME` datetime DEFAULT NULL COMMENT '更新时间',
  `UPDATE_USER` varchar(50) DEFAULT NULL COMMENT '更新人',
  `TASK_JSON` text COMMENT '前台页面保存的json串',
  `JOB_STATUS` varchar(2) DEFAULT NULL COMMENT '模板的状态，是否执行中',
  `CRON` varchar(20) DEFAULT NULL COMMENT '周期表达式',
  `FLAG` char(255) DEFAULT NULL COMMENT 'cron启动之后的标记位，系统重启的时候用到',
  `COMPLEMENT` varchar(255) DEFAULT NULL COMMENT '如果有值就是补数任务',
  `COMPLEMENT_FLAG` char(2) DEFAULT NULL,
  `ACTOMATION_FLAG` char(1) DEFAULT NULL COMMENT '创建任务之后是否自动执行',
  PRIMARY KEY (`TASK_ID`)
) ENGINE=InnoDB AUTO_INCREMENT=1000202 DEFAULT CHARSET=utf8 COMMENT='这是一张模板表';

SET FOREIGN_KEY_CHECKS = 1;
```

## 注意事项

修改模板,周期性任务同时生效

# 任务

## 常用操作

### 启动(cron定时触发)  

```java
public interface IEtlTaskDefSV {    
    /**
     * 把生成数据这个统一化
     * 
     * @param taskId
     * @return
     */
    @POST
    @Path("/generateTaskById")
    public BaseResponse generateTaskById(String taskId);
}
```

- #### 自动

  当**etl_task_def**中ACTOMATION_FLAG中字段是1,自动启动任务程序

- #### 手动

  当**etl_task_def**中ACTOMATION_FLAG中字段非1,需要操作员在前台手动启动程序

  前台可以支持多选的模式

  ```java
    public interface IEtlTaskBatchDefSV {
      /**
       * 批量启动(也可以单个启动)
       * 
       * @param batchIds
       * @return
       */
      @POST
      @Path("/batchStartTask")
      public BaseResponse batchStartTask(String batchIds);
    }
  ```


### 修改参数

- 定时处理器读取到模板表有任务要执行的时候,会直接调用这个保存的方法

- 当前台任务做参数修改的时候,会直接调用这个保存的方法

  参数包括：流程节点中参数的变化,基准时间的更改,备注的更改等

```java
public interface IEtlTaskBatchDefSV {
    @POST
    @Path("/saveBatchDef")
    public String saveBatchDef(EtlTaskBatchDefVo vo);
 }
```

分两步

1.从**etl_task_def**表拷贝数据到**etl_task_batch_def**表,

   判断是保存还是修改，根据传递的参数EtlTaskBatchDefVo 是否有TaskBatchId

2.从**etl_task_batch_def**表根据数据生成**etl_task_detail**与**etl_work_def**

### 修改启动点

```java
public interface IEtlTaskDetailSV {
   /**
     * 通过BatchId 查询detail状态，这个状态内部带有每一条的结果 前台界面会是一个定时更新的查询
     * 
     * @param taskBatchId
     * @return
     */
    @POST
    @Path("/updateEtlTaskDetail")
    public BaseResponse updateEtlTaskDetail(EtlTaskDetailVo json);
}
```

### 查询

目前把查询条件封装到json里面，方便后续扩展

查询条件有：时间段/状态/任务名称等

```java
public interface IEtlTaskBatchDefSV {
     /**
     * 这是按照条件分页查询
     * 
     * @param json
     * @return
     */
    @POST
    @Path("/showBatchDefByCondition")
    public PageInfoResponse<EtlTaskBatchDefVo> showBatchDefByCondition(String json);
 }
```

### 删除

删除任务记录

```java
public interface IEtlTaskBatchDefSV { 
    @POST
    @Path("/deleteBatchDef")
    public BaseResponse deleteBatchDef(EtlTaskBatchDefVo vo);
    }
```

## 数据库表

### **etl_task_batch_def**

| 字段          | 类型          | 允许空 | 默认 | 注释                                  |
| :------------ | :------------ | :----- | ---- | ------------------------------------- |
| TASK_BATCH_ID | varchar(200)  | NO     | NULL | 批次号任务唯一标识                    |
| TASK_ID       | bigint(20)    | NO     | NULL | 任务ID:来自etl_task_def               |
| TASK_NAME     | varchar(200)  | YES    | NULL | 任务名称：etl_task_def+STANDARD_TIME  |
| STATUS        | char(1)       | YES    | NULL | 0删除/1待执行/2已执行/3完成/4执行失败 |
| CREATE_TIME   | datetime      | YES    | NULL | 创建时间                              |
| CREATE_USER   | varchar(50)   | YES    | NULL | 创建人来自etl_task_def                |
| REMARK        | varchar(1000) | YES    | NULL | 备注来自etl_task_def                  |
| UPDATE_TIME   | datetime      | YES    | NULL | 更新时间                              |
| UPDATE_USER   | varchar(50)   | YES    | NULL | 更新人                                |
| START_TIME    | datetime      | YES    | NULL | 开始时间                              |
| END_TIME      | datetime      | YES    | NULL | 结束时间                              |
| TASK_JSON     | text          | YES    | NULL |                                       |
| STANDARD_TIME | varchar(50)   | YES    | NULL | 执行基准时间                          |

```sql
/*
 Navicat Premium Data Transfer

 Source Server         : 192.168.100.53
 Source Server Type    : MySQL
 Source Server Version : 50634
 Source Host           : 192.168.100.53:3306
 Source Schema         : dvpdpdb01

 Target Server Type    : MySQL
 Target Server Version : 50634
 File Encoding         : 65001

 Date: 10/02/2020 11:07:51
*/

SET NAMES utf8mb4;
SET FOREIGN_KEY_CHECKS = 0;

-- ----------------------------
-- Table structure for etl_task_batch_def
-- ----------------------------
DROP TABLE IF EXISTS `etl_task_batch_def`;
CREATE TABLE `etl_task_batch_def` (
  `TASK_BATCH_ID` varchar(200) NOT NULL COMMENT '批次号任务唯一标识',
  `TASK_ID` bigint(20) NOT NULL COMMENT '任务ID:来自etl_task_def',
  `TASK_NAME` varchar(200) DEFAULT NULL COMMENT '任务名称：etl_task_def+STANDARD_TIME',
  `STATUS` char(1) DEFAULT NULL COMMENT '0删除/1待执行/2已执行/3完成/4执行失败',
  `CREATE_TIME` datetime DEFAULT NULL COMMENT '创建时间',
  `CREATE_USER` varchar(50) DEFAULT NULL COMMENT '创建人来自etl_task_def',
  `REMARK` text COMMENT '备注来自etl_task_def',
  `UPDATE_TIME` datetime DEFAULT NULL COMMENT '更新时间',
  `UPDATE_USER` varchar(50) DEFAULT NULL COMMENT '更新人',
  `START_TIME` datetime DEFAULT NULL COMMENT '开始时间',
  `END_TIME` datetime DEFAULT NULL COMMENT '结束时间',
  `TASK_JSON` text COMMENT '页面展示图形的json串',
  `STANDARD_TIME` varchar(50) DEFAULT NULL COMMENT '执行基准时间',
  PRIMARY KEY (`TASK_BATCH_ID`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='这是任务表,用来记录执行任务';

SET FOREIGN_KEY_CHECKS = 1;
```

## 注意事项

这张表数据的修改只会影响到本次执行的变更

# 参数配置(待完善)

## 常用操作

### 新增

### 修改

### 删除

### 查询

## 数据库表

### **etl_data_source**

| 字段            | 类型         | 允许空 | 默认 | 注释           |
| :-------------- | :----------- | :----- | ---- | -------------- |
| SOURCE_ID       | bigint(20)   | NO     | NULL | 无             |
| SOURCE_NAME     | varchar(200) | YES    | NULL | 资源名称       |
| SOURCE_TYPE     | varchar(10)  | YES    | NULL | FTP :GP :MYSQL |
| SOURCE_USERNAME | varchar(20)  | YES    | NULL | 用户名         |
| SOURCE_PASSWORD | varchar(20)  | YES    | NULL | 密码           |
| PATH            | varchar(500) | YES    | NULL | 路径           |
| PORT            | varchar(20)  | YES    | NULL | 无             |
| URL             | varchar(500) | YES    | NULL | jdbc           |
| HOST            | varchar(20)  | YES    | NULL | 无             |
| FTP_TYPE        | varchar(20)  | YES    | NULL | 无             |

```sql
/*
 Navicat Premium Data Transfer

 Source Server         : 192.168.100.53
 Source Server Type    : MySQL
 Source Server Version : 50634
 Source Host           : 192.168.100.53:3306
 Source Schema         : dvpdpdb01

 Target Server Type    : MySQL
 Target Server Version : 50634
 File Encoding         : 65001

 Date: 10/02/2020 17:23:02
*/

SET NAMES utf8mb4;
SET FOREIGN_KEY_CHECKS = 0;

-- ----------------------------
-- Table structure for etl_data_source
-- ----------------------------
DROP TABLE IF EXISTS `etl_data_source`;
CREATE TABLE `etl_data_source` (
  `SOURCE_ID` bigint(20) NOT NULL AUTO_INCREMENT,
  `SOURCE_NAME` varchar(200) DEFAULT NULL COMMENT '资源名称',
  `SOURCE_TYPE` varchar(10) DEFAULT NULL COMMENT 'FTP :GP :MYSQL',
  `SOURCE_USERNAME` varchar(20) DEFAULT NULL COMMENT '用户名',
  `SOURCE_PASSWORD` varchar(20) DEFAULT NULL COMMENT '密码',
  `PATH` varchar(500) DEFAULT NULL COMMENT '路径',
  `PORT` varchar(20) DEFAULT NULL,
  `URL` varchar(500) DEFAULT NULL COMMENT 'jdbc',
  `HOST` varchar(20) DEFAULT NULL,
  `FTP_TYPE` varchar(20) DEFAULT NULL,
  PRIMARY KEY (`SOURCE_ID`)
) ENGINE=InnoDB AUTO_INCREMENT=1000024 DEFAULT CHARSET=utf8 COMMENT='这里面配置参数';

SET FOREIGN_KEY_CHECKS = 1;
```

## 注意事项

### 处理逻辑

创建任务--->周期处理任务--->生成数据---->执行---->如果有查询状态就查询状态，如果没有就拉倒

# 业务图

### 流程图

```flow
st=>start: 开始
op=>operation: 模板表etl_task_def
op1=>operation: 任务表etl_task_batch_def
op2=>operation: 任务明细表etl_task_detail
op3=>operation: 任务执行工作表etl_work_def
e=>end: 结束框
st->op->op1->op2->op3->e
```

### 时序图

```sequence
Title: 任务线
定时->表etl_task_def: 根据cron获取待执行任务（请求）
表etl_task_def-->定时: 返回taskID(响应)
定时->表etl_task_batch_def: 根据taskID创建任务（请求）
Note right of 表etl_task_batch_def: 任务表
Note left of 定时: 定时器

表etl_task_batch_def->表etl_task_detail: 生成数据
表etl_task_detail->表elt_work_def: 生成真正执行数据
表etl_task_batch_def->表etl_task_detail: 根据cron执行状态为1的detail（请求）
表etl_task_detail->表elt_work_def: 工作（请求）
表elt_work_def->redis: 塞入查询值（请求）
表elt_work_def-->表etl_task_detail: 更新状态（响应）
Note over 表etl_task_detail,表elt_work_def: 工作者
定时->redis: 根据cron查询redis中的值,获取状态（请求）
redis-->>表etl_task_detail: 更新detail状态
```

# 节点模板

### **etl_node_def**

| 字段        | 类型          | 允许空 | 默认 | 注释 |
| :---------- | :------------ | :----- | ---- | ---- |
| NODE_ID     | bigint(20)    | NO     | NULL | 无   |
| NODE_NAME   | varchar(255)  | YES    | NULL | 无   |
| NODE_TYPE   | varchar(255)  | YES    | NULL | 无   |
| NODE_JSON   | varchar(5000) | YES    | NULL | 无   |
| CREATE_TIME | datetime      | YES    | NULL | 无   |
| CREATE_USER | varchar(255)  | YES    | NULL | 无   |

```sql
/*
 Navicat Premium Data Transfer

 Source Server         : 192.168.100.53
 Source Server Type    : MySQL
 Source Server Version : 50634
 Source Host           : 192.168.100.53:3306
 Source Schema         : dvpdpdb01

 Target Server Type    : MySQL
 Target Server Version : 50634
 File Encoding         : 65001

 Date: 10/02/2020 17:37:37
*/

SET NAMES utf8mb4;
SET FOREIGN_KEY_CHECKS = 0;

-- ----------------------------
-- Table structure for etl_node_def
-- ----------------------------
DROP TABLE IF EXISTS `etl_node_def`;
CREATE TABLE `etl_node_def` (
  `NODE_ID` bigint(20) NOT NULL AUTO_INCREMENT,
  `NODE_NAME` varchar(255) DEFAULT NULL,
  `NODE_TYPE` varchar(255) DEFAULT NULL,
  `NODE_JSON` varchar(5000) DEFAULT NULL,
  `CREATE_TIME` datetime DEFAULT NULL,
  `CREATE_USER` varchar(255) DEFAULT NULL,
  PRIMARY KEY (`NODE_ID`)
) ENGINE=InnoDB AUTO_INCREMENT=1000055 DEFAULT CHARSET=utf8 COMMENT='etl_node_def节点模板表';

SET FOREIGN_KEY_CHECKS = 1;

```

# 插件

### etl_plugin_def

| 字段        | 类型         | 允许空 | 默认 | 注释                                        |
| :---------- | :----------- | :----- | ---- | ------------------------------------------- |
| PLUGIN_ID   | bigint(20)   | NO     | NULL | 无                                          |
| PLUGIN_NAME | varchar(200) | YES    | NULL | 无                                          |
| PLUGIN_TYPE | varchar(10)  | YES    | NULL | SQL:FTP:SHELL:READER:WRITER:DATAX:PROCEDURE |
| STATUS      | char(1)      | YES    | NULL | 0失效1生效                                  |
| LOGO        | varchar(50)  | YES    | NULL | 无                                          |
| PARENT_ID   | bigint(20)   | YES    | NULL | 无                                          |
| SORT        | int(2)       | YES    | NULL | 无                                          |

```sql
/*
 Navicat Premium Data Transfer

 Source Server         : 192.168.100.53
 Source Server Type    : MySQL
 Source Server Version : 50634
 Source Host           : 192.168.100.53:3306
 Source Schema         : dvpdpdb01

 Target Server Type    : MySQL
 Target Server Version : 50634
 File Encoding         : 65001

 Date: 12/02/2020 13:58:54
*/

SET NAMES utf8mb4;
SET FOREIGN_KEY_CHECKS = 0;

-- ----------------------------
-- Table structure for etl_plugin_def
-- ----------------------------
DROP TABLE IF EXISTS `etl_plugin_def`;
CREATE TABLE `etl_plugin_def` (
  `PLUGIN_ID` bigint(20) NOT NULL AUTO_INCREMENT,
  `PLUGIN_NAME` varchar(200) DEFAULT NULL,
  `PLUGIN_TYPE` varchar(10) DEFAULT NULL COMMENT 'SQL:FTP:SHELL:READER:WRITER:DATAX:PROCEDURE',
  `STATUS` char(1) DEFAULT NULL COMMENT '0失效1生效',
  `LOGO` varchar(50) DEFAULT NULL,
  `PARENT_ID` bigint(20) DEFAULT NULL,
  `SORT` int(2) DEFAULT NULL,
  PRIMARY KEY (`PLUGIN_ID`)
) ENGINE=InnoDB AUTO_INCREMENT=1018 DEFAULT CHARSET=utf8 COMMENT='etl_plugin_def';

-- ----------------------------
-- Records of etl_plugin_def
-- ----------------------------
BEGIN;
INSERT INTO `etl_plugin_def` VALUES (1, '1', '2', '0', '4', 3, 5);
INSERT INTO `etl_plugin_def` VALUES (2, '1', '2', '0', '4', 3, 5);
INSERT INTO `etl_plugin_def` VALUES (3, '执行SHELL', 'SHELL', '0', 'SHELL-LOAD', 0, 6);
INSERT INTO `etl_plugin_def` VALUES (4, '执行SHELL', 'SHELL', '0', 'SHELL-LOAD', 0, 7);
INSERT INTO `etl_plugin_def` VALUES (5, '1', '2', '0', '4', 3, 5);
INSERT INTO `etl_plugin_def` VALUES (6, '节点检查', 'CHECK', '1', 'NODE-CHECK', 0, 8);
INSERT INTO `etl_plugin_def` VALUES (1001, 'SHELL执行', 'SHELL', '1', 'SHELL', 0, 1);
INSERT INTO `etl_plugin_def` VALUES (1002, 'SQL执行', 'SQL', '1', 'SQL', 0, 2);
INSERT INTO `etl_plugin_def` VALUES (1003, '存储过程执行', 'PROCEDURE', '1', 'FUNC-PROCESS', 0, 3);
INSERT INTO `etl_plugin_def` VALUES (1004, '数据迁移', 'CHANGE', '1', 'DATA-TRANSFORM', 0, 4);
INSERT INTO `etl_plugin_def` VALUES (1006, 'FTP', 'READER', '1', NULL, 1005, 1);
INSERT INTO `etl_plugin_def` VALUES (1007, 'MYSQL', 'READER', '1', NULL, 1005, 2);
INSERT INTO `etl_plugin_def` VALUES (1008, 'GP', 'READER', '1', NULL, 1005, 3);
INSERT INTO `etl_plugin_def` VALUES (1009, 'FTP', 'WRITER', '1', NULL, 1005, 1);
INSERT INTO `etl_plugin_def` VALUES (1010, 'MYSQL', 'WRITER', '1', NULL, 1005, 2);
INSERT INTO `etl_plugin_def` VALUES (1011, 'GP', 'WRITER', '1', NULL, 1005, 3);
INSERT INTO `etl_plugin_def` VALUES (1012, 'TXT', 'READER', '1', NULL, 1005, 4);
INSERT INTO `etl_plugin_def` VALUES (1013, 'TXT', 'WRITER', '1', NULL, 1005, 4);
INSERT INTO `etl_plugin_def` VALUES (1014, '文件检查', 'CHECK', '1', 'FILE-CHECK', 0, 9);
INSERT INTO `etl_plugin_def` VALUES (1015, '文件入GP', 'LOAD', '1', 'GP-LOAD', 0, 10);
INSERT INTO `etl_plugin_def` VALUES (1016, 'ORACLE', 'READER', '1', NULL, 1005, 5);
INSERT INTO `etl_plugin_def` VALUES (1017, '多任务执行', 'MUTIF', '1', 'MULTI-TASK', 0, 11);
COMMIT;

SET FOREIGN_KEY_CHECKS = 1;

```

# 系统管理表

### **sys_menu**

| 字段        | 类型          | 允许空 | 默认 | 注释       |
| :---------- | :------------ | :----- | ---- | ---------- |
| menu_id     | bigint(20)    | NO     | NULL | 无         |
| menu_name   | varchar(50)   | YES    | NULL | 菜单名称   |
| menu_url    | varchar(200)  | YES    | NULL | url        |
| state       | varchar(1)    | YES    | NULL | 0禁用1启用 |
| sort        | int(11)       | YES    | NULL | 排序       |
| remark      | varchar(1000) | YES    | NULL | 无         |
| staff_id    | varchar(20)   | YES    | NULL | 无         |
| create_time | datetime      | YES    | NULL | 无         |
| update_time | datetime      | YES    | NULL | 无         |
| class_name  | varchar(255)  | YES    | NULL | 无         |

```sql
/*
 Navicat Premium Data Transfer

 Source Server         : 192.168.100.53
 Source Server Type    : MySQL
 Source Server Version : 50634
 Source Host           : 192.168.100.53:3306
 Source Schema         : dvpdpdb01

 Target Server Type    : MySQL
 Target Server Version : 50634
 File Encoding         : 65001

 Date: 12/02/2020 10:32:30
*/

SET NAMES utf8mb4;
SET FOREIGN_KEY_CHECKS = 0;
-- ----------------------------
-- Table structure for sys_menu
-- ----------------------------
DROP TABLE IF EXISTS `sys_menu`;
CREATE TABLE `sys_menu` (
  `menu_id` bigint(20) NOT NULL AUTO_INCREMENT,
  `menu_name` varchar(50) DEFAULT NULL COMMENT ' 菜单名称',
  `menu_url` varchar(200) DEFAULT NULL COMMENT 'url',
  `state` varchar(1) DEFAULT NULL COMMENT '0禁用1启用',
  `sort` int(11) DEFAULT NULL COMMENT '排序',
  `remark` varchar(1000) DEFAULT NULL,
  `staff_id` varchar(20) DEFAULT NULL,
  `create_time` datetime DEFAULT NULL,
  `update_time` datetime DEFAULT NULL,
  `class_name` varchar(255) DEFAULT NULL,
  PRIMARY KEY (`menu_id`)
) ENGINE=InnoDB AUTO_INCREMENT=1000013 DEFAULT CHARSET=utf8 COMMENT='菜单表';

-- ----------------------------
-- Records of sys_menu
-- ----------------------------
BEGIN;
INSERT INTO `sys_menu` VALUES (1, '角色管理', '/home/rolelist', '1', 1, '111', 'admin', '2018-08-27 09:31:34', '2019-04-19 14:12:19', 'rolelist');
INSERT INTO `sys_menu` VALUES (2, '用户管理', '/home/userlist', '1', 2, '', 'admin', '2018-08-27 09:31:51', '2018-09-17 11:17:11', 'userlist');
INSERT INTO `sys_menu` VALUES (3, '菜单管理', '/home/menulist', '1', 3, NULL, 'admin', '2018-11-19 02:23:55', '2018-11-19 02:23:55', 'menulist');
INSERT INTO `sys_menu` VALUES (1000000, '1', '1', '0', 1, '1', 'admin', '2019-01-23 16:29:11', '2019-01-23 16:29:16', '1');
INSERT INTO `sys_menu` VALUES (1000001, '流程配置', '/home/etl', '1', 4, NULL, 'admin', '2019-01-24 10:46:15', '2019-01-30 10:30:59', 'etl');
INSERT INTO `sys_menu` VALUES (1000002, '任务管理', '/home/tasklist', '1', 5, NULL, 'admin', '2019-01-21 13:26:27', '2019-01-30 10:35:08', 'tasklist');
INSERT INTO `sys_menu` VALUES (1000003, '插件管理', '/home/pluginlist', '1', 6, 'plugin', 'admin', '2019-01-30 10:34:38', '2019-01-30 10:35:51', 'plugin');
INSERT INTO `sys_menu` VALUES (1000005, '资源管理', '/home/dataSource', '1', 7, 'dataSource', 'admin', '2019-02-12 11:19:13', '2019-02-14 09:33:15', 'dataSource');
INSERT INTO `sys_menu` VALUES (1000006, 'DATAX配置', '/home/dataxConfig', '1', 8, 'dataxConfig', 'admin', '2019-02-14 13:51:27', '2019-02-14 13:51:27', 'dataxConfig');
INSERT INTO `sys_menu` VALUES (1000009, '参数配置', '/home/configParam', '1', 9, 'configParam', 'admin', '2019-03-05 15:36:38', '2019-03-05 15:36:38', 'configParam');
INSERT INTO `sys_menu` VALUES (1000010, '缓存配置', '/home/configProperty', '1', 10, 'configProperty', 'admin', '2019-04-10 09:46:00', '2019-04-10 09:46:02', 'configProperty');
INSERT INTO `sys_menu` VALUES (1000012, '模板管理', '/home/templateTasklist', '1', 2, NULL, 'admin', '2020-01-19 15:05:26', '2020-01-19 15:05:26', 'moduleManage');
COMMIT;

SET FOREIGN_KEY_CHECKS = 1;
```





### **sys_role**

| 字段        | 类型          | 允许空 | 默认 | 注释       |
| :---------- | :------------ | :----- | ---- | ---------- |
| role_id     | bigint(20)    | NO     | NULL | 无         |
| role_name   | varchar(50)   | YES    | NULL | 无         |
| role_code   | varchar(20)   | YES    | NULL | 无         |
| state       | varchar(1)    | YES    | NULL | 0禁用1启用 |
| remark      | varchar(1000) | YES    | NULL | 无         |
| staff_id    | varchar(20)   | YES    | NULL | 无         |
| create_time | datetime      | YES    | NULL | 无         |
| update_time | datetime      | YES    | NULL | 无         |

```sql
/*
 Navicat Premium Data Transfer

 Source Server         : 192.168.100.53
 Source Server Type    : MySQL
 Source Server Version : 50634
 Source Host           : 192.168.100.53:3306
 Source Schema         : dvpdpdb01

 Target Server Type    : MySQL
 Target Server Version : 50634
 File Encoding         : 65001

 Date: 12/02/2020 10:39:37
*/

SET NAMES utf8mb4;
SET FOREIGN_KEY_CHECKS = 0;

-- ----------------------------
-- Table structure for sys_role
-- ----------------------------
DROP TABLE IF EXISTS `sys_role`;
CREATE TABLE `sys_role` (
  `role_id` bigint(20) NOT NULL AUTO_INCREMENT,
  `role_name` varchar(50) DEFAULT NULL,
  `role_code` varchar(20) DEFAULT NULL,
  `state` varchar(1) DEFAULT NULL COMMENT '0禁用1启用',
  `remark` varchar(1000) DEFAULT NULL,
  `staff_id` varchar(20) DEFAULT NULL,
  `create_time` datetime DEFAULT NULL,
  `update_time` datetime DEFAULT NULL,
  PRIMARY KEY (`role_id`)
) ENGINE=InnoDB AUTO_INCREMENT=1000021 DEFAULT CHARSET=utf8 COMMENT='这是角色表';

-- ----------------------------
-- Records of sys_role
-- ----------------------------
BEGIN;
INSERT INTO `sys_role` VALUES (1, '系统管理员', 'admin', '1', '系统管理员', 'admin', '2018-08-10 14:46:03', '2018-08-28 10:17:24');
INSERT INTO `sys_role` VALUES (2, '管理员', 'user', '1', '管理员', NULL, NULL, NULL);
INSERT INTO `sys_role` VALUES (1000000, '测试', 'test', '0', NULL, 'admin', '2019-02-25 14:25:54', '2019-02-25 15:09:42');

COMMIT;

SET FOREIGN_KEY_CHECKS = 1;
```

### sys_user_role

| 字段         | 类型        | 允许空 | 默认 | 注释 |
| :----------- | :---------- | :----- | ---- | ---- |
| user_role_id | bigint(20)  | NO     | NULL | 无   |
| user_id      | bigint(20)  | YES    | NULL | 无   |
| role_id      | bigint(20)  | YES    | NULL | 无   |
| staff_id     | varchar(20) | YES    | NULL | 无   |
| create_time  | datetime    | YES    | NULL | 无   |

```sql
/*
 Navicat Premium Data Transfer

 Source Server         : 192.168.100.53
 Source Server Type    : MySQL
 Source Server Version : 50634
 Source Host           : 192.168.100.53:3306
 Source Schema         : dvpdpdb01

 Target Server Type    : MySQL
 Target Server Version : 50634
 File Encoding         : 65001

 Date: 12/02/2020 10:45:03
*/

SET NAMES utf8mb4;
SET FOREIGN_KEY_CHECKS = 0;

-- ----------------------------
-- Table structure for sys_user_role
-- ----------------------------
DROP TABLE IF EXISTS `sys_user_role`;
CREATE TABLE `sys_user_role` (
  `user_role_id` bigint(20) NOT NULL AUTO_INCREMENT,
  `user_id` bigint(20) DEFAULT NULL,
  `role_id` bigint(20) DEFAULT NULL,
  `staff_id` varchar(20) DEFAULT NULL,
  `create_time` datetime DEFAULT NULL,
  PRIMARY KEY (`user_role_id`)
) ENGINE=InnoDB AUTO_INCREMENT=1000015 DEFAULT CHARSET=utf8 COMMENT='sys_user_role';

SET FOREIGN_KEY_CHECKS = 1;

```





### sys_user

| 字段        | 类型        | 允许空 | 默认 | 注释         |
| :---------- | :---------- | :----- | ---- | ------------ |
| user_id     | bigint(20)  | NO     | NULL | 无           |
| login_code  | varchar(50) | YES    | NULL | 登录账号     |
| password    | varchar(50) | YES    | NULL | 登录密码     |
| user_name   | varchar(50) | YES    | NULL | 姓名         |
| phone       | varchar(11) | YES    | NULL | 联系电话     |
| state       | varchar(1)  | YES    | NULL | 0禁用1启用   |
| sex         | varchar(5)  | YES    | NULL | 性别         |
| email       | varchar(50) | YES    | NULL | 邮箱         |
| staff_id    | varchar(20) | YES    | NULL | 无           |
| create_time | datetime    | YES    | NULL | 无           |
| update_time | datetime    | YES    | NULL | 无           |
| login_time  | datetime    | YES    | NULL | 最后登录时间 |
| ip          | varchar(20) | YES    | NULL | 最近访问ip   |

```sql
/*
 Navicat Premium Data Transfer

 Source Server         : 192.168.100.53
 Source Server Type    : MySQL
 Source Server Version : 50634
 Source Host           : 192.168.100.53:3306
 Source Schema         : dvpdpdb01

 Target Server Type    : MySQL
 Target Server Version : 50634
 File Encoding         : 65001

 Date: 12/02/2020 10:44:55
*/

SET NAMES utf8mb4;
SET FOREIGN_KEY_CHECKS = 0;

-- ----------------------------
-- Table structure for sys_user
-- ----------------------------
DROP TABLE IF EXISTS `sys_user`;
CREATE TABLE `sys_user` (
  `user_id` bigint(20) NOT NULL AUTO_INCREMENT,
  `login_code` varchar(50) DEFAULT NULL COMMENT '登录账号',
  `password` varchar(50) DEFAULT NULL COMMENT '登录密码',
  `user_name` varchar(50) DEFAULT NULL COMMENT '姓名',
  `phone` varchar(11) DEFAULT NULL COMMENT '联系电话',
  `state` varchar(1) DEFAULT NULL COMMENT '0禁用1启用',
  `sex` varchar(5) DEFAULT NULL COMMENT '性别',
  `email` varchar(50) DEFAULT NULL COMMENT '邮箱',
  `staff_id` varchar(20) DEFAULT NULL,
  `create_time` datetime DEFAULT NULL,
  `update_time` datetime DEFAULT NULL,
  `login_time` datetime DEFAULT NULL COMMENT '最后登录时间',
  `ip` varchar(20) DEFAULT NULL COMMENT '最近访问ip',
  PRIMARY KEY (`user_id`)
) ENGINE=InnoDB AUTO_INCREMENT=1000013 DEFAULT CHARSET=utf8 COMMENT='sys_user表';

-- ----------------------------
-- Records of sys_user
-- ----------------------------
BEGIN;
INSERT INTO `sys_user` VALUES (1, 'admin', 'E10ADC3949BA59ABBE56E057F20F883E', '管理员', '13822226666', '1', NULL, NULL, NULL, NULL, '2019-04-04 14:34:05', '2020-02-12 10:30:58', NULL);

COMMIT;

SET FOREIGN_KEY_CHECKS = 1;

```

### sys_role_menu

| 字段         | 类型        | 允许空 | 默认 | 注释 |
| :----------- | :---------- | :----- | ---- | ---- |
| role_menu_id | bigint(20)  | NO     | NULL | 无   |
| menu_id      | bigint(20)  | YES    | NULL | 无   |
| role_id      | bigint(20)  | YES    | NULL | 无   |
| staff_id     | varchar(20) | YES    | NULL | 无   |
| create_time  | datetime    | YES    | NULL | 无   |

```sql
/*
 Navicat Premium Data Transfer

 Source Server         : 192.168.100.53
 Source Server Type    : MySQL
 Source Server Version : 50634
 Source Host           : 192.168.100.53:3306
 Source Schema         : dvpdpdb01

 Target Server Type    : MySQL
 Target Server Version : 50634
 File Encoding         : 65001

 Date: 12/02/2020 10:44:44
*/

SET NAMES utf8mb4;
SET FOREIGN_KEY_CHECKS = 0;

-- ----------------------------
-- Table structure for sys_role_menu
-- ----------------------------
DROP TABLE IF EXISTS `sys_role_menu`;
CREATE TABLE `sys_role_menu` (
  `role_menu_id` bigint(20) NOT NULL AUTO_INCREMENT,
  `menu_id` bigint(20) DEFAULT NULL,
  `role_id` bigint(20) DEFAULT NULL,
  `staff_id` varchar(20) DEFAULT NULL,
  `create_time` datetime DEFAULT NULL,
  PRIMARY KEY (`role_menu_id`)
) ENGINE=InnoDB AUTO_INCREMENT=1000313 DEFAULT CHARSET=utf8 COMMENT='sys_role_menu';

SET FOREIGN_KEY_CHECKS = 1;


```



### **config_property**

| 字段           | 类型          | 允许空 | 默认 | 注释                           |
| :------------- | :------------ | :----- | ---- | ------------------------------ |
| PROPERTY_ID    | bigint(20)    | NO     | NULL | 无                             |
| SYS_ID         | varchar(255)  | YES    | NULL | 系统IDSYS-系统管理MONITOR-监控 |
| PROPERTY_KEY   | varchar(255)  | NO     | NULL | 参数key                        |
| PROPERTY_VALUE | varchar(2000) | NO     | NULL | 参数值                         |
| PROPERTY_DESC  | varchar(255)  | NO     | NULL | 配置说明                       |
| STATE          | varchar(255)  | YES    | NULL | 无                             |
| CREATE_USER_ID | bigint(20)    | YES    | NULL | 创建人                         |
| CREATE_TIME    | datetime      | YES    | NULL | 创建时间                       |
| UPDATE_TIME    | datetime      | YES    | NULL | 更新时间                       |

```sql
/*
 Navicat Premium Data Transfer

 Source Server         : 192.168.100.53
 Source Server Type    : MySQL
 Source Server Version : 50634
 Source Host           : 192.168.100.53:3306
 Source Schema         : dvpdpdb01

 Target Server Type    : MySQL
 Target Server Version : 50634
 File Encoding         : 65001

 Date: 12/02/2020 13:48:34
*/

SET NAMES utf8mb4;
SET FOREIGN_KEY_CHECKS = 0;

-- ----------------------------
-- Table structure for config_property
-- ----------------------------
DROP TABLE IF EXISTS `config_property`;
CREATE TABLE `config_property` (
  `PROPERTY_ID` bigint(20) NOT NULL AUTO_INCREMENT,
  `SYS_ID` varchar(255) DEFAULT NULL COMMENT '系统ID  SYS-系统管理  MONITOR-监控',
  `PROPERTY_KEY` varchar(255) NOT NULL COMMENT '参数key\r\n            ',
  `PROPERTY_VALUE` varchar(2000) NOT NULL COMMENT '参数值',
  `PROPERTY_DESC` varchar(255) NOT NULL COMMENT '配置说明\r\n            ',
  `STATE` varchar(255) DEFAULT NULL,
  `CREATE_USER_ID` bigint(20) DEFAULT NULL COMMENT '创建人',
  `CREATE_TIME` datetime DEFAULT NULL COMMENT '创建时间',
  `UPDATE_TIME` datetime DEFAULT NULL COMMENT '更新时间',
  PRIMARY KEY (`PROPERTY_ID`)
) ENGINE=InnoDB AUTO_INCREMENT=404 DEFAULT CHARSET=utf8 COMMENT='配置常用参数';

SET FOREIGN_KEY_CHECKS = 1;
```

config_parameter

| 字段            | 类型         | 允许空 | 默认 | 注释                        |
| :-------------- | :----------- | :----- | ---- | --------------------------- |
| ID              | bigint(20)   | NO     | NULL | 无                          |
| PARAMETER_NAME  | varchar(200) | YES    | NULL | 参数名                      |
| PARAMETER_VALUE | varchar(200) | YES    | NULL | 参数值                      |
| PARAMETER_TYPE  | varchar(2)   | YES    | NULL | 无                          |
| PARAMETER_CONF  | varchar(200) | YES    | NULL | 参数其他的配置,例如数据源ID |
| STATE           | varchar(2)   | YES    | NULL | 无                          |
| REMARK          | varchar(500) | YES    | NULL | 无                          |

```sql
/*
 Navicat Premium Data Transfer

 Source Server         : 192.168.100.53
 Source Server Type    : MySQL
 Source Server Version : 50634
 Source Host           : 192.168.100.53:3306
 Source Schema         : dvpdpdb01

 Target Server Type    : MySQL
 Target Server Version : 50634
 File Encoding         : 65001

 Date: 12/02/2020 13:53:26
*/

SET NAMES utf8mb4;
SET FOREIGN_KEY_CHECKS = 0;

-- ----------------------------
-- Table structure for config_parameter
-- ----------------------------
DROP TABLE IF EXISTS `config_parameter`;
CREATE TABLE `config_parameter` (
  `ID` bigint(20) NOT NULL AUTO_INCREMENT,
  `PARAMETER_NAME` varchar(200) DEFAULT NULL COMMENT '参数名',
  `PARAMETER_VALUE` varchar(200) DEFAULT NULL COMMENT '参数值',
  `PARAMETER_TYPE` varchar(2) DEFAULT NULL,
  `PARAMETER_CONF` varchar(200) DEFAULT NULL COMMENT '参数其他的配置,例如数据源ID',
  `STATE` varchar(2) DEFAULT NULL,
  `REMARK` varchar(500) DEFAULT NULL,
  PRIMARY KEY (`ID`)
) ENGINE=InnoDB AUTO_INCREMENT=24 DEFAULT CHARSET=utf8 COMMENT='config_parameter';

SET FOREIGN_KEY_CHECKS = 1;

```

### config_code

| 字段           | 类型          | 允许空 | 默认 | 注释                            |
| :------------- | :------------ | :----- | ---- | ------------------------------- |
| CONFIG_ID      | bigint(20)    | NO     | NULL | 无                              |
| SYS_ID         | varchar(255)  | YES    | NULL | 系统IDSYS-系统管理 MONITOR-监控 |
| TYPE_CODE      | varchar(255)  | NO     | NULL | 参数key                         |
| PARAM_CODE     | varchar(255)  | NO     | NULL | 参数值                          |
| COLUMN_VALUE   | varchar(1024) | NO     | NULL | CODE值                          |
| COLUMN_DESC    | varchar(1024) | NO     | NULL | CODE描述                        |
| SEQ            | int(11)       | YES    | NULL | 顺序                            |
| STATE          | int(11)       | YES    | NULL | STATE 0-禁用 1启用              |
| CREATE_USER_ID | bigint(20)    | YES    | NULL | 创建人                          |
| CREATE_TIME    | datetime      | YES    | NULL | 创建时间                        |
| UPDATE_TIME    | datetime      | YES    | NULL | 更新时间                        |

```sql
/*
 Navicat Premium Data Transfer

 Source Server         : 192.168.100.53
 Source Server Type    : MySQL
 Source Server Version : 50634
 Source Host           : 192.168.100.53:3306
 Source Schema         : dvpdpdb01

 Target Server Type    : MySQL
 Target Server Version : 50634
 File Encoding         : 65001

 Date: 12/02/2020 13:53:15
*/

SET NAMES utf8mb4;
SET FOREIGN_KEY_CHECKS = 0;

-- ----------------------------
-- Table structure for config_code
-- ----------------------------
DROP TABLE IF EXISTS `config_code`;
CREATE TABLE `config_code` (
  `CONFIG_ID` bigint(20) NOT NULL,
  `SYS_ID` varchar(255) DEFAULT NULL COMMENT '系统ID  SYS-系统管理  MONITOR-监控',
  `TYPE_CODE` varchar(255) NOT NULL COMMENT '参数key\r\n            ',
  `PARAM_CODE` varchar(255) NOT NULL COMMENT '参数值',
  `COLUMN_VALUE` varchar(1024) NOT NULL COMMENT 'CODE值\r\n            ',
  `COLUMN_DESC` varchar(1024) NOT NULL COMMENT 'CODE描述',
  `SEQ` int(11) DEFAULT NULL COMMENT '顺序',
  `STATE` int(11) DEFAULT NULL COMMENT 'STATE 0-禁用  1启用',
  `CREATE_USER_ID` bigint(20) DEFAULT NULL COMMENT '创建人',
  `CREATE_TIME` datetime DEFAULT NULL COMMENT '创建时间',
  `UPDATE_TIME` datetime DEFAULT NULL COMMENT '更新时间',
  PRIMARY KEY (`CONFIG_ID`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='config_code';

SET FOREIGN_KEY_CHECKS = 1;

```

### et~~l_check_def~~

| 字段        | 类型         | 允许空 | 默认 | 注释   |
| :---------- | :----------- | :----- | ---- | ------ |
| CHECK_ID    | bigint(20)   | NO     | NULL | 无     |
| FILE_NAME   | varchar(200) | YES    | NULL | 无     |
| STATE       | char(2)      | YES    | NULL | 无     |
| FILE_COUNT  | bigint(20)   | YES    | NULL | 实际数 |
| CHECK_COUNT | bigint(20)   | YES    | NULL | 目标数 |
| TASK_ID     | bigint(20)   | YES    | NULL | 任务ID |
| LOG_ID      | bigint(20)   | YES    | NULL | LOGID  |

```sql
/*
 Navicat Premium Data Transfer

 Source Server         : 192.168.100.53
 Source Server Type    : MySQL
 Source Server Version : 50634
 Source Host           : 192.168.100.53:3306
 Source Schema         : dvpdpdb01

 Target Server Type    : MySQL
 Target Server Version : 50634
 File Encoding         : 65001

 Date: 12/02/2020 14:01:23
*/

SET NAMES utf8mb4;
SET FOREIGN_KEY_CHECKS = 0;

-- ----------------------------
-- Table structure for etl_check_def
-- ----------------------------
DROP TABLE IF EXISTS `etl_check_def`;
CREATE TABLE `etl_check_def` (
  `CHECK_ID` bigint(20) NOT NULL AUTO_INCREMENT,
  `FILE_NAME` varchar(200) DEFAULT NULL,
  `STATE` char(2) DEFAULT NULL,
  `FILE_COUNT` bigint(20) DEFAULT NULL COMMENT '实际数',
  `CHECK_COUNT` bigint(20) DEFAULT NULL COMMENT '目标数',
  `TASK_ID` bigint(20) DEFAULT NULL COMMENT '任务ID',
  `LOG_ID` bigint(20) DEFAULT NULL COMMENT 'LOGID',
  PRIMARY KEY (`CHECK_ID`)
) ENGINE=InnoDB AUTO_INCREMENT=1000037 DEFAULT CHARSET=utf8 COMMENT='etl_check_def';

SET FOREIGN_KEY_CHECKS = 1;
```

