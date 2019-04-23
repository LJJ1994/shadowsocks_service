# Ununtu18-SS
# shawdowsocks

## 1.更新apt安装源

`sudo apt-get update`   
`sudo apt install shadowsocks`  

## 2.用vim配置json文件

`sudo apt install vim`  
`vim /etc/shadowsocks.json`

## 3.json文件内容


`{`  
`"server":"你的ip地址",`  
`"server_port":端口号,`  
`"local_port":1080,`  
`"password":"你的秘玛",`  
`"timeout":600,`  
`"method":"加密方式"`  
`}`  

## 4.terminal加载配置文件

`sslocal -c /etc/shadowsocks.json`

## 5.在本地设置sock代理

`HTTP----端口：8080`  
`Socks5主机----端口: 1080`  

DONE!  
