# Docker for Android SDK 28

Docker for Android SDK 28 with preinstalled build tools and emulator image

> Edit from [androidsdk/android-28](https://github.com/docker-android-sdk/android-28)

**Installed Packages**
```bash
# sdkmanager --list
  Path                                        | Version | Description                                | Location
  -------                                     | ------- | -------                                    | -------
  build-tools;32.0.0                          | 32.0.0  | Android SDK Build-Tools 32.0.0             | build-tools/32.0.0/
  cmdline-tools;latest                        | 2.1     | Android SDK Command-line Tools (latest)    | cmdline-tools/latest/
  emulator                                    | 30.1.5  | Android Emulator                           | emulator/
  patcher;v4                                  | 1       | SDK Patch Applier v4                       | patcher/v4/
  platform-tools                              | 30.0.4  | Android SDK Platform-Tools                 | platform-tools/
  platforms;android-28                        | 6       | Android SDK Platform 28                    | platforms/android-28/
  system-images;android-28;android-tv;x86     | 10      | Android TV Intel x86 Atom System Image     | system-images/android-28/android-tv/x86/
```

**Usage**

- Already preinstalled
  ```bash
  $ docker run -it --rm --device /dev/kvm britishrockfan/androidsdk28_witn_androidtv:latest bash
  # check prebuilt emulator
  $ emulator -list-avds
  # launch Android TV 1080p emulator in headles mode
  $ emulator -avd AndroidTV_28 -no-window -no-audio
  ```
- Interactive way
  ```bash
  $ docker run -it --rm --device /dev/kvm britishrockfan/androidsdk28_witn_androidtv:latest bash
  # check installed packages
  $ sdkmanager --list
  # create and run emulator
  $ avdmanager create avd -n first_avd --abi android-tv/x86 -k "system-images;android-28;android-tv;x86"
  $ emulator -avd first_avd -no-window -no-audio &
  $ adb devices
  # You can also run other Android platform tools, which are all added to the PATH environment variable
  ```

  To connect the emulator using `adb` on the docker host machine, start the container with `--network host`.
  You could also use [`scrcpy`](https://github.com/Genymobile/scrcpy) to do a screencast of the emulator.

- Non-interactive way
  ```bash
  # check installed packages
  $ docker run -it --rm britishrockfan/androidsdk28_witn_androidtv:latest sdkmanager --list
  # list existing emulators
  $ docker run -it --rm britishrockfan/androidsdk28_witn_androidtv:latest list avd
  # You can also run other Android platform tools, which are all added to the PATH environment variable
  ```