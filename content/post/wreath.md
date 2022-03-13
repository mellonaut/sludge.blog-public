+++
title = "Wreath - Network"
description = "You know"
tags = [
    "CTF",
    "ejpt",
]
date = "2022-02-05"
categories = [
    "Red Team",
    "pentesting",
    "reports",
]
image = "https://sludgeassets-sync.s3.us-east-1.amazonaws.com/assets/headers/wp2759865-satanic-symbols-wallpaper.gif"
weight = 3
+++

---

<b>
# 'The Marketplace'

Going after it again.

Running Gobuster with the wildcard switch and raft-small-directories-lowercase.txt
Running feroxbuster
Noticed in the scan that Gobuster resolved the IP to thomaswreath.thm. going there now in firefox/burp

Had to add the host name I found into the hosts file on windows. Wouldn’t work on linux, I thionk that Id need to directly VPN into the wreath net with the wsl distro itself to get the host name working there

me@thomaswreath.thm

Not seeing much else on the page itself. Going to go back to the terminal and the scans see what we can see. Maybe start a scan of the subnet just to see

Looking at 

10000/tcp open   http       MiniServ 1.890 (Webmin httpd)

https://github.com/squid22/Webmin_CVE-2019-15107


[![N|Solid](/wreath/wreath01.png)](https://sludge.one/wreath)

[![N|Solid](/wreath/wreath02.png)](https://sludge.one/wreath)


That worked swimmingly.

Now I need to escalate priv I guess. I need to start poking around for passwords keys or suid bits set. 

Well, found this private ssh key called  called reverse in the home dir:

```
-----BEGIN OPENSSH PRIVATE KEY-----
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
qmV8AF1zpgrMLGXDnZiG1Bhct3k=
-----END OPENSSH PRIVATE KEY-----
```



Why is it called reverse? Is this the private key for this server? How do I check?

This is anaconda-ks.cfg and has interesting bits for sure



```
sh-4.4# cat anaconda-ks.cfg
cat anaconda-ks.cfg
#version=RHEL8
ignoredisk --only-use=sda
autopart --type=lvm
# Partition clearing information
clearpart --none --initlabel
# Use graphical install
graphical
# Use CDROM installation media
cdrom
# Keyboard layouts
keyboard --vckeymap=gb --xlayouts='gb'
# System language
lang en_GB.UTF-8

# Network information
network  --bootproto=dhcp --device=ens33 --ipv6=auto --activate
network  --hostname=tm-prod-serv
repo --name="Minimal" --baseurl=file:///run/install/repo/Minimal
# Root password
rootpw --iscrypted $6$i9vT8tk3SoXXxK2P$HDIAwho9FOdd4QCecIJKwAwwh8Hwl.BdsbMOUAd3X/chSCvrmpfy.5lrLgnRVNq6/6g0PxK9VqSdy47/qKXad1
# Run the Setup Agent on first boot
firstboot --enable
# Do not configure the X Window System
skipx
# System services
services --disabled="chronyd"
# System timezone
timezone Europe/London --isUtc --nontp
user --name=twreath --password=$6$0my5n311RD7EiK3J$zVFV3WAPCm/dBxzz0a7uDwbQenLohKiunjlDonkqx1huhjmFYZe0RmCPsHmW3OnWYwf8RWPdXAdbtYpkJCReg. --iscrypted --gecos="Thomas Wreath"

%packages
@^server-product-environment
kexec-tools

%end

%addon com_redhat_kdump --enable --reserve-mb='auto'

%end

%anaconda
pwpolicy root --minlen=6 --minquality=1 --notstrict --nochanges --notempty
pwpolicy user --minlen=6 --minquality=1 --notstrict --nochanges --emptyok
pwpolicy luks --minlen=6 --minquality=1 --notstrict --nochanges --notempty
%end
```



Start with these two in the home dir of root later

Well, looking at that twreath as a username…tried tssh into that using the key, not working. 

[![N|Solid](/wreath/wreath03.png)](https://sludge.one/wreath)

[![N|Solid](/wreath/wreath04.png)](https://sludge.one/wreath)

We have root. We need to pivot. I cant find anything in the route table but this box does have a couple entries in the arp table. Need to figure out how to ssh into this. If I can ssh into this I can forward ports.

[![N|Solid](/wreath/wreath05.png)](https://sludge.one/wreath)

[![N|Solid](/wreath/wreath06.png)](https://sludge.one/wreath)

Used getent and the uids

[![N|Solid](/wreath/wreath07.png)](https://sludge.one/wreath)

Checking netstat.....

[![N|Solid](/wreath/wreath08.png)](https://sludge.one/wreath)

The other 91s are…other students I think. That .150 looking awfully sexy though. I think if I change permissions on the key and try ssh as twreath and port forward my way to that system…

Was fucking around, tried to just create a user and add to sudo and login…need a key…tried to gen one…nope. Trying with reverse key.. Its saying no, public key authentication. I need to figure out whats going on here. Maybe Ill go check the INE notes and see if something pops out in the labs or something

[![N|Solid](/wreath/wreath09.png)](https://sludge.one/wreath)

[![N|Solid](/wreath/wreath10.png)](https://sludge.one/wreath)

Tried to gen my own from the private key. Need a passphrase…going to use john to try and crack the passhrase on the ssh key

[![N|Solid](/wreath/wreath11.png)](https://sludge.one/wreath)

[![N|Solid](/wreath/wreath12.png)](https://sludge.one/wreath)

Got the hash, going to try it with darkweb 2017 top 1000 passwords…


[![N|Solid](/wreath/wreath13.png)](https://sludge.one/wreath)



[![N|Solid](/wreath/wreath14.png)](https://sludge.one/wreath)

```
user --name=twreath --password=$6$0my5n311RD7EiK3J$zVFV3WAPCm/dBxzz0a7uDwbQenLohKiunjlDonkqx1huhjmFYZe0RmCPsHmW3OnWYwf8RWPdXAdbtYpkJCReg. --iscrypted --gecos="Thomas Wreath"

rootpw --iscrypted $6$i9vT8tk3SoXXxK2P$HDIAwho9FOdd4QCecIJKwAwwh8Hwl.BdsbMOUAd3X/chSCvrmpfy.5lrLgnRVNq6/6g0PxK9VqSdy47/qKXad1
```

I need to dehash these and see what they can do for me

Man, I don’t know what Im doing with this lol.

Nc, exploit, webmin…nc, exploit, webmin…nc, exploit, webmin….

[![N|Solid](/wreath/wreath15.png)](https://sludge.one/wreath)

twreath:$6$0my5n311RD7EiK3J$zVFV3WAPCm/dBxzz0a7uDwbQenLohKiunjlDonkqx1huhjmFYZe0RmCPsHmW3OnWYwf8RWPdXAdbtYpkJCReg.::0:99999:7:::

root:$6$p7Uhs/4PjCdnlyVM$iiDskHhs9a50ITRk1Bq/b6bxZenu8Vt9UqgxKapMvHBePwv21WQhHSQjGDOqZkLr4OXJ/3g9OWHZihIShi5oh.:19043:0:99999:7:::

We're either using these fucking hashes or I'm going to replace them with one of mine so we can ssh our way through to .150.

The ending of these hashes is different. 

[![N|Solid](/wreath/wreath16.png)](https://sludge.one/wreath)

Saw something to try unshadowing them Im going to cat the passwd file

```
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
sync:x:5:0:sync:/sbin:/bin/sync
shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown
halt:x:7:0:halt:/sbin:/sbin/halt
mail:x:8:12:mail:/var/spool/mail:/sbin/nologin
operator:x:11:0:operator:/root:/sbin/nologin
games:x:12:100:games:/usr/games:/sbin/nologin
ftp:x:14:50:FTP User:/var/ftp:/sbin/nologin
nobody:x:65534:65534:Kernel Overflow User:/:/sbin/nologin
dbus:x:81:81:System message bus:/:/sbin/nologin
systemd-coredump:x:999:997:systemd Core Dumper:/:/sbin/nologin
systemd-resolve:x:193:193:systemd Resolver:/:/sbin/nologin
tss:x:59:59:Account used by the trousers package to sandbox the tcsd daemon:/dev/null:/sbin/nologin
polkitd:x:998:996:User for polkitd:/:/sbin/nologin
libstoragemgmt:x:997:995:daemon account for libstoragemgmt:/var/run/lsm:/sbin/nologin
cockpit-ws:x:996:993:User for cockpit web service:/nonexisting:/sbin/nologin
cockpit-wsinstance:x:995:992:User for cockpit-ws instances:/nonexisting:/sbin/nologin
sssd:x:994:990:User for sssd:/:/sbin/nologin
sshd:x:74:74:Privilege-separated SSH:/var/empty/sshd:/sbin/nologin
chrony:x:993:989::/var/lib/chrony:/sbin/nologin
rngd:x:992:988:Random Number Generator Daemon:/var/lib/rngd:/sbin/nologin
twreath:x:1000:1000:Thomas Wreath:/home/twreath:/bin/bash
unbound:x:991:987:Unbound DNS resolver:/etc/unbound:/sbin/nologin
apache:x:48:48:Apache:/usr/share/httpd:/sbin/nologin
nginx:x:990:986:Nginx web server:/var/lib/nginx:/sbin/nologin
mysql:x:27:27:MySQL Server:/var/lib/mysql:/sbin/nologin
deeznuts:x:1001:1001::/home/deeznuts:/bin/bash
```
And the shadow file

```
root:$6$p7Uhs/4PjCdnlyVM$iiDskHhs9a50ITRk1Bq/b6bxZenu8Vt9UqgxKapMvHBePwv21WQhHSQjGDOqZkLr4OXJ/3g9OWHZihIShi5oh.:19043:0:99999:7:::
bin:*:18358:0:99999:7:::
daemon:*:18358:0:99999:7:::
adm:*:18358:0:99999:7:::
lp:*:18358:0:99999:7:::
sync:*:18358:0:99999:7:::
shutdown:*:18358:0:99999:7:::
halt:*:18358:0:99999:7:::
mail:*:18358:0:99999:7:::
operator:*:18358:0:99999:7:::
games:*:18358:0:99999:7:::
ftp:*:18358:0:99999:7:::
nobody:*:18358:0:99999:7:::
dbus:!!:18573::::::
systemd-coredump:!!:18573::::::
systemd-resolve:!!:18573::::::
tss:!!:18573::::::
polkitd:!!:18573::::::
libstoragemgmt:!!:18573::::::
cockpit-ws:!!:18573::::::
cockpit-wsinstance:!!:18573::::::
sssd:!!:18573::::::
sshd:!!:18573::::::
chrony:!!:18573::::::
rngd:!!:18573::::::
twreath:$6$0my5n311RD7EiK3J$zVFV3WAPCm/dBxzz0a7uDwbQenLohKiunjlDonkqx1huhjmFYZe0RmCPsHmW3OnWYwf8RWPdXAdbtYpkJCReg.::0:99999:7:::
unbound:!!:18573::::::
apache:!!:18573::::::
nginx:!!:18573::::::
mysql:!!:18573::::::
deeznuts:!!:19043:0:99999:7:::
```

[![N|Solid](/wreath/wreath17.png)](https://sludge.one/wreath)

[![N|Solid](/wreath/wreath18.png)](https://sludge.one/wreath)

I went back to the TryHackme room for a hint, after sinking a whole day into this. It won't give me the answer, and I won't have this hint on gameday, but just to make sure I'm on track…get webmin pseudoshell, rev shell, stabilize shell… good point, I'll get a better shell when I go back…man, it looks like they're going with the root hash and the private key. Shit !

[![N|Solid](/wreath/wreath19.png)](https://sludge.one/wreath)

Could stand to read the banners once in a while, damn.