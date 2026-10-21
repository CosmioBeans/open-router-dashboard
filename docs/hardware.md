# Hardware research

Updated October 20, 2026. These are available research devices, not the limits of project support. No device has been tested with project software.

| Device | Reported hardware | Reported firmware | Research status |
| --- | --- | --- | --- |
| GL.iNet Flint 2 | GL-MT6000 | Not yet provided | Upstream OpenWrt support documented; project validation pending. |
| TP-Link HB810 | HB810 v2.6 00000000 | 0.6.0 3.1.10 v6095.0 Build 260729 Rel.57027n | No confirmed upstream OpenWrt support found. Treat as unverified. |
| TP-Link Archer AX55 | Archer AX55 v1.0 | 1.5.11 Build 20251119 rel.49503(4341) | Upstream snapshot support reported for compatible switch variants; exact unit compatibility unverified. |

## Findings and limits

The [OpenWrt AX55 hardware record](https://openwrt.org/toh/hwdata/tp-link/tp-link_ax55_v1) lists snapshot support and an unsupported RTL8367S-VB switch variant. The v1.0 label and vendor firmware version do not establish which switch is present or prove that a migration method works with this installed firmware. Check the [device instructions](https://openwrt.org/toh/tp-link/archer_ax55_v1) before planning any installation. Indexed documentation was available; earlier direct retrieval hit an anti-bot challenge.

TP-Link describes the [HB810 family](https://service-provider.tp-link.com/uk/home-wifi-system/hb810/) as a Wi-Fi 7 mesh system. Searches did not establish an upstream OpenWrt device profile or supported image for the reported v2.6 unit. Absence of a search result is not proof that support is impossible. Region, chipset, boot process, and upstream development status remain research questions.

The [Flint 2 hardware record](https://openwrt.org/toh/hwdata/gl.inet/gl.inet_gl-mt6000) documents upstream support. Running vendor firmware and running upstream OpenWrt remain distinct installation environments.

Capability detection applies once a compatible software environment is running; it cannot supply missing boot support or drivers. Never select a firmware image solely from a similar product name.
