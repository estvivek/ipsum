![Logo](https://i.imgur.com/PyKLAe7.png)

[![License](https://img.shields.io/badge/license-Public_domain-red.svg)](https://wiki.creativecommons.org/wiki/Public_domain)

About
----

**IPsum** is a threat intelligence feed based on 30+ different publicly available [lists](https://github.com/stamparm/maltrail) of suspicious and/or malicious IP addresses. All lists are automatically retrieved and parsed on a daily (24h) basis and the final result is pushed to this repository. List is made of IP addresses together with a total number of (black)list occurrence (for each). Greater the number, lesser the chance of false positive detection and/or dropping in (inbound) monitored traffic. Also, list is sorted from most (problematic) to least occurent IP addresses.

As an example, to get a fresh and ready-to-deploy auto-ban list of "bad IPs" that appear on at least 3 (black)lists you can run:

```
curl --compressed https://raw.githubusercontent.com/stamparm/ipsum/master/ipsum.txt 2>/dev/null | grep -v "#" | grep -v -E "\s[1-2]$" | cut -f 1
```

If you want to try it with `ipset`, you can do the following:

```
sudo su
apt-get -qq install iptables ipset
ipset -q flush ipsum
ipset -q create ipsum hash:net
for ip in $(curl --compressed https://raw.githubusercontent.com/stamparm/ipsum/master/ipsum.txt 2>/dev/null | grep -v "#" | grep -v -E "\s[1-2]$" | cut -f 1); do ipset add ipsum $ip; done
iptables -I INPUT -m set --match-set ipsum src -j DROP
```

In directory [levels](levels) you can find preprocessed raw IP lists based on number of blacklist occurrences (e.g. [levels/3.txt](levels/3.txt) holds IP addresses that can be found on 3 or more blacklists).

**Important:** If you are planning to use `git` to get the content of this repository do it like `git clone --depth 1 https://github.com/stamparm/ipsum.git`

Wall of shame (2019-02-12)
----

|IP|DNS lookup|Number of (black)lists|
|---|---|--:|
171.25.193.20|tor-exit0-readme.dfri.se|10
197.231.221.211|exit1.ipredator.se|10
178.73.215.171|178-73-215-171-static.glesys.net|9
171.25.193.25|tor-exit5-readme.dfri.se|9
171.25.193.77|tor-exit1-readme.dfri.se|9
158.69.254.114|ns548311.ip-158-69-254.net|9
80.82.77.139|dojo.census.shodan.io|9
58.210.156.141|-|9
185.244.25.167|-|9
80.82.77.33|sky.census.shodan.io|8
89.234.157.254|marylou.nos-oignons.net|8
171.25.193.235|tor-exit3-readme.dfri.se|8
144.132.10.218|cpe-144-132-10-218.rjui-cr-101.win.vic.bigpond.net.au|8
60.12.215.85|-|8
23.94.27.17|23-94-27-17-host.colocrossing.com|8
222.184.79.10|-|8
221.210.237.5|-|8
65.19.167.132|-|8
183.131.3.147|-|8
49.76.153.222|-|8
185.104.120.3|exit04.brasshorncomms.uk|8
121.11.75.190|-|8
87.236.212.222|-|8
139.59.94.9|-|8
199.87.154.255|tor.les.net|8
199.249.230.73|tor50.quintex.com|8
222.75.163.28|-|8
185.220.101.70|-|8
89.248.172.16|house.census.shodan.io|8
192.173.146.4|-|8
219.135.194.73|73.194.135.219.broad.gz.gd.dynamic.163data.com.cn|8
182.79.223.194|-|8
193.188.22.253|-|8
183.136.136.241|-|8
192.160.102.170|ogopogo.relay.coldhak.com|8
73.20.107.242|c-73-20-107-242.hsd1.ut.comcast.net|8
198.96.155.3|exit.tor.uwaterloo.ca|8
69.247.144.228|c-69-247-144-228.hsd1.tn.comcast.net|8
89.248.167.131|mason.census.shodan.io|8
211.144.1.142|-|8
185.142.236.34|-|8
111.186.56.129|-|8
58.210.156.132|-|8
43.225.180.30|-|8
46.172.247.140|-|8
192.241.141.208|sizuma.com|8
