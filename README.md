# mi-snisix

This is a small service that helps you make IPv6 only services available to IPv4 only users.


## How it works

You deploy as many IPv6 only services as you like and don't have to care about legacy IP.
In your DNS configuration you name the IPv4 Address of the SNI Proxy in addition to your usual quad-A record.

<img src="http://up.frubar.net/2997/sniproxy.svg">

The <a href="https://github.com/dlundquist/sniproxy">sniproxy</a> has IPv4 and IPv6 connectivity. It listens on port 80 and 443 on its IPv4 address.
For unencrypted HTTP traffic on port 80 it looks for the `Host:` header, for encrypted TLS traffic it uses the SNI details to lookup the intendet destination.

It then forwards the connection over IPv6.

Traffic is **not decrypted** and so sniproxy does **NOT** need the private key to your certificate.

This makes deployment of new services easy and secure: just setup the service on IPv6 and configure DNS accordingly. No changes, key material or configuration on the SNI Proxy is needed.

IPv6 users connect directly without the proxy.
