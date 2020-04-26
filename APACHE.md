## APACHE
**Linux**
```text
LoadModule proxy_module modules/mod_proxy.so
LoadModule proxy_http_module modules/mod_proxy_http.so
LoadModule proxy_http2_module modules/mod_proxy_http2.so
LoadModule socache_shmcb_module modules/mod_socache_shmcb.so
```
```text
<IfModule ssl_module>
SSLRandomSeed startup builtin
SSLRandomSeed connect builtin
SSLSessionCache "shmcb:c:/apache/logs/ssl_scache(512000)"
</IfModule>
```
```text
Listen 8080
<VirtualHost *:8080>
    SSLEngine on
    SSLProxyEngine on
    SSLCertificateFile localhost.crt
    SSLCertificateKeyFile localhost.key
    #SSLCertificateChainFile chain.pem
    ProxyRequests On
    ProxyPreserveHost On	
    ProxyPass / http://localhost:3001/
    ProxyPassReverse / http://localhost:3001/
</VirtualHost>
```
