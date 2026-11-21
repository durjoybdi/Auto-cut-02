name: Build APK
on:
  push:
    branches: [main]
  workflow_dispatch:
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Arrange files
        run: |
          mkdir -p app/src/main/java/com/example/autocut app/src/main/res/layout
          mv Processor.kt MainActivity.kt ColorGrade.kt app/src/main/java/com/example/autocut/
          mv activity_main.xml app/src/main/res/layout/
          mv AndroidManifest.xml app/src/main/
          mv app-build.gradle.kts app/build.gradle.kts
      - uses: actions/setup-java@v4
        with:
          distribution: temurin
          java-version: 17
      - uses: gradle/actions/setup-gradle@v4
        with:
          gradle-version: 8.9
      - run: gradle :app:assembleDebug --no-daemon
      - uses: actions/upload-artifact@v4
        with:
          name: AutoCut-apk
          path: app/build/outputs/apk/debug/*.apk
