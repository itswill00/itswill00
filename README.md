<p align="center">
  <img src="https://img.shields.io/badge/will-android%20tinkerer-3DDC84?style=flat-square&logo=android&logoColor=white" />
  <img src="https://img.shields.io/badge/Surabaya-MT6789-ff6b35?style=flat-square" />
  <img src="https://img.shields.io/badge/focus-MediaTek%20boot%20%26%20ports-8E44AD?style=flat-square" />
</p>

<p align="center">
  <em>It's not about having, but about maintaining</em>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/python-3776AB?style=flat-square&logo=python&logoColor=white" />
  <img src="https://img.shields.io/badge/c-A8B9CC?style=flat-square&logo=c&logoColor=white" />
  <img src="https://img.shields.io/badge/shell-4EAA25?style=flat-square&logo=gnubash&logoColor=white" />
  <img src="https://img.shields.io/badge/java-007396?style=flat-square&logo=openjdk&logoColor=white" />
  <img src="https://img.shields.io/badge/kotlin-7F52FF?style=flat-square&logo=kotlin&logoColor=white" />
  <img src="https://img.shields.io/badge/sqlite-003B57?style=flat-square&logo=sqlite&logoColor=white" />
</p>

<p align="center">
  <img src="https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fapi.github.com%2Fusers%2Fitswill00&query=%24.public_repos&label=repos&color=24292f&style=flat-square" />
  <img src="https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fapi.github.com%2Fusers%2Fitswill00&query=%24.followers&label=followers&color=24292f&style=flat-square" />
  <img src="https://img.shields.io/github/stars/itswill00?affiliations=OWNER&label=stars&color=24292f&style=flat-square" />
</p>

---

## What I work on

Three Xiaomi phones, three different kinds of problem. On the Redmi Note 14 4G (`tanzanite`,
MT6789) Xiaomi never released the kernel source, so the pieces had to be recovered from firmware.
On the Redmi Note 8 (`ginkgo`, SM6125) the source is public, and the work is finding what the
existing ports silently get wrong. And on the same phone, running Apple's kernel instead of
Linux, the work is a hardware map that has never been written down.

The two ginkgo projects are deliberately one above the other: same board, same device tree, and
the second one exists because reading that tree carefully turned up facts the first one needed.

<table>
<tr>
<td width="50%" valign="top">

### [tanzanite-ubuntu-touch](https://github.com/itswill00/tanzanite-ubuntu-touch)
Ubuntu Touch 20.04 / Halium 12. Kernel from GKI 5.10 with AppArmor, 385 vendor modules recovered
from the `vendor_dlkm` partition, recovery installer with AVB handling.

<img src="https://img.shields.io/github/v/release/itswill00/tanzanite-ubuntu-touch?style=flat-square&label=release&color=77216F" />
<img src="https://img.shields.io/github/actions/workflow/status/itswill00/tanzanite-ubuntu-touch/validate.yml?branch=main&style=flat-square&label=validate" />
<img src="https://img.shields.io/badge/Halium-12-4E9A06?style=flat-square" />

</td>
<td width="50%" valign="top">

### [ginkgo-ubuntu-touch](https://github.com/itswill00/ginkgo-ubuntu-touch)
Ubuntu Touch 20.04 / Halium 10. Kernel 4.14 CAF NICOBAR built natively on aarch64. Found six
upstream overlay defects, including a fingerprint HAL that never started.

<img src="https://img.shields.io/github/v/release/itswill00/ginkgo-ubuntu-touch?style=flat-square&label=release&color=77216F" />
<img src="https://img.shields.io/github/actions/workflow/status/itswill00/ginkgo-ubuntu-touch/validate.yml?branch=main&style=flat-square&label=validate" />
<img src="https://img.shields.io/badge/Halium-10-4E9A06?style=flat-square" />

</td>
</tr>
<tr>
<td width="50%" valign="top">

### [android_kernel_xiaomi_tanzanite](https://github.com/itswill00/android_kernel_xiaomi_tanzanite)
Kernel bring-up by reverse engineering: GKI 5.10 configs, DTB, and the module layout the stock
firmware actually uses.

<img src="https://img.shields.io/badge/kernel-5.10%20GKI-333333?style=flat-square&logo=linux&logoColor=white" />
<img src="https://img.shields.io/badge/SoC-MT6789-8E44AD?style=flat-square" />

</td>
<td width="50%" valign="top">

### [kernelis](https://github.com/itswill00/kernelis)
Android root kernel and system manager. Kotlin, capability-based.

<img src="https://img.shields.io/badge/kotlin-7F52FF?style=flat-square&logo=kotlin&logoColor=white" />

</td>
</tr>
<tr>
<td width="50%" valign="top">

### [HyperDL](https://github.com/itswill00/HyperDL)
Minimalist media downloader module for rooted Android devices. Releases at
[HyperDL-Release](https://github.com/itswill00/HyperDL-Release).

<img src="https://img.shields.io/badge/python-3776AB?style=flat-square&logo=python&logoColor=white" />

</td>
<td width="50%" valign="top">

### [ios-ginkgo](https://github.com/itswill00/ios-ginkgo)
Apple's XNU kernel on the same Redmi Note 8. A hardware probe and an honest map of why this board
is harder than the ports that work: eMMC where every port expects UFS, and ARMv8.0 cores that
cannot use the 16 KB pages iOS is built for.

<img src="https://img.shields.io/github/v/release/itswill00/ios-ginkgo?style=flat-square&label=release&color=77216F" />
<img src="https://img.shields.io/github/license/itswill00/ios-ginkgo?style=flat-square&color=blue" />
<img src="https://img.shields.io/badge/status-probe%20only-critical?style=flat-square" />

</td>
</tr>
</table>

---

## Notes worth reading

From the tanzanite port, because the reasoning matters more than the result:

- **[Module audit](https://github.com/itswill00/tanzanite-ubuntu-touch/blob/main/docs/MODULE_AUDIT.md)** —
  audio, torch and camera were all broken by the same cause: 178 vendor modules that live on
  `vendor_dlkm` inside `super.img`, not in `vendor_boot` where the port was looking. Records two
  wrong assumptions and what disproved them.
- **[Bootloader and AVB](https://github.com/itswill00/tanzanite-ubuntu-touch/blob/main/docs/BOOTLOADER.md)** —
  why "you must flash fenrir/lkpatcher first" does not apply here: AVB in `vbmeta` is the mechanism
  that matters, and lkpatcher cannot patch this device (ARM32 patch set, AArch64 LK).
- **[Changelog](https://github.com/itswill00/tanzanite-ubuntu-touch/blob/main/CHANGELOG.md)** —
  written as cause and effect, not as a diff summary.
- **[Port landscape](https://github.com/itswill00/ginkgo-ubuntu-touch/blob/main/docs/PORT_LANDSCAPE.md)** —
  four Ubuntu Touch trees already exist for the Redmi Note 8 and all four are broken in different
  ways. Why this is a fifth rather than a fork, and what each one gets wrong.
- **[ginkgo build notes](https://github.com/itswill00/ginkgo-ubuntu-touch/blob/main/docs/BUILD_NOTES.md)** —
  the ARM32 compat vDSO is assembled by the wrong toolchain because a Makefile passes a directory
  where clang expects a prefix. One line, four hours.
- **[Hardware map](https://github.com/itswill00/ios-ginkgo/blob/ginkgo-port/devices/ginkgo/profile.py)** —
  every address the Redmi Note 8 needs to boot a non-Linux kernel, with the device tree node each
  one came from. Written as data with the reasoning attached, so a wrong value can be traced back
  to an artifact instead of an opinion.
- **[Observed vs guessed](https://github.com/itswill00/ios-ginkgo/blob/ginkgo-port/NOTES-ginkgo.md)** —
  the handoff separates what was read out of a device tree from what was inferred from position.
  Three of the six hardware facts in that port started as guesses, and saying so is what keeps the
  other three trustworthy.

---

<p align="center">
  <img src="https://github-profile-summary-cards.vercel.app/api/cards/profile-details?username=itswill00&theme=github_dark" />
</p>

<p align="center">
  <img src="https://github-profile-summary-cards.vercel.app/api/cards/repos-per-language?username=itswill00&theme=github_dark" />
  <img src="https://github-profile-summary-cards.vercel.app/api/cards/most-commit-language?username=itswill00&theme=github_dark" />
</p>

<p align="center">
  <img src="https://github-readme-streak-stats.herokuapp.com/?user=itswill00&theme=github-dark&hide_border=true" />
</p>
