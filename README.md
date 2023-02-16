# LLVM Obfuscator for Android NDK r23c

## How to download and build

Build is only available on Linux. (tested on Ubuntu 22.04.1 LTS)

```sh
$ sudo apt install repo
$ repo init -u https://android.googlesource.com/platform/manifest -b llvm-toolchain
$ cp manifest_8481493.xml .repo/manifests // Download xml from this repository
$ repo init -m manifest_8481493.xml
$ repo sync -c
```

copy & overwrite `/llvm` from this repository to `/toolchain/llvm-project/llvm`

```sh
$ curl -LO http://archive.ubuntu.com/ubuntu/pool/main/libf/libffi/libffi6_3.2.1-8_amd64.deb
$ sudo dpkg -i libffi6_3.2.1-8_amd64.deb
$ sudo apt-get install bison
$ python toolchain/llvm_android/build.py --no-build=windows --skip-package --skip-runtimes // linux binary
$ python toolchain/llvm_android/build.py --no-build=linux --skip-package --skip-runtimes // windows binary
```

## Apply to Android NDK r23c
1. download & extract [`android-ndk-r23c-windows`](https://dl.google.com/android/repository/android-ndk-r23c-windows.zip) or [`android-ndk-r23c-linux`](https://dl.google.com/android/repository/android-ndk-r23c-linux.zip)
2. copy `ollvm-ndk/out/stage2-install/bin/clang` to the NDK directory `/toolchains/llvm/prebuilt/[os]/bin/`

## Apply to Visual Studio
1. cd C:/Microsoft/AndroidNDK
2. rename the directory on `android-ndk-r[version]` to `android-ndk-r[version]_org`
3. download & extract [`android-ndk-r23c-windows`](https://dl.google.com/android/repository/android-ndk-r23c-windows.zip) and rename the directory `android-ndk-r23c` to `android-ndk-r[version]`
4. copy `ollvm-ndk/out/windows-x86-64-install/bin/clang` to the visual studio NDK directory `C:/Microsoft/AndroidNDK/android-ndk-r[version]/toolchains/llvm/prebuilt/windows-x86_64/bin/`

## Troubleshooting Ubuntu Build
"Unknown endianness of the compilation platform, check this header aes_encrypt.h"

It seems that the current system is not recognized. 

Open the `llvm/include/llvm/Transforms/Obfuscation/CryptoUtils.h`, delete lines 32 to 84 and add `#define ENDIAN_LITTLE`

## Compile option example
``-mllvm -sub -mllvm -sub_loop=1 -mllvm -fla -mllvm -split -mllvm -split_num=5 -mllvm -bcf -mllvm -bcf_loop=2 -mllvm -bcf_prob=100 -mllvm -sobf`` 
