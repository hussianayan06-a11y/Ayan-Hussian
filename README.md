name: Build APK
on:
  workflow_dispatch:
  push:
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-java@v4
        with:
          distribution: temurin
          java-version: 17
      - uses: gradle/actions/setup-gradle@v4
        with:
          gradle-version: 8.9
      - run: unzip -q ayan-voice-android.zip
      - run: gradle assembleDebug
        working-directory: ayan-voice-android
      - uses: actions/upload-artifact@v4
        with:
          name: ayan-apk
          path: ayan-voice-android/app/build/outputs/apk/debug/app-debug.apk
