OpenWrt 22.03 mips_4kec repository for dnsdist
========

To install the dnsdist package, run

```
echo "src/gz pdns https://repo.powerdns.com/openwrt/OpenWrt_22.03/mips_4kec/dnsdist" >> /etc/opkg/customfeeds.conf
opkg update
opkg install dnsdist # or dnsdist-full if you need all the features
```
