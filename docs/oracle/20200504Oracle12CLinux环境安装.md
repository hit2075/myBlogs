# 1.课程来源

https://study.163.com/course/courseMain.htm?courseId=1209660808

# 2. 老师：风哥数据库

# 3.环境

Vmware WorkStation 虚拟机名称：fgedu51

用户名：root 

密码：Ad123

硬盘设置为：非永久（重启后还原）

# 4.基本目标

- 操作系统：Oracle Linux 7.6 x86_64

- 数据库版本：Oracle12cR2版本+多租户架构

- 创建数据库：itpuxdb

- 字符集：ZHS16GBK

- 数据块大小：8k

- 可以远程链接，提供给软件开发人员使用。

#Oracle12c安装过程

## 配置hosts

```shell
echo "192.168.31.51 fgedu51" >> /etc/hosts
```

## 关闭防火墙

```shell
 systemctl stop firewalld.service
 systemctl disable firewalld.service
```

## 创建用户，组，目录，权限

```shell
groupadd dba
useradd -g dba oracle
passwd oracle
mkdir -p /oracle/app/oracle
chown -R oracle:dba /oracle
chmod -R 775 /oracle
```

## 配置yum软件安装所需包

```shell
mkdir /mnt/linux
mount /dev/cdrom /mnt/linux
cd /etc/yum.repos.d
mkdir bk
mv *.repo bk/
echo "[EL]" >> /etc/yum.repos.d/itpux.repo
echo "name=Linux 7.x DVD" >> /etc/yum.repos.d/itpux.repo
echo "baseurl=file:///mnt/linux" >> /etc/yum.repos.d/itpux.repo
echo "gpgcheck=0" >> /etc/yum.repos.d/itpux.repo
echo "enable=1" >> /etc/yum.repos.d/itpux.repo
cat /etc/yum.repos.d/itpux.repo
```

## 安装:oracle所需要的软件安装包.txt

```shell
yum -y install autoconf
yum -y install automake
yum -y install binutils
yum -y install binutils-devel
yum -y install bison
yum -y install cpp
yum -y install dos2unix
yum -y install ftp
yum -y install gcc
yum -y install gcc-c++
yum -y install lrzsz
yum -y install python-devel
yum -y install compat-db*
yum -y install compat-gcc-34
yum -y install compat-gcc-34-c++
yum -y install compat-libcap1
yum -y install compat-libstdc++-33
yum -y install compat-libstdc++-33.i686
yum -y install glibc-*
yum -y install glibc-*.i686
yum -y install libXpm-*i686
yum -y install libXp.so6
yum -y install libXt.so6
yum -y install libXp.so.6
yum -y install libXt.so.6
yum -y install libXtst.so.6
yum -y install libXext
yum -y install libXext.i686
yum -y install libXtst
yum -y install libXtst.i686
yum -y install libX11
yum -y install libX11.i686
yum -y install libXau
yum -y install libXau.i686
yum -y install libXcb
yum -y install libXcb.i686
yum -y install libXi
yum -y install libXi.i686
yum -y install libXtst
yum -y install libstdc++-docs
yum -y install libgcc_s.so.1
yum -y install libstdc++.i686
yum -y install libstdc++-devel
yum -y install libstdc++-devel.i686
yum -y install libaio
yum -y install libaio.i686
yum -y install libaio-devel
yum -y install libaio-devel.i686
yum -y install ksh
yum -y instal libXp
yum -y instal libaio-devel
yum -y install libXp
yum -y install libaio-devel
yum -y install libaio-devel.i686
yum -y install numactl
yum -y install numactl-devel
yum -y install make -y
yum -y install sysstat -y
yum -y install unixODBC
yum -y install unixODBC-devel
yum -y install elfutils-libelf-devel
yum -y install redhat-lsb-core
```

## 配置环境变量

```shell
su - oracle
echo "export LANG=en_US" >> ~/.bash_profile
echo "export ORACLE_BASE=/oracle/app/oracle" >> ~/.bash_profile
echo "export ORACLE_HOME=/oracle/app/oracle/product/12.2.0/db_1" >> ~/.bash_profile
echo "export ORACLE_UNQNAME=itpuxdb" >> ~/.bash_profile
echo "export ORACLE_SID=itpuxdb" >> ~/.bash_profile
echo "export NLS_LANG=AMERICAN_AMERICA.ZHS16GBK;export NLS_LANG" >> ~/.bash_profile
echo "export PATH=$PATH:/oracle/app/oracle/product/12.2.0/db_1/bin" >> /.bash_profile
source ~/.bash_profile
```

## 解压安装包

```shell
su - oracle
cd /oracle
unzip /mnt/hgfs/..../linuxx64_12201*
cd database
./runInstaller
```

## 图形化界面安装

- 登录oracle用户

- /oracle/database/runInstaller 启动图形化安装界面

- 去掉 Oracle support

- create and configure a database

- server class

- single instance datatbase installation

- advance

- nterprise

- general purpose

- itpuxdb itpuxpdb

- Character sets ZHS16GBK

- user the same password for all accounts (oracle)

- database operator group——》dba

- fix & check again

- 使用root用户执行"/tmp/..../runfixup.sh"

- 剩下一个失败Soft Limit maximum stack size 忽略。

- 使用root安装脚本 

```shell
/oracle/app/oraInventory/orainstRoot.sh
/oracle/app/oracle/product/12.2.0/db_1/root.sh
```

## oracle数据库关闭

```sql
show pdbs;
alter pluggable database all close;
shutdown immediate;
exit;
```

```shell
lsnrctl stop
```

## oracle数据库启动

```sql
startup;
show pdbs;
alter pluggable database all open;
exit;
```

```shell
lsnrctl start
```

## 日志路径

```sql
select * from v$diag_info;
```

```shell
cd /oracle/app/oracle/diag/rdbms/itpuxdb/itpuxdb/trace
ls -lsa al*
tail -100f alert_itpuxdb.log
```

## Oracle PDB数据库登录

```sql
show pdbs;
show con_name;
--切换到PDB
alter session set container=ITPUXPDB;
```

## Oracle PDB表空间创建

```sql
select FILE_NAME from dba_data_files;
create tablespace fgedu datafile '/oracle/app/oracle/oradata/itpuxdb/itpuxpdb/fgedu01.dbf' size 10m;
```

## Oracle PDB用户创建

```sql
create user fgedu identified by fgedu default tablespace fgedu;
grant dba to fgedu;
```

## Oracle PDB用户登录

```shell
vi /oracle/app/oracle/product/12.2.0/db_1/network/admin/tnsnames.ora
```

```xml
ITPUXPDB =
 (DESCRIPTION =
  (ADDRESS = (PROTOCOL = TCP)(HOST = fgedu51)(PORT = 1521))
  (CONNECT_DATA =
   (SERVER = DEDICATED)
   (SERVICE_NAME = itpuxpdb)
  )
 )
```

```sql
sqlplus "/as sysdba"
conn fgedu/fgedu@itpuxpdb;
show con_name;
create table itpuxt1(id number(12) primary key,name varchar(20));
```

## Oracle PDB数据插入

```sql
insert into itpuxt1 values(1,'fgedu01');
insert into itpuxt1 values(2,'fgedu02');
commit;
```

## 删除数据库

```shell
su - oracle 
cd $ORACLE_HOME/BIN
./dbca
cd $ ORACLE_HOME/bin
./netca
cd $ORACLE_HOME/deinstall
./deinstall
```

