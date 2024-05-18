---
layout: docker实践和运用

title: docker实践和运用

date: 2023-04-17 23:59:38

tags: Web

categories: Web


top: 25

path: /article/docker

abbrlink: 1177767762
---

# <a href="https://fadeway32.gitee.io/" ><font color="#5577AA" size=8>Docker 原理和实践</font></a>



## <font color="#5577AA" size =5 >Docker原理</font>



***\*Docker是基于Go语言实现的云开源项目。\****

Docker的主要目标是“Build，Ship and Run Any App , Anywhere”，也就是通过对应用组件的封装、分发、部署、运行等生命周期的管理，使用户的APP（可以是一个WEB应用或数据库应用等等）及其运行
环境能够做到“一次封装，到处运行”。Linux 容器技术的出现就解决了这样一个问题，而 Docker 就是在它的基础上发展过来的。将应用运行在Docker 容器上面，而 Docker 容器在任何操作系统上都是一致的，这就实现了跨平台、跨服务器。只需要一次配置好环境，换到别的机子上就可以一键部署好，大大简化了操作。

Docker 可以干嘛

 Docker 和传统虚拟化方式的不同之处：
传统虚拟机技术是虚拟出一套硬件后，在其上运行一个完整操作系统，在该系统上再运行所需应用进程；而容器内的应用进程直接运行于宿主的内核，容器内没有自己的内核，而且也没有进行硬件虚拟。

因此容器要比传统虚拟机更为轻便。每个容器之间互相隔离，每个容器有自己的文件系统 ，容器之间进程不会相互影响，能区分计算资源。



<img src="https://gitee.com/fadeway32/fadeway32/raw/master/img/202304162154536.png" alt="image-20230416215446027" style="zoom:150%;" />



<font color="#5577AA" size=5>镜像（Image)</font>

操作系统分为内核和用户空间。对于Linux而言，内核启动后，会挂载root文件系统为其提供用户空间支持。而Docker镜像（Image），就相当于是一个root文件系统。

~~~ htmkl
Docker设计时，就充分利用Union FS的技术，将其设计为分层存储的架构。
镜像构建时，会一层层构建，前一层是后一层的基础。每一层构建完就不会再发生改变，后一层上的任何改变只发生在自己这一层。比如，删除前一层文件的操作，实际不是真的删除前一层的文件，而是仅在当前层标记为该文件已删除。在最终容器运行的时候，虽然不会看到这个文件，但是实际上该文件会一直跟随镜像。因此，在构建镜像的时候，需要额外小心，每一层尽量只包含该层需要添加的东西，任何额外的东西应该在该层构建结束前清理掉。
~~~

<font color="#5577AA" size =5 >容器（Container）</font>

~~~ html
镜像（Image）和容器（Container）的关系，就像是面向对象程序设计中的类和实例一样，镜像是静态的类，容器是镜像运行时的实体。容器可以被创建、启动、停止、删除、暂停等 。
容器的实质是进程，但与直接在宿主执行的进程不同，容器进程运行于属于自己的独立的命名空间。
前面讲过镜像使用的是分层存储，容器也是如此。
按照Docker最佳实践的要求，容器不应该向其存储层内写入任何数据 ，容器存储层要保持无状态化。所有的文件写入操作，都应该使用数据卷（Volume）、或者绑定宿主目录，在这些位置的读写会跳过容器存储层，直接对宿主（或网络存储）发生读写，其性能和稳定性更高。
~~~

<font color="#5577AA" size =5 >仓库（Repository）</font>

~~~java
一个Docker Registry中可以包含多个仓库（Repository）；每个仓库可以包含多个标签（Tag）；每个标签对应一个镜像。
通常，一个仓库会包含同一个软件不同版本的镜像，而标签就常用于对应该软件的各个版本 。我们可以通过<仓库名>:<标签>的格式来指定具体是这个软件哪个版本的镜像。
如果不给出标签，将以latest作为默认标签。
最常使用的Registry公开服务是官方的Docker Hub ，这也是默认的Registry，并拥有大量的高质量的官方镜像，网址为：http://hub.docker.com 
~~~

## Docker 命令

参考链接：

https://www.runoob.com/docker/docker-tutorial.html

## Docker部署

部署portainer

docker run -ti -d --name kevin-portainer -p 9000:9000 --restart=always -v /var/run/docker.sock:/var/run/docker.sock  portainer/portainer

参考链接：

https://blog.csdn.net/qq_41582883/article/details/113487186

部署mysql 命令

~~~java
1.docker run -it --name=mysql-test -d  --privileged=true  -p 3306:3306 -v /opt/software/mysql/conf:/etc/mysql/conf.d -v /opt/software/mysql/data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD='123456'  mysql

2.grant all privileges on *.* to 'root'@'%'；

3.flush privileges

~~~

参考文章：



https://www.cnblogs.com/tester-ggf/p/15800220.html



