# 局域网中的Windows与WSL
## windows下 使用

1. 查看本机所有监听端口和对应进程号

```pwsh
netstat -ano
```

2. 查看局域网内对应IP的网卡信息和计算机名称
```pwsh
nbtstat -A IP
```

3. 使用WSL的nmap工具查看局域网内IP电脑信息（会涉及到windows系统中文GBK编码显示的问题）：  

```bash
nmap --script nbstat IP 

# 提取并转换计算机名（GBK → UTF-8）正确在UTF-8终端显示为中文
echo -n "JK\xB7\xC0\xBF\xC6" |                                         
                               sed 's/\\x//g' |
                               xxd -r -p|
                               iconv -f GBK -t UTF-8
```