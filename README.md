# caddy-dyndns

Dynamic dns plugin for Caddy server (on this moment supports https://www.cloudflare.com/ , https://pdd.yandex.ru/, https://www.digitalocean.com/ and dnspod providers protocols).

Link in official caddyserver repository: https://caddyserver.com/docs/dyndns

Make this steps for compilation caddy with plugin caddy-dyndns:
- add directive in var section: "dyndns", //github.com/linkonoid/caddy-dyndns 
(in file github.com\mholt\caddy\caddyhttp\httpserver\plugin.go)
- add in import section _ "github.com/linkonoid/caddy-dyndns" (in caddymain/run.go)
- add directives in Caddyfile

Use "dyndns" directives in your configuration Caddyfile:
```
dyndns {

	provider cloudflare
	
	ipaddress http://whatismyip.akamai.com/
	
 	auth *****af380b8d3 *****@*****.com
	
 	domains *****.com www.*****.com
	
 	period 30m
}
```

Description:

provider: cloudflare/yandex/digitalocean/dnspod - name dns provider

ipaddress: http-url/remote/local/xxx.xxx.xxx.xxx - get external IP from remote server (http://whatismyip.akamai.com/, http://ipv4.myexternalip.com/raw or other with body in RAW format)/get remote IP auto in local mode/ get local IP auto)/Hand your IP xxx.xxx.xxx.xxx

auth: AuthApikeyToken - authentification token and via space Email - email address (for yandex -  not present)

	For dnspod token: id,token
	If you use dnspod international edition, please set `Email` as `international@dnspod.com`,and see https://www.dnspod.com/docs/info.html#get-the-user-token to get user_token.

domains: name.tld - list of domains to update via space symbol  

period: XXs/XXm/XXh/XXd - time period ip update (s - seconds, m - minutes, h - hours, d - days)
