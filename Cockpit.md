---  
share: true  
tag: public  
---  
# Cockpit  
  
## Settings  
ub-directory (https://example.com/cockpit/ 6)  
  
/etc/cockpit/cockpit.conf  
  
[WebService]  
Origins = https://example.com wss://example.com  
ProtocolHeader = X-Forwarded-Proto  
UrlRoot=/cockpit  
  
/etc/caddy/Caddyfile  
  
example.com {  
    reverse_proxy /cockpit/* localhost:9090 {  
        transport http {  
            tls_insecure_skip_verify  
        }  
    }  
}  
  
One thing to point out with the sub-directory approach is that the trailing slash is required by cockpit. If you would like Caddy to silently accept requests without the trailing slash, you can add this line to your Caddyfile:  
  
rewrite /cockpit /cockpit/  
  
Alternatively, you can configure Caddy to redirect clients to add the trailing slash:  
  
redir /cockpit /cockpit/  
