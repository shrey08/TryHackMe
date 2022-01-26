### CNAME of shop.website.thm
> $ nslookup --type=CNAME shop.wesite.thm
### Result:
Server: 127.0.0.53<br>
Address: 127.0.0.53#53<br>
<br>
Non-authoritative answer:<br>
shop.website.thm canonical name = shops.myshopify.com<br>
### Value of the TXT record of website.thm
> $ nslookup --type=TXT website.thm
### Result:
Server: 127.0.0.53<br>
Address: 127.0.0.53#53<br>
<br>
Non-authoritative answer:<br>
website.thm text = "THM{7012BBA60997F35A9516C2E16D2944FF}"<br>
### Numerical priority value for the MX record
> $ nslookup --type=MX website.thm
### Result:
Server: 127.0.0.53<br>
Address: 127.0.0.53#53<br>
<br>
Non-authoritative answer:<br>
website.thm mail exchanger = 30 alt4.aspmx.l.google.com<br>
### IP address for the A record of www.website.thm
> $ nslookup --type=A website.thm
### Result:
Server: 127.0.0.53<br>
Address: 127.0.0.53#53<br>
<br>
Non-authoritative answer:<br>
Name: website.thm<br>
Address: 10.10.10.10<br>
