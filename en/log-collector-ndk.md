<!-- machine_translated: true -->

<!-- pre-align:aligned sig=b91e3d4ff2a8 -->

<a id="nhn-cloud-sdk-user-guide-log-crash-android-ndk"></a>
## NHN Cloud > SDK User Guide > Log & Crash > Android (NDK) { #nhn-cloud-sdk-user-guide-log-crash-android-ndk }

<a id="android-ndk-crash-report"></a>
## Android NDK Crash Report { #android-ndk-crash-report }

If your Android app includes native libraries, a simple build setup will enable full stack traces and detailed error reports for native code.

* NHN Cloud Crash Reporter for NDK is available on **NHN Cloud 0.21.0 and higher**.
* NHN Cloud Crash Reporter for NDK sends crash logs through NHN Cloud Logger.
* It is recommended that you **use the same version** of NHN Cloud Logger and NHN Cloud Crash Reporter for NDK libraries.
* NHN Cloud Crash Reporter for NDK starts crash detection at NHN Cloud Logger initialization.
* NHN Cloud Crash Reporter for NDK requires **NDK r17c or higher**.

<a id="prerequisites"></a>
### Prerequisites { #prerequisites }

1. Install [NHN Cloud Log & Crash](./log-collector-android).

<a id="library-setting"></a>
### Library Setting { #library-setting }
- Add dependencies in the app-level build.gradle.

```groovy
repositories {
    mavenCentral()
}

dependencies {
    // ...
    // Add the NHN Cloud Logger dependency
    implementation 'com.nhncloud.android:nhncloud-logger:1.13.0'

    // Add the NHN Cloud Crash Reporter for NDK dependency
    implementation 'com.nhncloud.android:nhncloud-crash-reporter-ndk:1.13.0'
}
```

<a id="crash-analysis"></a>
### Crash Analysis { #crash-analysis }

* When native crash occurs, dump (.dmp) file is generated.
* The process of interpreting the generated dump file is called **Symbolication**.
* You must upload a symbol file for an accurate stack trace.
* When the symbol file is uploaded, you can check the crash information analyzed in Log & Crash Search Console when a crash occurs.

<a id="crash-analysis-symbol-upload"></a>
#### Symbol Upload

* A symbol file is generated as a {library name}.so file in the project's specific path.
* The maximum size of the upload file is 500 MB.
* Compress {library name}.so into {library name}.so.zip and upload it from [Log & Crash Search > Settings > Symbol File].

<a id="crash-analysis-symbol-file-path"></a>
#### Symbol File Path

- ndk-build: .so file is generated under {PROJECT}/obj/local/{ANDROID_ABI}.
- cmake: .so file is generated under {PROJECT}/build/intermediates/{VARIANTS}/obj/{ANDROID_ABI}.
