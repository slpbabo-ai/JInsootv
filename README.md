# 진수티비 배포

Windows 10/11 x64용 진수티비 설치파일과 자동 업데이트 파일을 배포하는 저장소입니다.

## 다운로드

[최신 정식 Release](https://github.com/slpbabo-ai/JInsootv/releases/latest)에서 `JinsuTV-버전-Windows-x64-Setup.exe`를 받으세요. Node.js 별도 설치는 필요 없습니다.

- 기존 포터블은 완전히 종료한 뒤 설치형을 한 번 수동 설치하세요.
- 설치형 앱은 실행할 때 새 안정 버전을 확인하고 다운로드·검증 후 설치/재실행합니다.
- 설치파일, `.blockmap`, `latest.yml`은 같은 Release에서 제공됩니다.
- GitHub의 자동 생성 Source code ZIP은 앱 설치파일이 아닙니다. 이 저장소는 바이너리 배포용입니다.

## 주의

현재 배포 파일은 Windows 코드 서명이 없습니다. 실제 Windows 장치의 설치·자동 업그레이드 및 모든 영상 재생을 보장하지 않습니다. Netflix·TVWIKI와 제휴한 앱이 아니며 영상 콘텐츠는 포함하지 않습니다.


## Android APK

[Android 0.5.0 다운로드](https://github.com/slpbabo-ai/JInsootv/releases/tag/android-v0.5.0) · Android 8.0 이상

- `JinsuTV-0.5.0-Android.apk`를 직접 설치하세요. 기존 0.4.0과 같은 서명키를 사용하며 versionCode는 5입니다.
- 새 APK는 실행 시 Android 전용 채널을 확인해 자동 다운로드·해시/패키지/버전/서명을 검증합니다. 마지막 설치는 Android 시스템 확인과 필요 시 진수티비의 '이 출처 허용'이 필요합니다.
- 기존 0.4.0에는 업데이트 기능이 없으므로 이번 0.5.0은 한 번 직접 설치해야 합니다.
- Android 채널: [updates/android.json](updates/android.json). **Android Release는 Latest로 지정하지 않습니다.** 저장소 Latest는 Windows 업데이트용입니다.
- 개발용 서명이며 Android 실기기 설치·자동 업그레이드·모든 영상 재생은 미검증입니다.
