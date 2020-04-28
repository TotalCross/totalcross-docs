---
description: Learn the steps to generate your custom VM.
---

# How to build TotalCross VM \(WIP\)

After cloning the project you will have:

{% hint style="success" %}
To clone the project use the command:  
`git clone https://github.com/TotalCross/totalcross.git TotalCross`
{% endhint %}

```text
TotalCross/
├─ LitebaseSDK/
├─ TotalCrossSDK/
└─ TotalCrossVM/
```

You will need to enter inside `TotalCrossVM/builders` folder, please:

```text
$ cd TotalCrossVM/builders
```

Your folder structure will be something like this:

```text
TotalCross
├─ LitebaseSDK
├─ TotalCrossSDK
└─ TotalCrossVM
     ├─ builders/
     │    ├─ droid/
     │    ├─ gcc-linux-arm/
     │    ├─ gcc-posix/
     │    ├─ vc2008/
     │    ├─ vc2013/
     │    ├─ vc2017/
     │    ├─ xcode/
     │    └─ build.xml
     ├─ deps/
     └─ src/
```

## Linux x86-64

Enter into `gcc-posix` folder:

```text
~TotalCrossVM/builders$ cd gcc-posix
```

First, let's build the docker image:

```text
~TotalCrossVM/builders/gcc-posix$ cd docker
~TotalCrossVM/builders/gcc-posix/docker$ ./build.sh
```

If you have no problems you should check the image:

```text
~TotalCrossVM/builders/gcc-posix/docker$ docker images
REPOSITORY                              TAG                 IMAGE ID            CREATED             SIZE
totalcross/amd64-cross-compile          bionic              cd8fb68f0fc6        a minute ago        1.03GB
<none>                                  <none>              1a0e943d6239        27 hours ago        464MB
.
.
.
~TotalCrossVM/builders/gcc-posix/docker$ cd ..
```

Next, let's build `libtcvm.so`:

```text
~TotalCrossVM/builders/gcc-posix$ cd tcvm
~TotalCrossVM/builders/gcc-posix/tcvm$ ./build.sh
```

If you don't have any build errors, your folder will be something like this:

```text
TotalCross
├─ LitebaseSDK
├─ TotalCrossSDK
└─ TotalCrossVM
     ├─ builders/
     │    ├─ droid/
     │    ├─ gcc-linux-arm/
     │    ├─ gcc-posix/
     │    │    ├─ docker
     │    │    ├─ launcher
     │    │    └─ tcvm
     │    │         ├─ bin/
     │    │         │    └─ libtcvm.so
     │    │         ├─ build.sh
     │    │         ├─ libskia.a
     │    │         └─ Makefile
     │    ├─ vc2008/
     │    ├─ vc2013/
     │    ├─ vc2017/
     │    ├─ xcode/
     │    └─ build.xml
     ├─ deps/
     └─ src/
```

Look to the `bin` folder, now you just need to copy `libtcvm.so` to your valid SDK folder

```text
~TotalCrossVM/builders/gcc-posix/tcvm$ cp bin/libtcvm.so $PATH_TO_VALID_SDK/dist/vm/linux
```

## Linux ARM

Enter into `gcc-linux-arm` folder:

```text
~TotalCrossVM/builders$ cd gcc-linux-arm
```

First, let's build the docker image:

```text
~TotalCrossVM/builders/gcc-linux-arm$ cd docker-builder-image
~TotalCrossVM/builders/gcc-linux-arm/docker-builder-image$ ./build.sh
```

If you have no problems you should check the image:

```text
~TotalCrossVM/builders/gcc-posix/docker$ docker images
REPOSITORY                              TAG                 IMAGE ID            CREATED             SIZE
totalcross/totalcross/cross-compile     latest              cd8fb68f0fc6        a minute ago        1.03GB
<none>                                  <none>              1a0eea5a6dv0        15 hours ago        1.46GB
.
.
.
~TotalCrossVM/builders/gcc-linux-arm/docker-builder-image$ cd ..
```

TotalCross Linux ARM VM needs SDL2 statically linked, please:

```text
~TotalCrossVM/builders/gcc-linux-arm$ cd sdl
~TotalCrossVM/builders/gcc-linux-arm/sdl$ ./build.sh
```

If you have no errors:

```text
~TotalCrossVM/builders/gcc-linux-arm/sdl$ cd ..
```

Next, let's build `libtcvm.so`:

```text
~TotalCrossVM/builders/gcc-linux-arm$ cd tcvm
~TotalCrossVM/builders/gcc-linux-arm/tcvm$ ./build.sh
```

If you don't have any build errors, your folder will be something like this:

```text
TotalCross
├─ LitebaseSDK
├─ TotalCrossSDK
└─ TotalCrossVM
     ├─ builders/
     │    ├─ droid/
     │    ├─ gcc-linux-arm/
     │    │    ├─ docker-builder-image
     │    │    ├─ launcher
     │    │    ├─ sdl
     │    │    └─ tcvm
     │    │         ├─ bin/
     │    │         │    └─ libtcvm.so
     │    │         ├─ build.sh
     │    │         ├─ libskia.a
     │    │         └─ Makefile
     │    ├─ gcc-posix/
     │    ├─ vc2008/
     │    ├─ vc2013/
     │    ├─ vc2017/
     │    ├─ xcode/
     │    └─ build.xml
     ├─ deps/
     └─ src/
```

Look to the `bin` folder, now you just need to copy `libtcvm.so` to your valid SDK folder

```text
~TotalCrossVM/builders/gcc-linux-arm/tcvm$ cp bin/libtcvm.so $PATH_TO_VALID_SDK/dist/vm/linux_ar
```

