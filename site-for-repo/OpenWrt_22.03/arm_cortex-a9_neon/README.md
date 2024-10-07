OpenWrt 22.03 arm_cortex-a9_neon repository for dnsdist
========

To install the dnsdist package, run

```
echo "src/gz pdns https://repo.powerdns.com/openwrt/OpenWrt_22.03/arm_cortex-a9_neon/dnsdist" >> /etc/opkg/customfeeds.conf
opkg update
opkg install dnsdist # or dnsdist-full if you need all the features
```
