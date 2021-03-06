# ubuntu配置
## 一、更换软件源
> 默认的软件源在国外，下载太慢了，建议更换到aliyun
## 二、安装vim
``` sudo apt install vim  ```   
> apt 是apt-get的子集，建议使用apt  
> yum 和 apt 都是linux平台软件依赖安装的管理工具，一般红帽用yum,ubuntu用apt
## 三、给ubuntu 18.04添加root用户
***
Linux系统下文件的权限十分重要，大多数操作都需要一定的权限才可以操作，Ubuntu18.04默认安装是没有设置root账户的，因此想要获得root账户登录可以使用以下步骤：
***
1. 首先获得临时的root权限，因为后面的一些操作需要root权限才可以，打开终端输入以下命令
```sudo -s```
>之后直接输入当前账户的密码，就可以获得临时的root权限
2. 先创建root账户：
```sudo passwd root```
>根据提示输入密码（此时输入的密码是以后登录root账户时的密码）

3. 修改配置文件
```vi /usr/share/lightdm/lightdm.conf.d/50-unity-greeter.conf```
>（对普通文件进行编辑一定要先获得root权限）
打开后，在文档末尾输入
```
greeter-show-manual-login = true
all-guest = false
```
4. 去除gdm登陆用户名检测：
```
vi /etc/pam.d/gdm-autologin  
vi /etc/pam.d/gdm-password
```    
> 都注释掉以下语句 auth required pam_succeed_if.so user != root quiet_success  
5. 修改/root/.profile文件
``` vi /root/.profile```
>文档最后一行 mesg n || true 前添加  tty -s && 即``` tty -s &&mesg n || true```

6. 重启系统，终端界面输入 #reboot
>重启完成后，登陆界面选择 “未列出”，之后用户名输入 root 进行登录即可。
## 四、安装ssh
 1. 安装启动ssh
 ```
 apt install openssh-client   
 apt install openssh-server  
 service ssh start 
 ```
 2. root方式远程登录  
 ```vi /etc/ssh/sshd_config```
 > 修改 PermitRootLogin yes （默认为#PermitRootLogin prohibit-password）
