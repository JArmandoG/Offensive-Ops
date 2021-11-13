# Reconnaissance-Methodology

---

Check out: Lazy Recon, Nuclei

Also Red Teaming Toolkit

# GENERAL ENGAGEMENT

- Rules: Understand the scope
- Use a cloud env -> Bandwidth: AWS/Digital Ocean

---

### Tools

- INFRA:
    - Cloud env -> Bandwidth / ISP problems: AWS/DO
        - DO ~0.35 USD / hr (~$60 mxn / 8hr && ~250USD/Mo)
        32GB/8vCPUs/6TB-bandwidth/100GB-SSD
    - Tools:
    Dump lists of tools to automate a bash script & Install stuff (apt install & git clone)
- CERTIFICADOS DIGITALES, DOMINIOS:
[crt.sh](http://crt.sh/) -> `https://crt.sh/?q=target.domain&output=json`
(Se puede parsear pero hay que extraer el json raw)
censys -> certificados digitales
- [dnsdumpster](https://dnsdumpster.com/)
Shodan
- SCANNING:
Funnel scanning:
    - masscan (Spray mass IP scan)
    - nmap (Focused scan) (Usar Rustscan o threader3000)
- SUBDOMAIN ENNUM:
    - webscreenshot,
    - [Photon](https://github.com/s0md3v/Photon) (Subdomain ennum, internal links, keys, etc.)
    - metasploit
    - sublist3r
    - Nahamsec's [Lazyrecon](https://github.com/nahamsec/lazyrecon)
    - Tib3rius' [autorecon](https://github.com/Tib3rius/AutoRecon)
    - ffuf - [codingo tutorial](https://www.youtube.com/watch?v=iLFkxAmwXF0)

### METHODOLOGY

- Get URL/IP
- With IP -> Masscan

```
sudo dir/masscan -iL cidr.txt -p 0-65535 --rate 100000 -n -Pn -oG greppable_result.txt
```

### HTTP/S webscreenshot:

1. Extract IP addresses (1 outfile for every port)
    
    Filter results for port 80, 443, 8080, etc. (Only extract IP addresses that have p. 80 open) > http_ips.txt, https_ips.txt, etc.
    
    Filter for not_http_ips.txt
    
2. Run webscreenshot:

Dependencies: `sudo apt install phantomjs`

```
xvfb-run webscreenshot --no-xserver --renderer-binary $(which phantomjs) -s -r phantomjs -i https_ips.txt -p 80 -o mytarget_screenshots_80

```

- s -> SSL certs. Si no, falla con http

### SHODAN

- Query: `org:"Equifax"` + -port:443 -port:80

# Web Scanners

Geekflare: Several security testing tools (Wordpress scans, TLS, etc.)

[](https://gf.dev/)

Net tools (Anonymous)

[Free online network tools - traceroute, nslookup, dig, whois lookup, ping - IPv6](https://centralops.net/co/)

# Quick Recons + OSINT

[External Recon Methodology](https://book.hacktricks.xyz/external-recon-methodology)

Recon methods (Good to follow)

[Google Hacking - Free Google Dorks for Recon](https://pentest-tools.com/information-gathering/google-hacking#)

Google Dorking Automático

[Investigator](https://abhijithb200.github.io/investigator/)

*Auto scraping, auto Dorking,*

[Website Analysis of blacktrust.net - Threat Intelligence Platform](https://threatintelligenceplatform.com/report/blacktrust.net/E8jfKOEzx5)

Quick Recon

[Threat Crowd | Threatcrowd.org Open Source Threat Intelligence](https://www.threatcrowd.org/)

📍 Central Recon

[IPv4Info - 209.182.202.96 ip address information.](http://ipv4info.com/ip-address/s31aa61/209.182.202.96.html/grupopicacho.com.mx/#_)

IPV4 Info (ASN, propietario, etc.)

[](https://spyse.com/search?target=domain&query=blacktrust.net)

*Domain, org, IP, AS, etc. fingerprinting*

[Host: 104.22.36.154](https://www.threatminer.org/host.php?q=104.22.36.154#gsc.tab=0&gsc.q=104.22.36.154&gsc.page=1)

Another central | OTX, etc.

[](https://dnsdumpster.com/)

DNS DUMPSTER (GOOD)

[Threat Intelligence - Pulsedive](https://pulsedive.com/indicator/?ioc=YmxhY2t0cnVzdC5uZXQ=)

Haven't tested it

[ImmuniWeb® - Web and Mobile Security Testing, Application Penetration Testing, Security Ratings](https://www.immuniweb.com/)

SSL TEST (BUENO, MEJOR QUE QUALYS Y CLI TOOL)

## WAF Bypassing & Info

[Uncovering CloudFlare](https://book.hacktricks.xyz/pentesting/pentesting-web/uncovering-cloudflare)

## General Recon

```bash
theHarvester -d bkbn.mx -b otx | httprobe | sed 's/.*:\/\///' | nslookup | grep 'name =' | awk '{print $NF}'
```

```bash
Recon-ng 
```

```bash
theHarvester -d [domain.co](http://domain.co) -l 500 -b otx 
```

```python
arjun -u api-endpoint.example.com
```

## Subdomain-takeover

[A Guide To Subdomain Takeovers](https://www.hackerone.com/application-security/guide-subdomain-takeovers)

[The Bug Hunter's Methodology Full 2-hour Training by Jason Haddix](https://www.youtube.com/watch?v=uKWu6yhnhbQ)

~1:30 nuclei templates for subdomain takeover

[GitHub - EdOverflow/can-i-take-over-xyz: "Can I take over XYZ?" - a list of services and how to claim (sub)domains with dangling DNS records.](https://github.com/edoverflow/can-i-take-over-xyz)

## Intrigue Core + Amazon Elastic Search & Kibana

[Scaling up - Automated Attack Surface Discovery With Intrigue Core by @jcran #NahamCon2020](https://www.youtube.com/watch?v=I4i0aaD23-M)

docker installling for specific plugins, or complete docker installation 👍
