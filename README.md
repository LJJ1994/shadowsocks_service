## 1. 在Centos7上构建属于你自己的Shadowsocks服务
首先你需要购买一台vps服务器，网上有很多vps厂商，比如vultr，virmatch, 搬瓦工等
1. vultr
  价格还可以，可以无限创建销毁服务器，如果服务器IP被墙的话，最低一个月2.5美金，只提供ipv6, 建议购买5美金的，线路走传统163线路，一般我会选择硅谷地区。
  
2. virmatch
  价格非常便宜，最低1.5美金，也就是不到10RMB，而且带宽大，有1GB，速率有1GB，线路也是走163线路。

3. 搬瓦工
  知名的代理服务器提供商，优点是速度快，稳定，走CN2 GIA线路，目前最好的线路，没有之一，即使是高峰也是稳如狗。价格只有年付，49.9美金。
  
  总结，如果只是日常Google搜索，上推特，telegram，看视频要求不高的话，推荐选1, 2; 如果土豪，想稳定，要求速度的话，推荐选搬瓦工。搬瓦工还提供了自建的机场-Just my socks，只需要付费，会提供4个shadowsocks节点，并且节点被封会自动更换IP，如果不想折腾，推荐选这个。
 
 ### 以上可以自行搜索并购买服务器，选择vps关键词，不要选host之类的，在此不再赘述。
 
 ## 2. 下面以Virmatch为例，带领大家手把手建立shadowsocks服务。在此先通过Xshell连接你的远程服务器。
  ### 以下是virmatch控制面板提供的信息，其中ip是地址，用户名为root, 密码为 Root/Admin Password
  ![image](https://github.com/LJJ1994/shadowsocks_service/raw/master/images/test04.png)
  
  ### 以下是xshell登录设置，由于一些原因（GFW, 墙），通过ssh登录远程服务器速度会很慢，请耐心等待，或者重新开启新的窗口登录。
  ![image](https://github.com/LJJ1994/shadowsocks_service/raw/master/images/test03.png)
  
  ### 然后xshell会提示你输入账号和密码，分别输入root和你的密码即可。
  
 ## 3. 获取shadowsocks脚本，并开始构建服务, 这里使用了秋水逸冰的脚本。
   ```
   wget --no-check-certificate -O shadowsocks-all.sh https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks-all.sh
   chmod +x shadowsocks-all.sh
   ./shadowsocks-all.sh 2>&1 | tee shadowsocks-all.log
   ```
   然后回车开始......
  
  以下是安装的脚本提示，安装脚本提示输入相应的文字即可。
  
  ### 1. 选择哪个版本的shadowsocks, 由于shadowsocks由各种语言构建，但是目前还在维护的且稳定的是shadowsocks-libev, 选择 4
   ![image](https://github.com/LJJ1994/shadowsocks_service/raw/master/images/test05.png)
  
  ### 2. 输入你自己的密码，直接回车是默认密码
   ![image](https://github.com/LJJ1994/shadowsocks_service/raw/master/images/test06.png)
    
  ### 3. 选择端口，默认即可，注意：不要选择一些服务器的默认端口，比如22端口是SSH协议的默认端口，是要通过xshell类似的远程连接工具连接的，还有http的80，https的443端口
   ![image](https://github.com/LJJ1994/shadowsocks_service/raw/master/images/test07.png)
    
  ### 4. 选择shadowsocks的加密协议，目前我一直用的协议是aes-256-gcm协议，稳定。回车默认即可
   ![image](https://github.com/LJJ1994/shadowsocks_service/raw/master/images/test08.png)
    
  ### 5. 选择协议混淆，我一直使用混淆，比较稳定，由于地区的原因，使用混淆不一定起效果，如果使用了混淆还翻不了墙，可以选择不用。这里输入y, 然后回车
   ![image](https://github.com/LJJ1994/shadowsocks_service/raw/master/images/test09.png)
    
  ### 6. 如果选择了混淆，那么会选择哪种方式，是http还是tls（一种安全套接字，可以给http加上一层‘皮’，这样监听者就看不到你传输的数据包里的内容，如果是http，完全是裸露），这里输入2
   ![image](https://github.com/LJJ1994/shadowsocks_service/raw/master/images/test10.png)
    
  ### 然后会提示press any key to start之类的，直接回车开始安装，这里会出现一大堆安装信息，过程可能需要5~9分钟，请耐心等待，可以随机用鼠标点击xshell页面，防止连接中断
  ### 如果连接中断，那么需要重新用xshell连接服务器，重复上述过程，但是可能会遇到yum lock has hold之类的信息，那是因为之前的程序正在安装，所以请等待吧。
  
  
  ### 安装成功，会出现如下界面，这是你的shadowsocks配置信息。
   ![image](https://github.com/LJJ1994/shadowsocks_service/raw/master/images/success.jpeg)
