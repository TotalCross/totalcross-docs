# teste

After cloning the project \(`git clone https://github.com/TotalCross/totalcross.git TotalCross`\) you will have:

```text
TotalCross/
├─ LitebaseSDK/
├─ TotalCrossSDK/
└─ TotalCrossVM/
```

You will need to enter inside `TotalCrossSDK` folder, please:

```text
$ cd TotalCrossSDK
```

The next step you need to call _Gradle_:

```text
~/TotalCrossSDK$ ./gradlew dist
```

If you don't have any package errors, your folder will be something like this:

```text
TotalCross
├─ LitebaseSDK
├─ TotalCrossSDK
│    ├─ bin/
│    ├─ build/
│    ├─ dist/
│    │    ├─vm/
│    │    │    ├─ TCBase.tcz
│    │    │    ├─ TCFont.tcz
│    │    │    └─ TCUI.tcz
│    │    └─totalcross-sdk.jar
│    ├─ docs/
│    ├─ etc/
│    ├─ gradle/
│    ├─ src/
│    ├─ build.gradle
│    ├─ build.xml
│    ├─ gradlew
│    ├─ gradlew.bat
│    ├─ license.txt
│    └─ proguard.txt
└─ TotalCrossVM
```

Look to the `dist` folder, if you have the same files you just need to copy `dist` to your valid SDK folder

```text
~/TotalCrossSDK$ cp -r dist $PATH_TO_VALID_SDK/
```

