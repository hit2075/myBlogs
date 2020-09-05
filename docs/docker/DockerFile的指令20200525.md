步骤：开发、部署、运维。。。缺一不可

DockerFile：构建文件，定义了一切的步骤，源代码

DockerImages：通过DockerFile构建生成镜像，最终发布何运行的产品！

Docker容器：容器就是镜像运行起来提供服务。





### DockerFile的指令

```shell
FROM			# 基础镜像，一切从这里开始构建
MAINTAINER		# 镜像是谁写的，姓名+邮箱
RUN				# 镜像构建的时候需要运行的命令
ADD				# 步骤：tomcat镜像，这个tomcat压缩包！ 添加内容
WORKDIR			# 镜像工作目录
VOLUME			# 挂载目录
EXPOSE			# 保留端口配置
CMD				# 指定这个容器启动时需要运行的命令，只有最后的一个会生效
ENTRYPOINT		# 指定这个容器启动时需要运行的命令，可以追加命令
ONBUILD			# 当构建一个被继承 DockerFile 这个时候就会运行 ONBUILD
COPY			# 类似ADD，将我们文件拷贝到镜像中
ENV				# 构建时设置环境变量
```



### 实战测试

![image-20200526063436765](D:\myBlogs\docs\docker\image-20200526063436765.png)

> 编写一个自己的dockerfile

```shell
# 1 编写一个Dockerfile的文件
[root@docker dockerfile]# cat mydockerfile 
FROM centos
MAINTAINER zhangwenjie<18071081081@189.cn>

ENV MYPATH /usr/local
WORKDIR $MYPATH

RUN yum -y install vim
RUN yum -y install net-tools

EXPOSE 80


CMD echo $MYPATH
CMD echo "----end----"
CMD /bin/bash

# 2、通过这个镜像构建
[root@docker dockerfile]# docker build -f mydockerfile -t mycentos:0.1 .
Sending build context to Docker daemon  2.048kB
Step 1/10 : FROM centos
 ---> 470671670cac
Step 2/10 : MAINTAINER zhangwenjie<18071081081@189.cn>
 ---> Running in 20a737b3a2ea
Removing intermediate container 20a737b3a2ea
 ---> 6d8daa8f0fc8
Step 3/10 : ENV MYPATH /usr/local
 ---> Running in 2574feb10685
Removing intermediate container 2574feb10685
 ---> cf4ea9119d5b
Step 4/10 : WORKDIR $MYPATH
 ---> Running in fd6db63b2c33
Removing intermediate container fd6db63b2c33
 ---> 65785bcf3401
Step 5/10 : RUN yum -y install vim
 ---> Running in 361ae84164fb
CentOS-8 - AppStream                            5.0 MB/s | 7.0 MB     00:01    
CentOS-8 - Base                                 2.8 MB/s | 2.2 MB     00:00    
CentOS-8 - Extras                               8.8 kB/s | 5.9 kB     00:00    
Dependencies resolved.
================================================================================
 Package             Arch        Version                   Repository      Size
================================================================================
Installing:
 vim-enhanced        x86_64      2:8.0.1763-13.el8         AppStream      1.4 M
Installing dependencies:
 gpm-libs            x86_64      1.20.7-15.el8             AppStream       39 k
 vim-common          x86_64      2:8.0.1763-13.el8         AppStream      6.3 M
 vim-filesystem      noarch      2:8.0.1763-13.el8         AppStream       48 k
 which               x86_64      2.21-10.el8               BaseOS          49 k

Transaction Summary
================================================================================
Install  5 Packages

Total download size: 7.8 M
Installed size: 31 M
Downloading Packages:
(1/5): gpm-libs-1.20.7-15.el8.x86_64.rpm        220 kB/s |  39 kB     00:00    
(2/5): vim-filesystem-8.0.1763-13.el8.noarch.rp 582 kB/s |  48 kB     00:00    
(3/5): which-2.21-10.el8.x86_64.rpm             407 kB/s |  49 kB     00:00    
(4/5): vim-enhanced-8.0.1763-13.el8.x86_64.rpm  2.3 MB/s | 1.4 MB     00:00    
(5/5): vim-common-8.0.1763-13.el8.x86_64.rpm    6.3 MB/s | 6.3 MB     00:01    
--------------------------------------------------------------------------------
Total                                           3.9 MB/s | 7.8 MB     00:02     
warning: /var/cache/dnf/AppStream-02e86d1c976ab532/packages/gpm-libs-1.20.7-15.el8.x86_64.rpm: Header V3 RSA/SHA256 Signature, key ID 8483c65d: NOKEY
CentOS-8 - AppStream                            151 kB/s | 1.6 kB     00:00    
Importing GPG key 0x8483C65D:
 Userid     : "CentOS (CentOS Official Signing Key) <security@centos.org>"
 Fingerprint: 99DB 70FA E1D7 CE22 7FB6 4882 05B5 55B3 8483 C65D
 From       : /etc/pki/rpm-gpg/RPM-GPG-KEY-centosofficial
Key imported successfully
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                        1/1 
  Installing       : which-2.21-10.el8.x86_64                               1/5 
  Installing       : vim-filesystem-2:8.0.1763-13.el8.noarch                2/5 
  Installing       : vim-common-2:8.0.1763-13.el8.x86_64                    3/5 
  Installing       : gpm-libs-1.20.7-15.el8.x86_64                          4/5 
  Running scriptlet: gpm-libs-1.20.7-15.el8.x86_64                          4/5 
  Installing       : vim-enhanced-2:8.0.1763-13.el8.x86_64                  5/5 
  Running scriptlet: vim-enhanced-2:8.0.1763-13.el8.x86_64                  5/5 
  Running scriptlet: vim-common-2:8.0.1763-13.el8.x86_64                    5/5 
  Verifying        : gpm-libs-1.20.7-15.el8.x86_64                          1/5 
  Verifying        : vim-common-2:8.0.1763-13.el8.x86_64                    2/5 
  Verifying        : vim-enhanced-2:8.0.1763-13.el8.x86_64                  3/5 
  Verifying        : vim-filesystem-2:8.0.1763-13.el8.noarch                4/5 
  Verifying        : which-2.21-10.el8.x86_64                               5/5 

Installed:
  vim-enhanced-2:8.0.1763-13.el8.x86_64 gpm-libs-1.20.7-15.el8.x86_64          
  vim-common-2:8.0.1763-13.el8.x86_64   vim-filesystem-2:8.0.1763-13.el8.noarch
  which-2.21-10.el8.x86_64             

Complete!
Removing intermediate container 361ae84164fb
 ---> 0e368a7a9d8d
Step 6/10 : RUN yum -y install net-tools
 ---> Running in 277f385f56f8
Last metadata expiration check: 0:00:09 ago on Mon May 25 23:07:49 2020.
Dependencies resolved.
================================================================================
 Package         Architecture Version                        Repository    Size
================================================================================
Installing:
 net-tools       x86_64       2.0-0.51.20160912git.el8       BaseOS       323 k

Transaction Summary
================================================================================
Install  1 Package

Total download size: 323 k
Installed size: 1.0 M
Downloading Packages:
net-tools-2.0-0.51.20160912git.el8.x86_64.rpm   2.0 MB/s | 323 kB     00:00    
--------------------------------------------------------------------------------
Total                                           537 kB/s | 323 kB     00:00     
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                        1/1 
  Installing       : net-tools-2.0-0.51.20160912git.el8.x86_64              1/1 
  Running scriptlet: net-tools-2.0-0.51.20160912git.el8.x86_64              1/1 
  Verifying        : net-tools-2.0-0.51.20160912git.el8.x86_64              1/1 

Installed:
  net-tools-2.0-0.51.20160912git.el8.x86_64                                     

Complete!
Removing intermediate container 277f385f56f8
 ---> 81ecae2fac0f
Step 7/10 : EXPOSE 80
 ---> Running in 29714580205b
Removing intermediate container 29714580205b
 ---> 1f610bf4f0de
Step 8/10 : CMD echo $MYPATH
 ---> Running in 80c78269f658
Removing intermediate container 80c78269f658
 ---> a460a9eb790a
Step 9/10 : CMD echo "----end----"
 ---> Running in cf1f58c65784
Removing intermediate container cf1f58c65784
 ---> 803c3142bd09
Step 10/10 : CMD /bin/bash
 ---> Running in 611b7f0dcd75
Removing intermediate container 611b7f0dcd75
 ---> 34a264f2ff0c
Successfully built 34a264f2ff0c
Successfully tagged mycentos:0.1
```

