# flutter Setting

## flutter doctor

- **java 1.8 버전 사용 시 Android toolchain 에러 해결 방법**

  에러 내용

  ```html
  Android sdkmanager tool not
  found(/Users/ryan/Library/Android/sdk/tools/bin/sdkmanager). Try re-installing
  or updating your Android SDK, visit https://flutter.dev/setup/#android-setup
  for detailed instructions.
  ```

  Tools - SDK Manager - Setting - Appearance & Behavior - System Settings - Android SDK
  하단의 Show Package Details를 체크하고 Android SDK Command-line Tools의 버전 9 이하 사용
