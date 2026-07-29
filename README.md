# Android device tree for HONOR DUA-L22EEA (HWDUA-M)

```
#
# Copyright (C) 2026 The Android Open Source Project
# Copyright (C) 2026 SebaUbuntu's TWRP device tree generator
#
# SPDX-License-Identifier: Apache-2.0
#
```
Anyway that's the default readme file out of the way, this took a lot of trial and error to make sure it works and I will also try to give further instructions on how to compile a TWRP recovery for this device.

The device is technically not **huawei_HWDUA** but **honor_HWDUA-M**. However, since twrpdtgen detected it as a Huawei, I left is as is. The "-M" removal is because lunch gets confused by the "-M" and treats it like "-userdebug" or something which does not work and fails. Anyway, there are 5 files you will need to source from your own device because I am not sure if I am allowed to upload them
