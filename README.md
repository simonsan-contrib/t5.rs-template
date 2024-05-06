# t5.rs

[![Rust](https://img.shields.io/badge/Rust-f75208?style=for-the-badge&logo=rust&logoColor=white)](https://www.rust-lang.org/)
[![Dioxus](https://img.shields.io/badge/Dioxus-00a8d6?style=for-the-badge&logo=rust)](https://dioxuslabs.com/)
[![Warp](https://img.shields.io/badge/Warp-1a202c?style=for-the-badge&logo=rust&logoColor=white)](https://github.com/seanmonstar/warp)
[![Bun](https://img.shields.io/badge/Bun-14151a?style=for-the-badge&logoColor=fbf0df&logo=bun)](https://bun.sh/)
[![TailwindCSS](https://img.shields.io/badge/TailwindCSS-38b2ac?style=for-the-badge&logo=tailwind-css&logoColor=white)](https://tailwindcss.com/)

- Install cargo-watch using `cargo install cargo-watch`
- Install dependencies using `bun install`
- Watch and build TailwindCSS using `bun tailwind`

>All the below notes on various package versions and features are handled by the `bun web`, `bun android`, and `bun desktop` commands by copying the correct `Cargo.toml` file to the project root

## API

- Run API server using `bun api`

## Web

> To compile this you must switch on the "web" feature of the `dioxus` package and remove the "mobile" one.

> Works only without `openssl` installed with the `vendor` option in the `Cargo.toml`.

- Compile and run web app using `bun web`

## Desktop

> Works with `openssl` installed with the `vendor` option and also without it (builds significantly faster both on Windows and Linux).

- Compile and run desktop app using `bun desktop`

## Android

> Works only with `openssl` installed with the `vendor` option (requires `perl` of the UNIX flavour to build it).

You have to create a `.cargo/config.toml` file in your home directory or in the project folder with the following content:

```toml
[target.aarch64-linux-android]
linker = "/<absolute-path-to-home>/<path-to-sdk>/ndk/<ndk-version>/toolchains/llvm/prebuilt/linux-x86_64/bin/aarch64-linux-android<api-version>-clang"
```

Also you should setup all these environment variables in your terminal or in your `.bashrc` or `.zshrc` file:

```sh
export JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64
export ANDROID_HOME=$HOME/android
export ANDROID_SDK_ROOT=$ANDROID_HOME
export NDK_HOME=$ANDROID_HOME/ndk/26.3.11579264
export ANDROID_NDK_HOME=$NDK_HOME

export TOOLCHAIN=$ANDROID_NDK_HOME/toolchains/llvm/prebuilt/linux-x86_64

# These two variables depend on the architecture of the device and the API version you are targeting
export TARGET=aarch64-linux-android
export API=33

export AR=$TOOLCHAIN/bin/llvm-ar
export CC=$TOOLCHAIN/bin/$TARGET$API-clang
export AS=$CC
export CXX=$TOOLCHAIN/bin/$TARGET$API-clang++
export LD=$TOOLCHAIN/bin/ld
export RANLIB=$TOOLCHAIN/bin/llvm-ranlib
export STRIP=$TOOLCHAIN/bin/llvm-strip

export PATH=$JAVA_HOME/bin:$ANDROID_HOME/cmdline-tools/latest/bin:$TOOLCHAIN/bin:$NDK_HOME:$ANDROID_HOME/platform-tools:$ANDROID_HOME/tools:$ANDROID_HOME/tools/bin:$PATH
```

- Compile and run Android app using `bun android`
- Connect to the local API server using `adb reverse tcp:8000 tcp:8000`
