

## 卸载自带mysql:

 1. 查询mysql的安装情况
 ` rpm -qa | grep mysql –-color`
 2. 卸载原生的MySQL 
 `rpm -e --nodeps mysql-libs-5.1.71-1.el6.i686`

##上传mysql到Centos7:
 

 1. 安装依赖：
`yum -y install libaio.so.1 libgcc_s.so.1 libstdc++.so.6`
`yum  update libstdc++-4.4.7-4.el6.x86_64`
 2. 如果还提示缺少依赖则使用yum缺少什么安装什么，例如：
```
error: Failed dependencies:
        libncurses.so.5 is needed by MySQL-client-5.6.22-1.el6.i686
        libtinfo.so.5 is needed by MySQL-client-5.6.22-1.el6.i686
        ```
        安装缺少的依赖：
       `  yum -y install libncurses.so.5`
 3. 安装mysql的服务端：

安装服务端
`rpm -ivh MySQL-server-5.6.22-1.el6.i686.rpm `
安装mysql的客户端：
`rpm -ivh MySQL-client-5.6.22-1.el6.i686.rpm`
启动mysql的服务：
启动MySQL服务
`service mysql start`
### 设置mysql初始密码并登陆MySQL:

> A RANDOM PASSWORD HAS BEEN SET FOR THE MySQL root USER !
You will find that password in '/root/.mysql_secret'.
You must change that password on your first connect,
no other statement but 'SET PASSWORD' will be accepted.
See the manual for the semantics of the 'password expired' flag.**

根据上面的提示知道，mysql5.6为我们生成了一个随机密码并保存在'/root/.mysql_secret'.里面，现在我们修改密码：

 - 首先去上面的文件里面拷贝密码，然后登录mysql:
`vim /root/.mysql_secret`
> The random password set for the root user at Mon Jan  8 21:39:58 2018 (local time): pRzxLH7xqSLv3htt
登录mysql:

`mysql -u root -p`
重设密码：
` set password=password('123456');`
`select 1;`


###设置开机自动启动mysql:
加入到系统服务：
chkconfig --add mysql
自动启动：
chkconfig mysql on
