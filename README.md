# Android device tree for HONOR DUA-L22EEA (HWDUA-M)

```
#
# Copyright (C) 2026 The Android Open Source Project
# Copyright (C) 2026 SebaUbuntu's TWRP device tree generator
#
# SPDX-License-Identifier: Apache-2.0
#
```
Now that the default readme is out of the way...
# MUST READ!!! EXPLANATION BELOW OR IT WILL NOT BUILD!
This took a lot of trial and error to make sure it works and I will also try to give further instructions on how to compile a Team Win Recovery Project (`3.7.0_9-0`) custom recovery for this device, just in case someone is crazy enough like me to build a custom recovery like it's 2018.

The device is technically not **huawei_HWDUA** but **honor_HWDUA-M**. However, since [twrpdtgen](https://github.com/twrpdtgen/twrpdtgen) detected it as a Huawei, I left is as is. The `HWDUA-M` to `HWDUA` rename is because lunch gets confused by the `-M` and treats it like `-userdebug` or something which does not work and fails.

Anyway, there are 5 files listed here that you will need to source from your own device because I am not sure if I am allowed to upload them:

| File in tree | Where to get | Explanation |
| --- | --- | --- |
| `prebuilt/kernel` | stock recovery/kernel | The kernel image can be found in the extracted stock recovery's root folder (extract it with whatever tool works) |
| `recovery/root/init.recovery.huawei.rc` | stock recovery/ramdisk/init.recovery.huawei.rc | I don't know if I can upload it. It's just text but I'd rather not risk getting sued. |
| `recovery/root/init.recovery.mt6739.rc` | stock recovery/ramdisk/init.recovery.mt6739.rc | I don't know if I can upload it. It's just text but I'd rather not risk getting sued. |
| `recovery/root/microtrust.rc` | stock recovery/ramdisk/microtrust.rc | I don't know if I can upload it. It's just text but I'd rather not risk getting sued. |
| `recovery/root/ueventd.rc` | stock recovery/ramdisk/ueventd.rc | I don't know if I can upload it. It's just text but I'd rather not risk getting sued. |

These files do exist in this repository but they are just placeholder text so you must replace them.

# Building for TWRP Minimal Manifest 9.0
Stuff you will need:

| What | Where | Why |
| --- | --- | --- |
| Ubuntu 18 | https://releases.ubuntu.com/18.04/ | To pretend it's 2018 and use old dependencies and software like openjdk-8 without compromising your main Linux system with old packages. Also, the compiler may not work with modern dependencies and to avoid that just use Ubuntu 18 |
| The full device tree | This repository and replace the placeholder files | Obviously |
| Google's Repo Python script | https://storage.googleapis.com/git-repo-downloads/repo | To download the source code |

# Steps:

1. Set up an Ubuntu 18 VM with the VM software of your choice and give it enough storage and RAM. I had given it a 40GB disk image and 4GB of RAM and it worked but I cannot say for anyone else.
2. Set up Google's Repo Python script by running
```bash
curl -O https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
```
and
```bash
chmod +x ~/bin/repo
```
3. Create a directory where you want to download the TWRP Minimal Manifest 9.0 Source Code and `cd` to it.
4. Run
```bash
~/bin/repo init --depth=1 -u https://github.com/minimal-manifest-twrp/platform_manifest_twrp_omni.git -b twrp-9.0
```
to initiate the TWRP repository.

5. Run
```bash
~/bin/repo sync
```
to download the source code. (Use arguments `-j1` to improve perfomance in some cases and `--force-sync` to fix stuff sometimes)

6. After the source code is downloaded, clone the device tree into the respective device/huawei/HWDUA directory. (For example, `Android.mk` should be located in `twrp_repo/device/huawei/HWDUA/Android.mk`)
7. Acquire (from your device) the files which I did not provide and replace them accordingly in the respective device tree directory (see above, first table).
8. Run
```bash
. build/envsetup.sh
```
and then
```bash
lunch
```
9. Select the omni_HWDUA-userdebug option because that one actually compiles. If it complains, it may be fine, just ignore it.
10. Now here's the actual fun part. If everything is supposed to be working, run
```bash
mka recoveryimage -j$(nproc)
```
and wait. Watch out for errors if compiling for the first time because you might still need to install some dependencies like `openjdk-8-dev` or `m4`. Ignore warnings.

11. At the end, you should have a `recovery.img` file in `out/target/product/HWDUA/recovery.img` so take that and do what you want with it.


*"How do you build a custom recovery for an old device with a modern system?"*

*"We can't, we don't know how to do it."*
