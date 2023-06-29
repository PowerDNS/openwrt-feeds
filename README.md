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

<!-- 56 -->
