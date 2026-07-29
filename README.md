# Android device tree for HONOR DUA-L22EEA (HWDUA-M)

```
#
# Copyright (C) 2026 The Android Open Source Project
# Copyright (C) 2026 SebaUbuntu's TWRP device tree generator
#
# SPDX-License-Identifier: Apache-2.0
#
```
# MUST READ!!! EXPLANATION BELOW OR IT WILL NOT BUILD!
Anyway that's the default readme file out of the way, this took a lot of trial and error to make sure it works and I will also try to give further instructions on how to compile a TWRP recovery for this device, just in case someone is crazy enough like me to build a custom recovery like it's 2018.

The device is technically not **huawei_HWDUA** but **honor_HWDUA-M**. However, since twrpdtgen detected it as a Huawei, I left is as is. The "-M" removal is because lunch gets confused by the "-M" and treats it like "-userdebug" or something which does not work and fails. Anyway, there are 6 files you will need to source from your own device because I am not sure if I am allowed to upload them

| Files in tree | Where to get | Explanation |
| --- | --- | --- |
| prebuilt/kernel | stock recovery ramdisk kernel | The kernel image can be found in the stock recovery's ramdisk (extract it with whatever tool works) |
| prebuilt/zImage | stock recovery ramdisk kernel | Same file, I don't know if it will build without it. Just in case. |
| recovery/root/init.recovery.huawei.rc | stock recovery ramdisk | I don't know if I can upload it. It's just text but I'd rather not risk getting sued. |
| recovery/root/init.recovery.mt6739.rc | stock recovery ramdisk | I don't know if I can upload it. It's just text but I'd rather not risk getting sued. |
| recovery/root/microtrust.rc | stock recovery ramdisk | I don't know if I can upload it. It's just text but I'd rather not risk getting sued. |
| recovery/root/ueventd.rc | stock recovery ramdisk | I don't know if I can upload it. It's just text but I'd rather not risk getting sued. |

# Building for TWRP Minimal Manifest 9.0
Stuff you will need:

| What | Where | Why |
| --- | --- | --- |
| Google's Repo Client | https://storage.googleapis.com/git-repo-downloads/repo | To download the source code |
| TWRP Minimal Manifest 9.0 Source | ??? | The source code |
| The device tree | ??? | Obviously |
| Ubuntu 18 | https://releases.ubuntu.com/18.04/ | To pretend it's 2018 and use old dependencies and software like openjdk-8 without compromising your main Linux system with old packages. Also, the compiler may not work with modern dependencies and to avoid that just use Ubuntu 18 |

Steps:
