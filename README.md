# 진수티비 Android 0.5.2

Android 8.0 이상용 APK입니다. Node.js·PC 서버 없이 기기에서 실제 목록·검색·회차를 처리하고, 원본 재생 페이지는 앱 브리지가 없는 별도 WebView에서 엽니다.

## 0.5.2 빌드 상태

- APK: `JinsuTV-0.5.2-Android.apk`
- package `app.jinsu.tv`, versionName `0.5.2`, versionCode `6`, minSdk `26`, targetSdk `35`
- 크기: **2,569,810 bytes**
- SHA-256: `e41b16058d60bb63c43b22493e6de73c55cf67f8d642b5e848e5f4986434b0d2`
- 서명 인증서 SHA-256: `91c80fd08f32a24980cd7604f53cfd530decd97ceed913202a2a80e79b964616` — 0.5.0과 같은 키여서 기존 앱을 지우지 않고 업그레이드할 수 있는 구성입니다.
- 빌드/정적 검증은 완료됐지만, 이 문서 작성 시점의 실제 Android 기기 WebView·설치·업그레이드·재생은 아직 검증하지 않았습니다.

### 주요 변경: 목록 연결 경로

0.5.2는 WebView가 `Chromium 서버 연결 오류`로 실패한 기기를 위해 목록/검색/상세 HTML 연결을 보정합니다. 오래된 고정 Chrome 사용자 에이전트를 제거하고 **기기에 설치된 최신 System WebView의 실제 UA**를 브라우저 형태로 사용합니다. 목록 WebView는 화면 밖이 아닌 앱 창 안의 1px 연결 뷰로 유지해 일부 제조사의 off-screen/background 연결 실패 가능성도 줄였습니다.

- 서버가 렌더링한 최종 HTML만 기존의 신뢰된 네이티브 파서에 전달하며, 원격 페이지를 앱 UI로 렌더링하지 않습니다.
- 목록 WebView에는 JavaScript 인터페이스·파일/콘텐츠 접근·다운로드·새 창·권한이 없고, HTTP/HTTPS 하위 리소스를 차단합니다.
- HTTPS·공개 DNS·동일 출처·리디렉션 3회·응답 크기·시간 제한을 유지합니다. 초기화/연결 실패 때만 기존의 엄격한 직접 HTTPS 전송을 fallback으로 사용합니다.
- 원본 영상 URL·세션·DRM을 추출하거나 우회하지 않습니다. 재생 페이지의 기존 별도 WebView에도 앱 브리지를 추가하지 않습니다.

## APK 자동 업데이트

실행 시 고정된 Android 채널을 확인합니다:

`https://raw.githubusercontent.com/slpbabo-ai/JInsootv/main/updates/android.json`

새 versionCode가 있으면 APK를 자동 다운로드하고 **SHA-256·바이트 수·패키지명·versionCode/versionName·minSdk·기존 앱 서명**을 확인합니다. 설치 직전에 다시 확인합니다. 다운로드가 실패하거나 검증되지 않으면 설치하지 않습니다.

**일반 APK 배포에서 마지막 설치는 Android 시스템 확인이 필요합니다.** 준비되면 설치 안내가 표시됩니다. 요청받으면 진수티비의 **이 출처 허용**을 켜고 돌아와 설치를 확인하세요. 무인 설치, 루팅, 시스템 권한·보안 정책 우회는 하지 않습니다.

- 설정 → **Android 앱 업데이트 → 업데이트 확인 / Android 설치 화면 열기**
- 앱 실행 때만 자동 확인하며 원격 재생 Activity나 백그라운드에서 설치 화면을 강제로 띄우지 않습니다.
- 모바일 데이터가 사용될 수 있습니다. 설치를 취소하면 현재 앱을 계속 사용할 수 있습니다.
- 설치 허용/기기 정책 때문에 실패하면 보안 정책을 끄지 말고 기기 담당자에게 확인하세요.

## Windows와 배포 채널 분리

- Android는 `android-v0.5.2` 같은 별도 태그와 `updates/android.json`을 씁니다.
- **Android Release를 저장소 Latest로 지정하지 마세요.** Windows Latest는 `v0.3.4`로 유지해야 합니다.
- APK 공개·해시·서명을 먼저 확인한 뒤에만 `updates/android.json`을 새 버전으로 갱신합니다. 같은 공개 버전을 덮어쓰지 않습니다.

## 권한 / 보안

권한은 `INTERNET`과 `REQUEST_INSTALL_PACKAGES`입니다. 외부 저장소·카메라·마이크·위치·관리자 권한을 요구하지 않습니다.

- 메타데이터 URL과 APK GitHub 저장소를 코드에서 고정합니다. 로컬 UI RPC는 상태·확인·설치 요청만 허용하며 URL·경로·명령어를 받지 않습니다.
- HTTPS 기본 인증서/호스트 검증, 공개 DNS 검사, 승인된 GitHub CDN 리디렉션, 메타데이터 64 KB / APK 32 MB / 시간 제한을 적용합니다.
- 검증 APK는 앱 내부 저장소의 SHA-256 파일명으로 보관합니다. 원격 WebView에는 네이티브 인터페이스가 없습니다.
- 비공개 `UpdateApkProvider`는 정확한 해시 URI만 읽기 전용으로 열며 설치 Intent에만 URI 읽기 권한을 부여합니다. 일반 파일 접근/쓰기/경로 탐색은 거부합니다.
- 기존 설정/찜/기록 저장 키를 유지하며 삭제나 마이그레이션을 강요하지 않습니다.

현재 키는 **기존 개발용 테스트 키**입니다. 키 파일은 GitHub/APK에 넣지 않았습니다. 안전하게 백업하고 공개하지 마세요. 정식 배포키로 바꾸려면 별도 마이그레이션 계획이 필요합니다.

## 빌드 / 검사

`build.sh`는 준비된 Android SDK 35 build-tools/platform, JDK 17, 고정 해시 Jsoup jar, 로컬 웹 assets 및 기존 서명키를 사용합니다. SDK/JDK 다운로드 출처와 해시는 `SDK-LOCK.json`, `JDK-LOCK.json`, 런타임/호스트 의존성은 `DEPENDENCIES.json`에 있습니다. 웹 UI는 공유 `../noir-desktop`에서 Node 22로 빌드해 `app/src/main/assets/www`로 복사합니다. **앱 실행에 Node.js는 필요하지 않습니다.**

```sh
JAVA_HOME=/path/to/jdk17 bash build.sh
```

검사 결과는 `TEST-REPORT.md`와 `build-0.5.2.log`를 참고하세요. 키가 없으면 새 키를 몰래 생성하지 않고 빌드를 중단합니다.

**Android 실기기 설치·0.5.0에서 0.5.2로의 실제 자동 업그레이드·시스템 WebView 목록 연결·원본 영상 재생은 미검증**입니다. 알려진 광고 필터를 유지하지만 모든 광고 차단/콘텐츠 동작을 보장하지 않습니다.
