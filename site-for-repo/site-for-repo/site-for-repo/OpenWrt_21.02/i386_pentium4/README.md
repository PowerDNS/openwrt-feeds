OpenWrt 21.02 i386_pentium4 repository for dnsdist
========

To install the dnsdist package, run

```
echo "src/gz pdns https://repo.powerdns.com/openwrt/OpenWrt_21.02/i386_pentium4/dnsdist" >> /etc/opkg/customfeeds.conf
opkg update
opkg install dnsdist # or dnsdist-full if you need all the features
```
