OpenWrt 23.05 mips64_octeonplus repository for dnsdist
========

To install the dnsdist package, run

```
echo "src/gz pdns https://repo.powerdns.com/openwrt/OpenWrt_23.05/mips64_octeonplus/dnsdist" >> /etc/opkg/customfeeds.conf
opkg update
opkg install dnsdist # or dnsdist-full if you need all the features
```
