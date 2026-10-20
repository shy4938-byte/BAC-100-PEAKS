# 갤럭시 APK v0.9.0

100개 산별 일러스트·지도·최단/추천 코스·주변 식당을 보는 현재 앱을 Capacitor Android 설치 파일로 포함했다. 회원가입·Supabase·Vercel 없이 실행하며 이미지와 코스 안내는 앱 안에 있다. 정상석 사진 등록 기능은 없다. 외부 공식 자료·네이버 링크에는 인터넷이 필요하다. 공식 대조 범위는 COURSE-PAIRS.md를 참고한다.

## 설치와 공유

1. 갤럭시에서 `BAC-100-PEAKS-Galaxy-v0.9.0.apk`를 다운로드한다.
2. 다운로드 알림 또는 ‘내 파일 → 다운로드’에서 해당 APK를 연다.
3. 휴대폰이 요청하면 파일을 연 앱에 대해 ‘이 출처 허용’을 선택하고 설치한다.
4. BAC 100 PEAKS 아이콘을 열어 사용한다.

같은 APK를 다른 갤럭시 사용자에게 공유할 수 있다. Play Store 배포본이 아닌 직접 설치 파일이다. Android 6(API 23) 이상, Android System WebView 92 이상을 요구한다. 삼성 실기기 설치·동작과 모든 구형 기기 호환을 검증한 것은 아니다.

앱 ID는 `kr.bac100peaks.app`, versionName은 `0.9.0`, versionCode는 `9000`이다. v0.4.0 APK와 서명 인증서가 같음을 비교했다. 따라서 같은 공식 배포 APK가 설치되어 있다면 삭제하지 않고 새 파일로 업데이트할 수 있다. 기존 기기 저장소를 지우거나 사진·기록을 읽는 새 동작은 없다. 현재 UI에는 기록·사진 기능을 제공하지 않는다.

## 확인 범위

- 웹 빌드·Capacitor sync·서명된 release APK 생성 성공.
- apksigner 검증 성공; 이전 v0.4.0 인증서 SHA-256 일치.
- Android manifest의 버전·최소/대상 SDK 확인. 별도 사진·카메라·위치 권한 없음.
- APK 내부에 배너와 일러스트 포함. 서비스 워커와 웹 매니페스트 제외.
- 실제 APK에서 추출한 정적 파일을 390×844 모바일 Chromium에서 오프라인으로 검사: 100개 지도 마커, 한라산 일러스트, 확대, 추천 코스 선택·새로고침, 식당 3개, 사진 입력 없음, 가로 넘침 없음, 외부 요청·JavaScript 오류 없음.
- 실제 Android WebView/삼성 기기 설치·실행은 미검증. 이 환경에는 KVM 장치가 없으며 이전 API 35 소프트웨어 에뮬레이터 부팅도 실패하여 동일 시도를 반복하지 않았다. 모바일 Chromium 검사는 실기기 검사와 구분한다.

## 재빌드

Node 24, JDK 21, Android SDK 플랫폼 35, build-tools 35.0.0이 필요하다. 이 환경은 `/workspace/android-jdk/current`, `/workspace/android-sdk`를 사용한다.

```bash
JAVA_HOME=/workspace/android-jdk/current PATH=/workspace/android-jdk/current/bin:$PATH npm run android:apk
node tests/android-assets-smoke.mjs
```

APK 이름과 Android versionName은 package.json의 버전에서 가져온다. versionCode는 major×1000000 + minor×1000 + patch로 생성한다. 서명 키는 저장소 바깥의 기존 `.bac100-android-signing`을 재사용하며 파일·암호를 배포물이나 Git에 포함하지 않는다. 키를 잃으면 같은 앱으로 업데이트할 수 없으므로 개발자가 별도로 보관한다. SDK·Gradle 다운로드와 TLS 검증은 유지한다.
