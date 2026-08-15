# AOSP x86_64 Cuttlefish

A reproducible development project for building and running an
AOSP x86_64 Cuttlefish Android virtual device.

## Current Target

- Android platform: Android 17
- Product: `aosp_cf_x86_64_only_phone`
- Release: `aosp_current`
- Build variant: `userdebug`
- Architecture: `x86_64`
- Build ID: `CP2A.260605.016`
- Virtual device: Cuttlefish

## Host Requirements

Recommended:

- Linux x86_64
- 32 GB RAM or more
- Hardware virtualization enabled
- KVM available
- Adequate SSD storage
- Git
- Repo
- AOSP build dependencies

The current development machine has 16 GB physical RAM and
encountered memory pressure during the Soong bootstrap stage.
A larger-memory build machine is therefore planned.

## AOSP Source

The AOSP source tree is maintained separately using Google's
`repo` tool.

The project repository does **not** contain the AOSP source tree.

Initialize the AOSP checkout with:

```bash
mkdir -p ~/AOSP
cd ~/AOSP

repo init --partial-clone \
  --no-use-superproject \
  -b android-latest-release \
  -u https://android.googlesource.com/platform/manifest

repo sync -c -j8
## Build Target

The configured build target is:

- Product: `aosp_cf_x86_64_only_phone`
- Release: `aosp_current`
- Variant: `userdebug`
- Architecture: `x86_64`

Build with:

    cd ~/AOSP
    source build/envsetup.sh
    lunch aosp_cf_x86_64_only_phone-aosp_current-userdebug
    m

Build parallelism should be adjusted according to available RAM.

## Project Goals

1. Reproduce the AOSP x86_64 Cuttlefish build.
2. Build a userdebug Android image.
3. Run and test the resulting virtual device.
4. Maintain project-specific configuration and scripts in this repository.
5. Support migration of the build environment to a larger cloud build machine.

## Repository Structure

AOSP-x86_64-Cuttlefish/
├── README.md
├── .gitignore
├── config/
├── docs/
├── patches/
├── scripts/
└── build/

## Status

Initial AOSP checkout completed.

Current build target configured successfully.

Initial build attempts reached the Soong bootstrap stage but were terminated because the host had approximately 15.3 GiB of usable RAM.

Next step: continue the build on a sufficiently provisioned machine.
