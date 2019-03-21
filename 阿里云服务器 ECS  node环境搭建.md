# 云服务器

提供者

​	阿里云

​	百度云

​	新浪云

​	腾讯云

​	。。。



主机： 不建议



## 阿里云服务器 ECS  node环境搭建  流程

1. 购买一个云服务器 

2. 购买域名，进行备案  ||   云服务器提供的 ip地址（公有）

3. 选择公共镜像系统： Centos 64  7.6

4. 自定义密码

   1. 用户名： root
   2. 密码： xxxxxxxxxxxx

5. 记录自己的ip

   1. 公网 **59.110.226.77**   接口  项目地址
   2. 私网 **172.17.91.93**      起本地服务   localhost/主机IP

6. 远程连接

   1. 阿里云服务器网页自带的 ， 输入远程连接密码

   2. git  （推荐） gitbash 客户端输入一下命令

      `ssh root@公网IP `

      1. 连接是如果报错： 

         ```
         @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
         @    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
         @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
         IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
         Someone could be eavesdropping on you right now (man-in-the-middle attack)!
         It is also possible that a host key has just been changed.
         The fingerprint for the ECDSA key sent by the remote host is
         SHA256:AsIAPiYK8s+4gu6of4Xui8yjWCQ1lqltMow9iPvD85U.
         Please contact your system administrator.
         Add correct host key in /c/Users/Pc/.ssh/known_hosts to get rid of this message.
         Offending ECDSA key in /c/Users/Pc/.ssh/known_hosts:1
         ECDSA host key for 59.110.226.77 has changed and you have requested strict checking.
         Host key verification failed.
         
         ```

         解决方案： 

         `rm -rf ~/.ssh/known_hosts  `

7.  安装node

```
如何从EPEL库安装Node.js

另一个有效且简单的方法来安装Node.js就是从官方库。这同样确保您可以访问到EPEL库，

你可以通过运行以下命令。

sudo yum install epel-release

现在可以使用yum命令安装Node.js了。

sudo yum install nodejs

因为在开发过程中我需要管理节点包，我还要安装新公共管理的软件包管理器，

使用以下命令。

sudo yum install npm

whereis node 

```

8. 配置安全组

   1. 端口范围   1/60000
   2. 授权对象： 0.0.0.0/0

9. 书写代码来测试一下 node  使用

   1. 先使用express简单搭建一个服务器， 暴露几个接口， 本地测试， 测试通过在去连接远程

10. 连接远程服务器， 上传本地代码（本地文件） xftp 5

    1. 安装时我们选择 ： 选择第一个  ： 商用  添加注册码： 101210-450789-147200 

    2. 新建一个会话 连接远程服务器

       ![xftp5-会话创建](E:\1809\04-React Native\day05\xftp5-会话创建.png)



3. 连接之后就可以看到我们 远程服务器的根目录  /root

 4. 创建一个目录

 5. 将本地代码传输到 远程服务器目录（不要上传node_modules等文件）

 6. 在远程服务器目录 安装依赖  npm i 

 7. 启动项目 

    

11.添加负载均衡    pm2 https://www.cnblogs.com/lxg0/p/7771229.html

```
npm i pm2 -g 全局安装pm2

pm2 start app.js  后台挂起服务

pm2 list  查看后台挂起所有服务

pm2 stop id  根据服务id 停止当前服务 

pm2 delete id 根据服务 id 删除当前服务 

pm2 restart id 重启服务 

```

12. 安装  mongodb  数据库  http://www.cnblogs.com/web424/p/6928992.html 
    1. vim命令基本使用
       1. vim a.txt
       2. 先按键盘的 I
       3. 写入内容 （shift + ins）
       4. 退出 先按 ESC 键
       5. 再打 **: wq** 会出即可保存并退出
    2. 注意点： 防火墙忽略

**简介**
MongoDB 是一个介于关系数据库和非关系数据库之间的产品，是非关系数据库当中功能最丰富，最像关系数据库的。他支持的数据结构非常松散，是类似json的bson格式，因此可以存储比较复杂的数据类型。Mongo最大的特点是他支持的查询语言非常强大，其语法有点类似于面向对象的查询语言，几乎可以实现类似关系数据库单表查询的绝大部分功能，而且还支持对数据建立索引。
Packages包说明
MongoDB官方源中包含以下几个依赖包：
mongodb-org: MongoDB元数据包，安装时自动安装下面四个组件包：
1.mongodb-org-server: 包含MongoDB守护进程和相关的配置和初始化脚本。
2.mongodb-org-mongos: 包含mongos的守护进程。
3.mongodb-org-shell: 包含mongo shell。
4.mongodb-org-tools: 包含MongoDB的工具： mongoimport, bsondump, mongodump, mongoexport, mongofiles, mongooplog, mongoperf, mongorestore, mongostat, and mongotop。

**安装步骤**

**1.配置MongoDB的yum源**

创建yum源文件：
vim /etc/yum.repos.d/mongodb-org-3.4.repo
添加以下内容：
[mongodb-org-3.4]  
name=MongoDB Repository  
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.4/x86_64/  
gpgcheck=1  
enabled=1  
gpgkey=https://www.mongodb.org/static/pgp/server-3.4.asc

这里可以修改 gpgcheck=0, 省去gpg验证

安装之前先更新所有包 ：yum update （可选操作）

**2.安装MongoDB**
安装命令：
yum -y install mongodb-org

![img](https://images2015.cnblogs.com/blog/1152574/201706/1152574-20170601160538196-1564302992.png)

 

安装完成后

查看mongo安装位置 whereis mongod

查看修改配置文件 ： vim /etc/mongod.conf

 

**3.启动MongoDB** 
启动mongodb ：systemctl start mongod.service
停止mongodb ：systemctl stop mongod.service

查到mongodb的状态：systemctl status mongod.service

![img](https://images2015.cnblogs.com/blog/1152574/201706/1152574-20170601161448399-2066311169.png)

4.外网访问需要关闭防火墙：

 

 

 

 

 

 

5.设置开机启动

 

**![img](https://images2015.cnblogs.com/blog/1152574/201706/1152574-20170601161522071-1909983030.png)**

6.启动Mongo shell

 

 

 

查看数据库：show dbs

![img](https://images2015.cnblogs.com/blog/1152574/201706/1152574-20170601161721258-1755127562.png)

7.设置mongodb远程访问：

 

 

 ![img](https://images2015.cnblogs.com/blog/1152574/201706/1152574-20170601161847868-46882348.png)

重启mongodb：systemctl restart mongod.service



12. nginx  静态服务器

    **https://www.linuxidc.com/Linux/2016-09/134907.htm**

    ## 安装所需环境

    Nginx 是 C语言 开发，建议在 Linux 上运行，当然，也可以安装 Windows 版本，本篇则使用 [CentOS](https://www.linuxidc.com/topicnews.aspx?tid=14) 7 作为安装环境。

    **一. gcc 安装**
    安装 nginx 需要先将官网下载的源码进行编译，编译依赖 gcc 环境，如果没有 gcc 环境，则需要安装：

    ```
    yum install gcc-c++
    ```

    **二. PCRE pcre-devel 安装**
    PCRE(Perl Compatible Regular Expressions) 是一个Perl库，包括 perl 兼容的正则表达式库。nginx 的 http 模块使用 pcre 来解析正则表达式，所以需要在 linux 上安装 pcre 库，pcre-devel 是使用 pcre 开发的一个二次开发库。nginx也需要此库。命令：

    ```
    yum install -y pcre pcre-devel
    ```

    **三. zlib 安装**
    zlib 库提供了很多种压缩和解压缩的方式， nginx 使用 zlib 对 http 包的内容进行 gzip ，所以需要在 Centos 上安装 zlib 库。

    ```
    yum install -y zlib zlib-devel
    ```

    **四. OpenSSL 安装**
    OpenSSL 是一个强大的安全套接字层密码库，囊括主要的密码算法、常用的密钥和证书封装管理功能及 SSL 协议，并提供丰富的应用程序供测试或其它目的使用。
    nginx 不仅支持 http 协议，还支持 https（即在ssl协议上传输http），所以需要在 Centos 安装 OpenSSL 库。

    ```
    yum install -y openssl openssl-devel
    ```

    ## 官网下载

    1.直接下载`.tar.gz`安装包，地址：<https://nginx.org/en/download.html>

    ![nginx.png](https://www.linuxidc.com/upload/2016_09/160905180451092.png)

    2.使用`wget`命令下载（推荐）。

    ```
    wget -c https://nginx.org/download/nginx-1.10.1.tar.gz
    ```

    ![nginx-wget.png](https://www.linuxidc.com/upload/2016_09/160905180451091.png)

    我下载的是1.10.1版本，这个是目前的稳定版。

    ## 解压

    依然是直接命令：

    ```
    tar -zxvf nginx-1.10.1.tar.gz
    cd nginx-1.10.1
    ```

    ## 配置

    其实在 nginx-1.10.1 版本中你就不需要去配置相关东西，默认就可以了。当然，如果你要自己配置目录也是可以的。
    1.使用默认配置

    ```
    ./configure 
    ```

    2.自定义配置（不推荐）

    ```
    +
    ./configure \
    --prefix=/usr/local/nginx \
    --conf-path=/usr/local/nginx/conf/nginx.conf \
    --pid-path=/usr/local/nginx/conf/nginx.pid \
    --lock-path=/var/lock/nginx.lock \
    --error-log-path=/var/log/nginx/error.log \
    --http-log-path=/var/log/nginx/access.log \
    --with-http_gzip_static_module \
    --http-client-body-temp-path=/var/temp/nginx/client \
    --http-proxy-temp-path=/var/temp/nginx/proxy \
    --http-fastcgi-temp-path=/var/temp/nginx/fastcgi \
    --http-uwsgi-temp-path=/var/temp/nginx/uwsgi \
    --http-scgi-temp-path=/var/temp/nginx/scgi
    ```

    > 注：将临时文件目录指定为/var/temp/nginx，需要在/var下创建temp及nginx目录

    3. 配置https支持的ssl模块

       ```
       ./configure --prefix=/usr/local/nginx --with-http_ssl_module
       ```

    ## 编译安装

    ```
    make
    make install
    ```

    查找安装路径：

    ```
    whereis nginx
    ```

    ![nginx-whereis.png](https://www.linuxidc.com/upload/2016_09/160905180451094.png)

    ## 启动、停止nginx

    ```
    cd /usr/local/nginx/sbin/
    ./nginx 
    ./nginx -s stop
    ./nginx -s quit
    ./nginx -s reload
    ```

    > `./nginx -s quit`:此方式停止步骤是待nginx进程处理任务完毕进行停止。
    > `./nginx -s stop`:此方式相当于先查出nginx进程id再使用kill命令强制杀掉进程。

    查询nginx进程：

    ```
    ps aux|grep nginx
    ```

    ## 重启 nginx

    1.先停止再启动（推荐）：
    对 nginx 进行重启相当于先停止再启动，即先执行停止命令再执行启动命令。如下：

    ```
    ./nginx -s quit
    ./nginx
    ```

    2.重新加载配置文件：
    当 ngin x的配置文件 nginx.conf 修改后，要想让配置生效需要重启 nginx，使用`-s reload`不用先停止 ngin x再启动 nginx 即可将配置信息在 nginx 中生效，如下：
    ./nginx -s reload

    启动成功后，在浏览器可以看到这样的页面：

    ![nginx-welcome.png](https://www.linuxidc.com/upload/2016_09/160905180451093.png)

    ## 开机自启动

    即在`rc.local`增加启动代码就可以了。

    ```
    vi /etc/rc.local
    ```

    增加一行 `/usr/local/nginx/sbin/nginx`
    设置执行权限：

    ```
    chmod 755 rc.local
    ```

    ![nginx-rclocal.png](https://www.linuxidc.com/upload/2016_09/160905180451095.png)

    到这里，nginx就安装完毕了，启动、停止、重启操作也都完成了，当然，你也可以添加为系统服务，我这里就不在演示了。

    

    ### nginx配置问题解决

    1. 问题： 本地项目上传之后， 路由重定向 跳转 404 页面

       解决	

       ​	在 /usr/local/nginx/conf/nginx.conf  中修改如下配置:

       ```
       server {
             listen 10002;
             server_name localhost;
             location / {
                 root zmh_react_project;
                  try_files $uri /index.html; #解决路由重定向跳转 404 页面配置
                  index index.html;
             }
          
           }
       ```

       ```
       总设置  设置不同端口  来运行2个页面
       
       server {
       
       ​        listen       10001;
       
       ​        server_name  localhost;
       
       ​        \#charset koi8-r;
       
       ​        \#access_log  logs/host.access.log  main;
       
       ​        location / {
       
       ​            root   maoyan;
       
       ​           try_files $uri /index.html;
       
       ​            index  index.html index.htm;
       
       ​        }
       
       ​        location /ajax {
       
       ​                proxy_pass http://m.maoyan.com/ajax;
       
       ​        }
       ```

       

    2. 问题： 本地配置的反向代理数据获取不到， 

       解决

       ​	在 /usr/local/nginx/conf/nginx.conf  中修改如下配置:

    ```
    
    server {
          listen 10002;
          server_name localhost;
          location / {
              root zmh_react_project;
               try_files $uri /index.html; #解决路由重定向跳转 404 页面配置
               index index.html;
          }
          location /marketing { # 解决反向代理数据获取不到
                proxy_pass https://resource.smartisan.com/marketing;
          }
          location /ajax: {
                    proxy_pass http://m.maoyan.com/ajax；  // 跨域的路径
                }
          location /product {
                proxy_pass https://www.smartisan.com/product;
          }
        }
    ```

    3. 问题： 多项目配置多个端口

       解决： 在nginx配置文件中添加多个 server配置， 但是要注意  项目文件夹要和 nginx /html目录同级

       ​	

       ```
       目录应该如下： 
           nginx
       
           		html
       
           		vue-project
       
           		react-project
       ```

       ​	在 /usr/local/nginx/conf/nginx.conf  中修改如下配置:

       ```
       server {  #此2为默认端口设置
               listen       80;
               server_name  localhost;
       
               #charset koi8-r;
       
               #access_log  logs/host.access.log  main;
       
               location / {
                   root   project_list;
                   index  index.html index.htm;
               }
       
               #error_page  404              /404.html;
       
               # redirect server error pages to the static page /50x.html
               #
               error_page   500 502 503 504  /50x.html;
               location = /50x.html {
                   root   html;
               }
       
               # proxy the PHP scripts to Apache listening on 127.0.0.1:80
               #
               #location ~ \.php$ {
               #    proxy_pass   http://127.0.0.1;
               #}
       
               # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
               #
               #location ~ \.php$ {
               #    root           html;
               #    fastcgi_pass   127.0.0.1:9000;
               #    fastcgi_index  index.php;
               #    fastcgi_param  SCRIPT_FILENAME  /scripts$fastcgi_script_name;
               #    include        fastcgi_params;
               #}
       
               # deny access to .htaccess files, if Apache's document root
               # concurs with nginx's one
               #
               #location ~ /\.ht {
               #    deny  all;
               #}
           }
       
       server {
             listen 10002;
             server_name localhost;
             location / {
                 root zmh_react_project;
                  try_files $uri /index.html; #解决路由重定向跳转 404 页面配置
                  index index.html;
             }
             location /marketing { # 解决反向代理数据获取不到
                   proxy_pass https://resource.smartisan.com/marketing;
             }
             location /product {
                   proxy_pass https://www.smartisan.com/product;
             }
           }
           
        server {
             listen 10001;
             server_name localhost;
             location / {
                 root zmh_react_project;
                  try_files $uri /index.html; #解决路由重定向跳转 404 页面配置
                  index index.html;
             }
             location /marketing { # 解决反向代理数据获取不到
                   proxy_pass https://resource.smartisan.com/marketing;
             }
             location /product {
                   proxy_pass https://www.smartisan.com/product;
             }
           }
       ```

    4. 问题： ssh连接远程服务器异常

       解决： 

        	1. 保证 git 协议  中的公钥和私钥已配置
        	2. 配置完成之后重启 示例
        	3. 以上都不行， 重装镜像

    

    

    --------------------------------------分割线 --------------------------------------

    Nginx负载均衡配置实战  [http://www.linuxidc.com/Linux/2014-12/110036.htm](https://www.linuxidc.com/Linux/2014-12/110036.htm)

    CentOS 6.2实战部署Nginx+MySQL+PHP [http://www.linuxidc.com/Linux/2013-09/90020.htm](https://www.linuxidc.com/Linux/2013-09/90020.htm)

    使用Nginx搭建WEB服务器 [http://www.linuxidc.com/Linux/2013-09/89768.htm](https://www.linuxidc.com/Linux/2013-09/89768.htm)

    搭建基于Linux6.3+Nginx1.2+PHP5+MySQL5.5的Web服务器全过程 [http://www.linuxidc.com/Linux/2013-09/89692.htm](https://www.linuxidc.com/Linux/2013-09/89692.htm)

    CentOS 6.3下Nginx性能调优 [http://www.linuxidc.com/Linux/2013-09/89656.htm](https://www.linuxidc.com/Linux/2013-09/89656.htm)

    CentOS 6.3下配置Nginx加载ngx_pagespeed模块 [http://www.linuxidc.com/Linux/2013-09/89657.htm](https://www.linuxidc.com/Linux/2013-09/89657.htm)

    CentOS 6.4安装配置Nginx+Pcre+php-fpm [http://www.linuxidc.com/Linux/2013-08/88984.htm](https://www.linuxidc.com/Linux/2013-08/88984.htm)

    Nginx安装配置使用详细笔记 [http://www.linuxidc.com/Linux/2014-07/104499.htm](https://www.linuxidc.com/Linux/2014-07/104499.htm)

    Nginx日志过滤 使用ngx_log_if不记录特定日志 [http://www.linuxidc.com/Linux/2014-07/104686.htm](https://www.linuxidc.com/Linux/2014-07/104686.htm)

    --------------------------------------分割线 --------------------------------------


