LLVM Obfuscator for Android NDK r23c

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
$ python toolchain/llvm_android/build.py // linux binary
$ python toolchain/llvm_android/build.py --no-build=linux // windows binary
```

## Apply to Android NDK r23c
1. download & extract [`android-ndk-r23c-windows`](https://dl.google.com/android/repository/android-ndk-r23c-windows.zip) or [`android-ndk-r23c-linux`](https://dl.google.com/android/repository/android-ndk-r23c-linux.zip)
2. copy `ollvm-ndk/out/[os]-install/bin/clang` to the NDK directory `/toolchains/llvm/prebuilt/[os]/bin/`


## Apply to Visual Studio
1. cd C:/Microsoft/AndroidNDK
2. rename the directory on `android-ndk-r[version]` to `android-ndk-r[version]_org`
3. download & extract [`android-ndk-r23c-windows`](https://dl.google.com/android/repository/android-ndk-r23c-windows.zip) and rename the directory `android-ndk-r23c` to `android-ndk-r[version]`
4. copy `ollvm-ndk/out/windows-x86-64-install/bin/clang` to the visual studio NDK directory `C:/Microsoft/AndroidNDK/android-ndk-r[version]/toolchains/llvm/prebuilt/windows-x86_64/bin/`
