

mod_reverseproxy engintron cpanel
================

mod_reverseproxy - reverse proxy module for Apache

Based on mod_remoteip.c and mod_cloudflare.c , this Apache module  will replace the  remote_ip  variable in user's logs with the correct remote IP sent from frontend web server like nginxcp, engintron and varnish.

To install
   ```bash
   wget https://raw.github.com/mcl21us/mod_reverseproxy/master/mod_reverseproxy.c
   apxs -i -c -n mod_reverseproxy.so mod_reverseproxy.c  
   ```
## Configuration Directives ##
```bash
ReverseProxyEnable           (On|Off)          - Enable reverse proxy

ReverseProxyRemoteIPHeader   X-Real-IP         - The header to use for the real IP
                                                 address.
ReverseProxyRemoteIPTrusted  127.0.0.1         -  What IPs to adjust requests for
```

## Example Configuration ##
WHM --> Apache Configuration --> Include Editor (OPEN Pre Main Include and add the ff line  add your server IP's after ReverseProxyRemoteIPTrusted xxx.xxx.xxx.xxx)
```bash

LoadModule reverseproxy_module modules/mod_reverseproxy.so

<IfModule reverseproxy_module>
  ReverseProxyEnable  On
  ReverseProxyRemoteIPHeader X-Real-IP
  ReverseProxyRemoteIPTrusted 127.0.0.1
  ReverseProxyRemoteIPTrusted 46.xxx.xxx.192
  ReverseProxyRemoteIPTrusted (Server IP's)
</IfModule>

```


NOTES:

- If mod\_cloudflare or mod\_remoteip are already loaded on the same web server, the web server will crash because both modules try to set the remote IP to a different value.
