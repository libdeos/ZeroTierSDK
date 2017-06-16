ZeroTier Integrations
====

If you want everything built at once, type `make all` and go play outside for a few minutes, we'll copy all of the targets into the `build` directory for you along with specific instructions contained in a `README.md` on how to use each binary. You can then use `make -s check` to check the build status of each binary target.

*NOTE for Apple platforms: In order to build iOS/OSX Frameworks and Bundles you will need XCode command line tools `xcode-select --install`*

*NOTE: For Android JNI libraries to build you'll need to install [Android Studio](https://developer.android.com/studio/index.html) the [Android NDK](https://developer.android.com/ndk/index.html). Currently only Android NDK r10e is supported and can be found [here for OSX](http://dl.google.com/android/repository/android-ndk-r10e-darwin-x86_64.zip) and [here for Linux](http://dl.google.com/android/repository/android-ndk-r10e-linux-x86_64.zip). You'll need to tell our project where you put it by putting the path in [this file](android/proj/local.properties), you'll need to install the Android Build-Tools (this can typically be done through the editor the first time you start it up), and finally you should probably upgrade your Gradle plugin if it asks you to. If you don't have these things installed and configured we will detect that and just skip those builds automatically. Additionally, you can specify the target architectures you wish to build for by editing [Application.mk](android/android_jni_lib/java/jni/Application.mk). By default it will build `arm64-v8a`, `armeabi`, `armeabi-v7a`, `mips`, `mips64`, `x86`, and `x86_64`*

Below are the specific instructions for each integration requiring *little to no modification to your code*. Remember, with a full build we'll put a copy of the appropriate integration instructions in the resultant binary's folder for you anyway.

For more support on these integrations, or if you'd like help creating a new integration, stop by our [community section](https://www.zerotier.com/community/)!

***
## Important Build Flags

- `SDK_IPV4=1` - Enable IPv4 support
- `SDK_IPV6=1` - Enable IPv6 support

- `SDK_DEBUG=1` - Enables SDK debugging

- `SDK_PICOTCP=1` - Enable the use of `picoTCP` (recommended)
- `SDK_PICO_DEBUG=1` - Enables debug output for the `picoTCP` network stack

- `SDK_LWIP=1` - Enable the use of `lwIP` (deprecated)
- `SDK_LWIP_DEBUG=1` - Enables debug output for the `lwIP` library.

***

### Apple 
 - For everything: `make apple <flags>`

##### iOS
 - [Embedding within an app](apple/example_app/iOS) `make ios_app_framework` -> `build/ios_app_framework/*`
 - Unity3D plugin `make ios_unity3d_bundle` -> `build/ios_unity3d_bundle/*`

##### OSX
 - [Linking into an app at compiletime](../docs/osx.md) `make osx_static_lib` -> `build/libzt.a`
 - [Embedding within an app with Xcode](apple/example_app/OSX) `make osx_app_framework` -> `build/osx_app_framework/*`
 - [Dynamic-linking into an app/service at runtime](../docs/osx.md) `make osx_service_and_intercept` -> { `build/zerotier-sdk-service` + `build/libztintercept.so` }
 - [Intercept library](../docs/osx.md) `make osx_sdk_service` -> `build/zerotier-sdk-service`
 - [SDK Service](../docs/osx.md) `make osx_intercept` -> `build/libztintercept.so`
 - [Unity3D plugin](apple/ZeroTierSDK_Apple) `make osx_unity3d_bundle`

***
### Linux
 - For everything: `make linux <flags>`
 - [Dynamic-linking into an app/service at runtime](../docs/linux.md) `make linux_shared_lib`
 - Service and Intercept `make linux_service_and_intercept` -> { `build/zerotier-sdk-service` + `build/libztintercept.so` }
 - [Using the SDK with Docker](docker)

### Android 
 - For everything: `make android`
 
 - [Embedding within an app](android) `make android_jni_lib` -> `build/android_jni_lib/YOUR_ARCH/libZeroTierOneJNI.so`

***
### Windows
 - Not yet.
