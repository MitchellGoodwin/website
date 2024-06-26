## Configuring Android app support

{{site.alert.note}}
  Flutter relies on a full installation of Android Studio to supply
  its Android platform dependencies. However, you can write your
  Flutter apps in a number of editors; a later step discusses that.
{{site.alert.end}}

### Install Android Studio

 1. Download and install [Android Studio]({{site.android-dev}}/studio/install#chrome-os).
 1. Start Android Studio, and go through the 'Android Studio Setup Wizard'.
    This installs the latest Android SDK, platform tools and build tooling
    that are required by Flutter when developing for Android.
 1. From the welcome dialog, choose **More Actions -> SDK Manager**.
    From the SDK Tools tab, select
    **Android SDK Command-line Tools (latest)**
    to install additional necessary tooling.
 1. Accept Android licenses.

 ```console
$ flutter doctor --android-licenses
```

### Deploy to your Chromebook

To deploy apps directly to your Chromebook, you need to do the following:

 1. [Enable ADB][] in Settings. Note that this requires you to reboot your
    device once.
 1. In the Terminal, run `flutter devices`. If prompted, authorize access to
    the Android container. Verify that `flutter devices` lists your ChromeOS
    device as a recognized device.

### Set up your Android device

To prepare to run and test your Flutter app on an attached device,
you need an Android device running Android 5.0 (API level 21) or higher.

 1. Enable **Developer options** and **USB debugging** on your device.
    Detailed instructions are available in the
    [Android documentation]({{site.android-dev}}/studio/debug/dev-options).
 1. Using a USB cable, plug your phone into your computer.
    On your Chromebook, you might see a notification for
    "USB device detected". Click on "Connect to Linux".
    If prompted on your Android device,
    authorize your computer to access your device.
 1. In the terminal, run the `flutter devices` command to verify
    that Flutter recognizes your connected Android device.
    By default, Flutter uses the version of the
    Android SDK where your `adb` tool is based.
    If you want Flutter to use a different installation
    of the Android SDK, you must set the `ANDROID_SDK_ROOT`
    environment variable to that installation directory.

[Enable ADB]: https://support.google.com/chromebook/answer/9770692
