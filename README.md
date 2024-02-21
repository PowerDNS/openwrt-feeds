OpenWrt repository for dnsdist
========

Download the [signing key](public.key), add it to your device with `opkg-key add public.key`, and then select the version that matches your device (check `/etc/openwrt_release` or the LuCI status page):

* [OpenWrt 23.05](OpenWrt_23.05/)
* [OpenWrt 22.03](OpenWrt_22.03/)
* [OpenWrt 21.02](OpenWrt_21.02/)
* [Signing key](public.key)

These repositories offer two versions of dnsdist:

* `dnsdist`: `Enabled features: dns-over-tls(openssl) dns-over-https(DOH) outgoing-dns-over-https(nghttp2)`
* `dnsdist-full`: `Enabled features: cdb dns-over-tls(gnutls openssl) dns-over-https(DOH) dnscrypt ebpf fstrm ipcipher libeditr libsodium lmdb outgoing-dns-over-https(nghttp2) protobuf re2 snmp`

If you do [your own builds based on our package definition](https://github.com/PowerDNS/openwrt-feeds/tree/main/package) you can also build a version that is exactly right for your needs.

Installation instructions
-------------------------

Download and install the signing key:
```
root@OpenWrt:~# cd /tmp
root@OpenWrt:/tmp# wget https://repo.powerdns.com/openwrt/public.key
Downloading 'https://repo.powerdns.com/openwrt/public.key'
Connecting to 188.166.116.224:443
Writing to 'public.key'
public.key           100% |*******************************|   118   0:00:00 ETA
Download completed (118 bytes)
root@OpenWrt:/tmp# opkg-key add public.key
```

Then, pick your OpenWrt version above, followed by your architecture (see `opkg print-architecture` to find the right one).
Follow the instructions there (at least the `echo`), then continue reading here.

With the feed configured, three packages become available:

* `dnsdist`
* `dnsdist-full`
* `dnsdist-maindns`

See above for an explanation of `dnsdist` and `dnsdist-full`.

`dnsdist-maindns` is a meta package that configures dnsdist to replace dnsmasq.

Because `opkg` has limited conflict resolution, installation takes an extra step:

```
root@OpenWrt:~# opkg remove odhcpd-ipv6only
Removing package odhcpd-ipv6only from root...
root@OpenWrt:~# opkg install dnsdist-maindns
Installing dnsdist-maindns (1.8.0-pdns5) to root...
Downloading https://repo.powerdns.com/openwrt/OpenWrt_22.03/arm_cortex-a9_vfpv3-d16/dnsdist/dnsdist-maindns_1.8.0-pdns5_all.ipk
Installing odhcpd (2023-01-02-4a673e1c-2) to root...
Downloading https://downloads.openwrt.org/releases/22.03.2/packages/arm_cortex-a9_vfpv3-d16/base/odhcpd_2023-01-02-4a673e1c-2_arm_cortex-a9_vfpv3-d16.ipk
Configuring odhcpd.
odhcpd
Configuring dnsdist-maindns.

dnsmasq disabled, odhcpd set up, dnsdist enabled
Please reboot

root@OpenWrt:~# reboot
```

If, after reboot, DNS does not work, and `logread` shows a line like:

```
dnsdist[3112]: No downstream servers defined: all packets will get dropped
```

then make sure that whatever configures your WAN fills `/tmp/resolv.conf.d/resolv.conf.auto` correctly.
As a workaround until you debug that problem, you can do:

```
root@OpenWrt:~# echo nameserver 9.9.9.9 > /tmp/resolv.conf.d/resolv.conf.auto
root@OpenWrt:~# /etc/init.d/dnsdist restart
```

This workaround example uses Quad9's resolver (which dnsdist will auto-upgrade to DoT).
You can of course substitute your own preferred resolver.

<!-- 6 -->
