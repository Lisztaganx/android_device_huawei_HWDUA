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

The device is technically not **huawei_HWDUA** but **honor_HWDUA-M**. However, since [twrpdtgen](https://github.com/twrpdtgen/twrpdtgen) detected it as a Huawei, I left is as is. The "-M" removal is because lunch gets confused by the "-M" and treats it like "-userdebug" or something which does not work and fails.

Anyway, there are 6 files listed here that you will need to source from your own device because I am not sure if I am allowed to upload them:

| File in tree | Where to get | Explanation |
| --- | --- | --- |
| prebuilt/kernel | stock recovery ramdisk kernel | The kernel image can be found in the stock recovery's ramdisk (extract it with whatever tool works) |
| prebuilt/zImage | stock recovery ramdisk kernel | Same file, I don't know if it will build without it. Just in case. |
| recovery/root/init.recovery.huawei.rc | stock recovery ramdisk | I don't know if I can upload it. It's just text but I'd rather not risk getting sued. |
| recovery/root/init.recovery.mt6739.rc | stock recovery ramdisk | I don't know if I can upload it. It's just text but I'd rather not risk getting sued. |
| recovery/root/microtrust.rc | stock recovery ramdisk | I don't know if I can upload it. It's just text but I'd rather not risk getting sued. |
| recovery/root/ueventd.rc | stock recovery ramdisk | I don't know if I can upload it. It's just text but I'd rather not risk getting sued. |

Those files exist in this repository but they are just placeholder text so you can replace them.

# Building for TWRP Minimal Manifest 9.0
Stuff you will need:

| What | Where | Why |
| --- | --- | --- |
| Google's Repo Client | https://storage.googleapis.com/git-repo-downloads/repo | To download the source code |
| TWRP Minimal Manifest 9.0 Source | ??? | The source code |
| The device tree | ??? | Obviously |
| Ubuntu 18 | https://releases.ubuntu.com/18.04/ | To pretend it's 2018 and use old dependencies and software like openjdk-8 without compromising your main Linux system with old packages. Also, the compiler may not work with modern dependencies and to avoid that just use Ubuntu 18 |

# Steps:

1. Set up an Ubuntu 18 VM with the VM software of your choice and give it enough storage and RAM.
2. Set up Google's Repo tool
3. Create a directory where you want the TWRP Minimal Manifest 9.0 Source Code and cd to it.
4. Use `repo init` to clone source code
5. Use `repo sync` to download the source code. (Use arguments -j1 to improve perfomance in some cases and --force-sync to fix stuff sometimes)
6. After the source code is downloaded, clone the device tree into the respective device/huawei/HWDUA directory. (For example, Android.mk should be in twrp_repo/device/huawei/HWDUA/Android.mk)
7. Acquire (from your device) and replace the files I did not provide in the respective device tree directory (see above, first table).
8. Run lunch and select the omni userdebug option because that one actually compiles. If it complains, it may be fine, just ignore it.
9. Now here's the actual fun part. If everything is supposed to be working, run `mka recoveryimage -j$(nproc)` and wait. Watch out for errors if compiling for the first time because you might still need to install some dependencies like `openjdk-8-dev` or `m4`. Ignore warnings.
10. At the end, you should have a recovery.img somewhere in the output/ folder so take that and do what you want with it.
