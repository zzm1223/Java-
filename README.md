# Java分布式案例，基于<b>dubbo+zookeeper</b>搭建分布式服务
<br /><span style="font-family: simsun; font-size: 18px;">&nbsp; 一步步教你搭建基于Dubbo的分布式大型服务架构<br />Dubbo是一个来自阿里巴巴的开源分布式服务框架，当当根据自身的需求，为Dubbo实现了一些新的功能，包括REST风格远程调用、Kryo/FST序列化等等。并将其命名为Dubbox。<br />Dubbox基于非常成熟的JBoss RestEasy框架，在dubbo中实现了REST风格（HTTP + JSON/XML）的远程调用，以显著简化企业内部的跨语言交互，同时显著简化企业对外的Open API、无线API甚至AJAX服务端等等的开发。</span><br /><br /><br />![image](https://github.com/zzm1223/Java-dubbox/blob/picture/dubbo%E7%95%8C%E9%9D%A2.png)<br /><br /><br /><span style="font-size: 18px;"><b>工具和相关包资源：</b></span><br /><span style="font-size: 16px;"><b>&nbsp; Eclipse IDE;</b><br /><b>&nbsp; dubbo-2.8.4.jar;</b><br /><b>&nbsp; apache-tomcat-7.0.52.tar.gz</b><br /><b>&nbsp; zookeeper-3.4.6.tar.gz；</b><br /><b>&nbsp; apache-maven-3.2.2;</b><br /><b>&nbsp; dubbox-master.zip</b></span><br /><br /><span style="font-size: 18px;"><b>一.JDK安装（jdk1.7）</b></span><br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ......<br /><span style="font-size: 18px;"><b>二.Eclipse安装</b></span><br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ......<br /><span style="font-size: 18px;"><b>三.Maven安装（具体项目会用到）</b></span><br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="font-size: 16px; line-height: 100%;"> 3.1.1. 前往https://maven.apache.org/download.cgi 下载最新版的Maven程序：&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;<br /><br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 3.1.2. 将文件解压到D:\Program Files\Apache\maven目录下:<br /><br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 3.1.3. 新建环境变量MAVEN_HOME，赋值D:\Program Files\Apache\maven<br /><br /><br />![image](https://github.com/zzm1223/Java-dubbox/blob/picture/maven%E7%8E%AF%E5%A2%83%E5%8F%98%E9%87%8F.png)<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 3.1.4. 编辑环境变量Path，追加%MAVEN_HOME%\bin\;<br /><br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 3.1.5. 至此，maven已经完成了安装，我们可以通过DOS命令检查一下我们是否安装成功：<br /><br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; mvn -v</span><br />&nbsp;<span style="font-size: 18px;"><b>3.2、配置Ma</b></span><span style="line-height: 100%; font-size: 18px;"><b>ven本地仓库</b><br /><br /></span><span style="font-size: 16px; font-family: simsun;">&nbsp;3.2.1. 在D:\Program Files\Apache\目录下新建maven-repository文件夹，该目录用作maven的本地库。<br />&nbsp;3.2.2. 打开D:\Program Files\Apache\maven\conf\settings.xml文件，查找下面这行代码：<br />&nbsp;&lt;localRepository&gt;/path/to/local/repo&lt;/localRepository&gt;<br />&nbsp;localRepository节点默认是被注释掉的，需要把它移到注释之外，然后将localRepository节点的值改为我们在3.1中创建的目录D:\Program Files\Apache\maven-repository。<br />&nbsp;3.2.3、配置多个下载仓库中心，在&lt;mirrors&gt;之间添加下载镜像，以便快速下载相关文件。<br />
![image](https://github.com/zzm1223/Java-dubbox/blob/picture/3.2.3.png)<br />
<span>
alimaven <br />
aliyun maven<br />
http://maven.aliyun.com/nexus/content/groups/public/<br />
central<br />
repo2<br />
repo2 maven<br />
http://repo2.maven.org/maven2<br />
central<br /></span>
<br /><span style="font-size: 16px; font-family: simsun;">&nbsp; 3.2.3. localRepository节点用于配置本地仓库，本地仓库其实起到了一个缓存的作用，它的默认地址是 C:\Users\用户名.m2。<br />&nbsp; 当我们从maven中获取jar包的时候，maven首先会在本地仓库中查找，如果本地仓库有则返回；如果没有则从远程仓库中获取包，并在本地库中保存。<br />&nbsp; 此外，我们在maven项目中运行mvn install，项目将会自动打包并安装到本地仓库中。<br />&nbsp; 3.2.4. 运行一下DOS命令<br />&nbsp; mvn help:system<br />&nbsp; 如果前面的配置成功，那么D:\Program Files\Apache\maven-repository会出现一些文件。<br /><br /></span><span style="font-family: simsun; font-size: 18px;"><b>3.3、配置Eclipse的Maven环境</b></span><span style="font-size: 16px; font-family: simsun;"><br />&nbsp; 3.3.1. Eclipse Oxygen，打开Window-&gt;Preferences-&gt;Maven-&gt;Installations，右侧点击Add。<br /><br />&nbsp; 3.3.2. 设置maven的安装目录，然后Finish<br /><br />&nbsp; 3.3.3. 选中刚刚添加的maven，并Apply。<br /><br />&nbsp; 3.3.4. 打开Window-&gt;Preferences-&gt;Maven-&gt;User Settings，配置如下并Apply：<br /><br />&nbsp; 至此，Maven的安装和配置全部结束。<br /></span><span style="font-size: 18px; font-family: simsun;"><b>四、安装VMware &nbsp;</b>&nbsp; &nbsp;<br /><b>五、安装centOS</b><br /><b>六、传送文件</b></span><span style="font-size: 16px; font-family: simsun;"><br />&nbsp; 6.1、传zookeeper-3.4.6.tar.gz到CentOS并解压<br />&nbsp;&nbsp; 找到bin目录下的zkServer.sh启动（./zkServer.sh start）<br />&nbsp; 6.2、传apache-tomcat-7.0.52.tar.gz到CentOS并解压<br />&nbsp;&nbsp; 在bin目录下，输入startup.sh，启动tomcat服务<br />&nbsp; 6.3、将dubbo-admin.war传到CentOS<br />&nbsp;&nbsp; 在客户机上输入IP:8080/dubbo-admin/<br />&nbsp; 访问dubbo管理后台，账号密码都是root<br /><b>&nbsp; 至此，dubbo服务搭建好了</b><br />下面在eclipse里导入一个应用到分布式的项目<br /></span><span style="font-family: simsun; font-size: 18px;"><b>七、dubbo.xsd配置</b></span><span style="font-size: 16px; font-family: simsun;"><br />&nbsp;在Eclipse--窗口--首选项--xml目录--添加--Catalog Entry<br />&nbsp;位置找到配置文件里的dubbo.xsd<br />&nbsp;key值为http://code.alibabatech.com/schema/dubbo/dubbo.xsd<br />&nbsp;<br />![image](https://github.com/zzm1223/Java-dubbox/blob/picture/dubbo.xsd.png)<br /></span><span style="font-family: simsun; font-size: 18px;"><b>八、启用项目</b></span><span style="font-size: 16px; font-family: simsun;"><br />&nbsp;8.1、导入项目文件 <br />![image](https://github.com/zzm1223/Java-dubbox/blob/picture/8.1%E5%AF%BC%E5%85%A5.png) <br />&nbsp;8.2、更新，找到项目右键【Manven】--【Update project...】将相关项目更新一下<br />![image](https://github.com/zzm1223/Java-dubbox/blob/picture/8.2Manven%20updata.png)<br />&nbsp;8.3、安装，找到parent项目，右键【运行方式】--【Manven install】<br />&nbsp;8.4、开启项目<br />&nbsp;8.4.1、开启sellergoods-service项目，找到项目右键【运行方式】--【Manven bulid】--【Goals填写tomcat7:run】启动服务项目<br />&nbsp;8.4.2、开启manager-web项目，找到项目右键【运行方式】--【Manven bulid】--【Goals填写tomcat7:run】启动客户端项目<br />&nbsp;输入</span><span style="font-size: 16px; font-family: simsun; color: rgb(0, 0, 255);">localhost:9101/admin</span><span style="font-size: 16px; font-family: simsun;">即可查看该示例项目 <br />![image](https://github.com/zzm1223/Java-dubbox/blob/picture/8.4.2.png) <br />&nbsp;8.4.3、查看dubbo管理后台<br />&nbsp;输入服务</span><span style="font-size: 16px; font-family: simsun; color: rgb(0, 0, 255);">IP：8080/dubbo-admin/</span><br />&nbsp;<br /> <br />![image](https://github.com/zzm1223/Java-dubbox/blob/picture/8.4.3.png)<br />
