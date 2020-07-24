## 1. 在Centos7上构建属于你自己的Shadowsocks服务
首先你需要购买一台vps服务器，网上有很多vps厂商，比如vultr，virmatch, 搬瓦工等
1. <a href="https://my.vultr.com/deploy/" target="_blank">vultr</a>
  价格还可以，可以无限创建销毁服务器，如果服务器IP被墙的话，最低一个月2.5美金，只提供ipv6, 建议购买5美金的，线路走传统163线路，一般我会选择硅谷地区。
  
2. <a href="https://billing.virmach.com/cart.php?gid=1" target="_blank">virmatch</a>
  价格非常便宜，最低1.5美金，也就是不到10RMB，而且带宽大，有1GB，速率有1GB，线路也是走163线路。

3. <a href="https://bandwagonhost.com/" target="_blank">搬瓦工</a>
  知名的代理服务器提供商，优点是速度快，稳定，走CN2 GIA线路，目前最好的线路，没有之一，即使是高峰也是稳如狗。价格只有年付，49.9美金。
  
  总结，如果只是日常Google搜索，上推特，telegram，看视频要求不高的话，推荐选1, 2; 如果土豪，想稳定，要求速度的话，推荐选搬瓦工。搬瓦工还提供了自建的机场-Just my socks，只需要付费，会提供4个
  shadowsocks节点，并且节点被封会自动更换IP，如果不想折腾，推荐选这个。
 
 #### 以上可以自行搜索并购买服务器，选择vps关键词，不要选host之类的，在此不再赘述。
 
 ## 2. 下面以Virmatch为例，带领大家手把手建立shadowsocks服务。在此先通过Xshell连接你的远程服务器。
  ### 以下是virmatch控制面板提供的信息，其中ip是地址，用户名为root, 密码为 Root/Admin Password
  ![image](https://github.com/LJJ1994/shadowsocks_service/raw/master/images/test04.png)
  
  ### 以下是xshell登录设置，由于一些原因（GFW, 墙），通过ssh登录远程服务器速度会很慢，请耐心等待，或者重新开启新的窗口登录。
  ![image](https://github.com/LJJ1994/shadowsocks_service/raw/master/images/test03.png)
  
  ### 然后xshell会提示你输入账号和密码，分别输入root和你的密码即可。
  
 ## 3. 获取shadowsocks脚本，并开始构建服务, 这里使用了秋水逸冰的脚本。复制以下代码
   ```
   wget --no-check-certificate -O shadowsocks-all.sh https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks-all.sh
   chmod +x shadowsocks-all.sh
   ./shadowsocks-all.sh 2>&1 | tee shadowsocks-all.log
   ```
   然后回车开始......
  
  以下是安装的脚本提示，安装脚本提示输入相应的文字即可。
  
  #### 1. 选择哪个版本的shadowsocks, 由于shadowsocks由各种语言构建，但是目前还在维护的且稳定的是shadowsocks-libev, 选择 4
   ![image](https://github.com/LJJ1994/shadowsocks_service/raw/master/images/test05.png)
  
  #### 2. 输入你自己的密码，直接回车是默认密码
   ![image](https://github.com/LJJ1994/shadowsocks_service/raw/master/images/test06.png)
    
  #### 3. 选择端口，默认即可，注意：不要选择一些服务器的默认端口，比如22端口是SSH协议的默认端口，是要通过xshell类似的远程连接工具连接的，还有http的80，https的443端口
   ![image](https://github.com/LJJ1994/shadowsocks_service/raw/master/images/test07.png)
    
  #### 4. 选择shadowsocks的加密协议，目前我一直用的协议是aes-256-gcm协议，稳定。回车默认即可
   ![image](https://github.com/LJJ1994/shadowsocks_service/raw/master/images/test08.png)
    
  #### 5. 选择协议混淆，我一直使用混淆，比较稳定，由于地区的原因，使用混淆不一定起效果，如果使用了混淆还翻不了墙，可以选择不用。这里输入y, 然后回车
   ![image](https://github.com/LJJ1994/shadowsocks_service/raw/master/images/test09.png)
    
  #### 6. 如果选择了混淆，那么会选择哪种方式，是http还是tls（一种安全套接字，可以给http加上一层‘皮’，这样监听者就看不到你传输的数据包里的内容，如果是http，完全是裸露），这里输入2
   ![image](https://github.com/LJJ1994/shadowsocks_service/raw/master/images/test10.png)
    
  #### 然后会提示press any key to start之类的，直接回车开始安装，这里会出现一大堆安装信息，过程可能需要5~9分钟，请耐心等待，可以随机用鼠标点击xshell页面，防止连接中断
  #### 如果连接中断，那么需要重新用xshell连接服务器，重复上述过程，但是可能会遇到yum lock has hold之类的信息，那是因为之前的程序正在安装，所以请等待吧。
  
  
  #### 安装成功，会出现如下界面，这是你的shadowsocks配置信息。
   ![image](https://github.com/LJJ1994/shadowsocks_service/raw/master/images/success.jpg)
   
   
## 3. 这里还需要安装网络加速工具，可以让你的服务器更快的为你服务。复制以下代码
  ```
  wget -N --no-check-certificate "https://raw.githubusercontent.com/hijkpw/Linux-NetSpeed/master/tcp.sh" && chmod +x tcp.sh && ./tcp.sh
  ```
  #### 1. 然后直接回车，出现如下内容，有多款加速工具，还有魔改版的（笑），这里我选择BBR/BBR魔改版内核，输入 1，然后回车
  ![image](https://github.com/LJJ1994/shadowsocks_service/raw/master/images/test12.png)
  
  #### 2. 在一顿安装过后，会显示Complete! 字样，表示安装成功，需要重启服务器，输入Y回车。这里可能由于Linux版本不同会出现安装失败，为了不必要的麻烦，烦请选择CentOS7版本。
  ![image](https://github.com/LJJ1994/shadowsocks_service/raw/master/images/test13.png)
  
  #### 3. 重启后，输入 ```./tcp.sh```，然后回车
  ![image](https://github.com/LJJ1994/shadowsocks_service/raw/master/images/test15.png)
  
  
  #### 4. 出现如下字样，输入5，然后回车
  ![image](https://github.com/LJJ1994/shadowsocks_service/raw/master/images/test16.png)
  
  #### 5. 提示加速模块启动成功。
  ![image](https://github.com/LJJ1994/shadowsocks_service/raw/master/images/test17.png)
  
  #### 到此服务器的安装工具基本完成了，下来就是安装shadowsocks客户端，来连接服务器的shadowsocks，进行代理通信服务。
  
  
## 4. 在此以window10 为例，点击如下连接，然后下载箭头指向的assets, 这里版型选择4.1.10.0，注意：由于墙对Github的特殊感情（其实对于技术网站，基本都会被封禁掉，这也就是为啥你做开发，下载一个第三方包，会慢的要死的原因，因为这些东东不受审查，并且程序员容易开智，不容易被洗脑，所以这个群体很容易受到有关部门和墙的关照），所以打开GitHub可能会很慢，并且下载资源也会很慢

  <a href="https://github.com/shadowsocks/shadowsocks-windows/releases" target="_blank">shadowsocks window</a>
  
  ![image](https://github.com/LJJ1994/shadowsocks_service/raw/master/images/test20.png)
  
  #### 1. 然后在你的window10新建一个目录，将其解压到目录，目录路径不有中文（为什么不要有中文？因为这些软件是用英文开发的，一般使用的UTF8字符集，而中文一般是GBK开头的字符集，两个不同的字符集必然导致字符编码时造成混乱）。
  
  #### 2. 如果你使用了混淆，那么还需要一个混淆插件，点击如下连接，下载箭头的assets, 然后解压，将其放到你刚刚解压的 shadowsocks window 根目录。
  <a href="https://github.com/shadowsocks/simple-obfs/releases" target="_blank">obfs local</a>
  
  ![image](https://github.com/LJJ1994/shadowsocks_service/raw/master/images/test21.png)
  
  #### 3. 开始设置shadowsocks信息，安装刚刚在xshell安装成功后的信息如下填写就行。如果没来得急保存，在服务器下，输入 ` cat /etc/shadowsocks-libev/config.json ` 即可，会出现如下的配置信息。
  ```
  {
    "server":"0.0.0.0",
    "server_port":15762,
    "password":"teddysun.com",
    "timeout":300,
    "user":"nobody",
    "method":"aes-256-gcm",
    "fast_open":false,
    "nameserver":"1.0.0.1",
    "mode":"tcp_and_udp",
    "plugin":"obfs-server",
    "plugin_opts":"obfs=tls"
}
  ```
  **server** 服务器本地地址，在客户端输入你的真实IP地址  
  **server_port** 端口  
  **password** 密码  
  **method** 协议  
  **plugin** 混淆服务器插件  
  **obfs=tls** 混淆方式：tls  
  
  #### 这是客户端配置信息
  ![image](https://github.com/LJJ1994/shadowsocks_service/raw/master/images/test19.png)
  
  #### 这里的obfs是混淆插件，需要设置一些参数
   **插件程序** 固定写`obfs-local`  
   **插件选项** `obfs=tls;obfs-host=www.bing.com`, **tls**是你选择的混淆协议，**obfs-host**是访问某个网站（外网，可访问）来达到混淆墙的监测。  
   **需要命令行参数** 勾上  
   **插件参数** `obfs=tls` tls同理  
   **备注** 随意填写  
   **超时** 默认即可  
   
  #### 然后点击应用，确认。
  
  #### 右键你的shadowsocks客户端，鼠标点击系统代理，选择PAC模式。这里应该可以上网了。
  
  
## 5. 如果想让浏览器更加智能的上网，比如浏览国内网站不通过代理，浏览国外网站需要自动切换到代理，那么需要一款浏览器插件 SwitchyOmega. 通过如下连接查看教程使用
   
   #### <a href="https://github.com/FelisCatus/SwitchyOmega/wiki/GFWList" target="_blank">SwitchyOmega教程</a>
