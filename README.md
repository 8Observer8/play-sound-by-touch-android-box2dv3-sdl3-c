The sound file was taken here: https://opengameart.org/content/picked-coin-echo-2

Based on the info: https://gist.github.com/madebr/3563a41ec9d287b6754c5fe764f56a1c?permalink_comment_id=5776785#gistcomment-5776785

- Download [Android (SDK, NDK and so on)](https://www.mediafire.com/file/zt5n2q5hu70u94g/Android.zip/file)
- Install CMake and JDK. I used [JDK 17](https://www.oracle.com/java/technologies/javase/jdk17-archive-downloads.html)
- [Download libs](https://www.dropbox.com/scl/fi/90wkqzomm61s0lhmqcume/sdl-libs-and-box2dv3-v1.0.zip?rlkey=h8heed2gln48lfdh2jygd6ich&st=chgdwttl&raw=1)
- Save libs somewhere on your computer and changes paths in the `android-project/app/libs` folder:

```
dependencies {
    implementation files('H:/libs/SDL3-devel-3.3.0-android/SDL3-3.3.0.aar')
    implementation files('H:/libs/SDL3_image-devel-3.2.4-android/SDL3_image-3.2.4.aar')
    implementation files('H:/libs/SDL3_mixer-devel-3.1.0-android/SDL3_mixer-3.1.0.aar')
    implementation files('H:/libs/SDL3_ttf-devel-3.2.2-android/SDL3_ttf-3.2.2.aar')
    implementation files('H:/libs/box2d-3.2.0-android/box2d-3.2.0.aar')
    implementation 'androidx.appcompat:appcompat:1.5.1'
}
```

- Connect your device with USB-cable
- Active the Developer mode and Install mode in your phone settings
- Install APK:

```bash
> cd android-project
> gradlew installDebug
```

- Or build APK:

```bash
> cd android-project
> gradlew assembleDebug
```

Note. You can use [create-prefab-aar.py](https://gist.github.com/madebr/3563a41ec9d287b6754c5fe764f56a1c) to build Box2D AAR by yourself. For example you can build Box2D AAR with these commands:

Windows:

`
create-prefab-aar.py --verbose --cmake-source-dir H:/libs/box2d-build/tmp/box2d --cmake-common-args "-GNinja -DCMAKE_BUILD_TYPE=RelWithDebInfo -DANDROID_USE_LEGACY_TOOLCHAIN_FILE=FALSE -DCMAKE_TOOLCHAIN_FILE=H:/Android/SDK/ndk/23.1.7779620/build/cmake/android.toolchain.cmake -GNinja -DBOX2D_SAMPLES=OFF -DBOX2D_VALIDATE=OFF -DBOX2D_UNIT_TESTS=OFF -DBUILD_SHARED_LIBS=ON -DCMAKE_C_FLAGS=\"-ffile-prefix-map={SOURCE_DIR}=/src/{NAME}-{VERSION}\"" --name box2d --version 3.2.0 --add-target box2d --target-set-headers {PREFIX_DIR}/include/box2d/* --target-set-headers-root {PREFIX_DIR}/include --target-set-library {PREFIX_DIR}/lib/libbox2d.so --build-dir H:/libs/box2d-build/tmp/android-build --android-package-name org.box2d.android --license-paths {SOURCE_DIR}/LICENSE
`

Linux:

`
create-prefab-aar.py --cmake-source-dir /tmp/box2d --cmake-common-args "-GNinja -DCMAKE_BUILD_TYPE=RelWithDebInfo -DANDROID_USE_LEGACY_TOOLCHAIN_FILE=FALSE -DCMAKE_TOOLCHAIN_FILE=/home/maarten/Android/Sdk/ndk/27.0.11718014/build/cmake/android.toolchain.cmake -GNinja -DBOX2D_SAMPLES=OFF -DBOX2D_VALIDATE=OFF -DBOX2D_UNIT_TESTS=OFF -DBUILD_SHARED_LIBS=ON -DCMAKE_C_FLAGS=\"-ffile-prefix-map=<SOURCE_DIR>=/src/<NAME>-<VERSION>\"" --name box2d --version 3.2.0 --add-target box2d --target-set-headers <PREFIX_DIR>/include/box2d/* --target-set-headers-root <PREFIX_DIR>/include --target-set-library <PREFIX_DIR>/lib/libbox2d.so --build-dir /tmp/android-build --android-package-name org.box2d.android --license-paths <SOURCE_DIR>/LICENSE
`
