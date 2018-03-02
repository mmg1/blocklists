Blocklists
==========

Although Nefarious Laboratories prefers a *default deny* approach to security, we maintain blocklists for those who prefer a *default allow* policy. The included blacklists define corporations by [ASN](https://en.wikipedia.org/wiki/Autonomous_system_%28Internet%29), allowing administrators to block an entire IP range.

[Amazon](https://github.com/neflabs/blocklists/tree/master/corporations/amazon) `AS16509`  
[Apple](https://github.com/neflabs/blocklists/tree/master/corporations/apple) `AS714`  
[Facebook](https://github.com/neflabs/blocklists/tree/master/corporations/facebook) `AS32934`  
[Google](https://github.com/neflabs/blocklists/tree/master/corporations/google) `AS15169`  
[Microsoft](https://github.com/neflabs/blocklists/tree/master/corporations/microsoft) `AS8075`  

Note that these corporations operate hosting services, and blocking corporate IP [ranges](https://dnslytics.com/bgp/as32934) may prevent users and devices from accessing third-party domains which are unaffiliated with these corporations.

## IPTables Example Rules (for ASNs)

```
*filter
:INPUT ACCEPT [0:0]
:FORWARD ACCEPT [0:0]
:OUTPUT ACCEPT [0:0]
    
#Amazon
-A OUTPUT -s 8.18.145.0/24 -j DROP

#Apple
-A OUTPUT -s 17.0.0.0/21 -j DROP

#Facebook
-A OUTPUT -s 31.13.24.0/21 -j DROP

#Google
-A OUTPUT -s 8.8.4.0/24 -j DROP

#Microsoft
-A OUTPUT -s 13.64.0.0/11 -j DROP

COMMIT
```

## DNSmasq Example Rules (for Domains)

A dnsmasq configuration file `/etc/dnsmasq.conf` can block domains and their respective subdomains, while a hosts file `/etc/hosts` requires a complete listing of every subdomain.

```
# Blocking Cryptojacking Domains

address=/authedmine.com/0.0.0.0
address=/coinhive.com/0.0.0.0
address=/rocks.io/0.0.0.0
```

## Inferior Passwords

We recommend blocking all included passwords in every public-facing web application. The included passwords are at least 8 characters in length, as shorter passwords should be banned.
