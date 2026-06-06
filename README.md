# 🐧 Linux Kernel 3.18 — Moto G5 Plus (Potter) — Halium 9.0

> Patched Linux kernel for the Motorola Moto G5 Plus, adapted for **Halium 9.0**
> to support Ubuntu Touch bring-up.

[![Kernel Version](https://img.shields.io/badge/Kernel-3.18.140-blue?logo=linux)](https://kernel.org)
[![Halium](https://img.shields.io/badge/Halium-9.0-orange)](https://github.com/Halium/android)
[![Device](https://img.shields.io/badge/Device-Moto%20G5%20Plus-green)]()
[![Patches](https://img.shields.io/badge/Halium%20Config%20Patches-123-brightgreen)]()

---

## 📱 Device

| Field | Value |
|---|---|
| **Device** | Motorola Moto G5 Plus |
| **Codename** | `potter` |
| **SoC** | Qualcomm Snapdragon 625 (MSM8953) |
| **Architecture** | arm64 |
| **Kernel Base** | LineageOS 16.0 / Android 9 |

---

## 🌿 Branches

| Branch | Purpose |
|---|---|
| `master` | Upstream LineageOS 16.0 kernel (unmodified) |
| `halium-9.0` | **Patched for Halium 9.0** — use this for builds |

---

## 📋 What Changed in `halium-9.0`

**123 configuration changes** applied to `arch/arm64/configs/potter_defconfig`
to meet Halium 9.0 / Ubuntu Touch requirements:

| Category | Changes | Why Needed |
|---|---|---|
| **Control Groups (cgroups)** | 18 | systemd resource management |
| **Namespaces** | 9 | LXC container isolation |
| **Security (AppArmor/seccomp)** | 12 | Ubuntu Touch app security profiles |
| **Network filtering** | 31 | Container networking / iptables |
| **Filesystems (OverlayFS)** | 14 | Container image layers |
| **Scheduler** | 8 | Fair group scheduling for apps |
| **Misc** | 31 | Various Halium requirements |

Key configs enabled:
```
CONFIG_CGROUPS=y               # Control groups
CONFIG_NAMESPACES=y            # All namespace types
CONFIG_SECURITY_APPARMOR=y     # AppArmor
CONFIG_SECCOMP=y               # Secure computing mode
CONFIG_VETH=y                  # Virtual ethernet (container networking)
CONFIG_OVERLAY_FS=y            # OverlayFS
CONFIG_NET_NS=y                # Network namespaces
CONFIG_PID_NS=y                # PID namespaces
```

---

## 🛠️ Building

```bash
# From within the Halium workspace (see android_build_patches_potter)
source build/envsetup.sh
breakfast potter

# Build kernel only (fast)
mka halium-boot

# Output
ls out/target/product/potter/halium-boot.img
```

---

## ✅ Validation

Kernel config was validated using the official Halium checker:

```bash
bash check-kernel-config arch/arm64/configs/potter_defconfig
# All required configs: PASS
```

---

## 🔗 Related

| Repository | Description |
|---|---|
| [android_build_patches_potter](https://github.com/Nutricalboii/android_build_patches_potter) | Build patches, manifests, documentation |
| [Halium/android](https://github.com/Halium/android) | Halium 9.0 source manifest |

---

*Based on LineageOS kernel for MSM8953 — adapted for Halium 9.0 by [@Nutricalboii](https://github.com/Nutricalboii)*

<!-- updated documentation check 4195 -->
