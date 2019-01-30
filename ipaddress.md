 - ipaddress 模块

> 导入模块: 
>> `import ipaddress`

> ip地址转换: 
>> ip<=>int 192.168.0.1<=>3232235521
>>> `ipaddress.IPv4Address('192.168.0.1')`
>>> `ipaddress.IPv4Address(3232235521)`

> 
>> byte=>ip b'\xC0\xA8\x00\x01'=>192.168.0.1
>>> `ipaddress.IPv4Address(b'\x\xA8\x00\x01')`

> 获取网络掩码和主机掩码：
>> ```interface = IPv4Address.IPv4Interface('192.168.0.1/24')
   netmask = interface.netmask
   hostmask = interface.hostmask```

> 对象分类：IPv4Addres,IPv4Network,IPv4Interface详细对象属性见帮助文档

 - 帮助文档链接

>     https://docs.python.org/3.5/library/ipaddress.html?highlight=ip#module-ipaddress
