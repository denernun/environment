
```
LoadModule proxy_module modules/mod_proxy.so
LoadModule proxy_http_module modules/mod_proxy_http.so
LoadModule proxy_http2_module modules/mod_proxy_http2.so
```

```
Listen 8080
<VirtualHost *:8080>
	SSLEngine on
    SSLCertificateFile localhost.crt
    SSLCertificateKeyFile localhost.key
    SSLCertificateChainFile chain.pem
	SSLProxyEngine on
	ProxyRequests On
	ProxyPreserveHost On	
	ProxyPass / http://localhost:3001/
	ProxyPassReverse / http://localhost:3001/
</VirtualHost>
```
