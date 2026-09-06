<a href="#gh-light-mode-only">
  <img alt="Seoktae Lee — I ship apps, and I run the servers behind them." src="./assets/header-light.svg" width="100%">
</a>
<a href="#gh-dark-mode-only">
  <img alt="Seoktae Lee — I ship apps, and I run the servers behind them." src="./assets/header-dark.svg" width="100%">
</a>

기획부터 배포·운영까지 혼자 굴려본 개발자입니다.
**iOS·Android 네이티브 앱 2종**, **토스 미니앱 5종**, **웹 서비스**, **라즈베리파이 임베디드**까지
서로 다른 층위에서 만들어봤고, 그중 7개는 실제로 스토어에 올라가 사용자가 쓰고 있습니다.
지금은 그 운영 경험을 **Java · Spring Boot** 위에 다시 세우는 중입니다.

<br/>

## Projects

### 출시 제품

| 제품 | 무엇 | 내 역할 | 규모 · 근거 | 링크 |
|:--|:--|:--|:--|:--|
| **티처스노크** | 초등 임용고시 수험생 학습 관리 앱. 캐릭터 육성 · 스터디 그룹 · 공동 타이머로 장기 수험의 동기 유지를 설계 | 기획 · 디자인 · 서버 · iOS · Android · 배포 **전부** | Swift 120파일 32,899줄 · Cloud Functions 14개 · Firestore 19컬렉션 · 5개월 1인 개발 | [App Store](https://apps.apple.com/kr/app/id6757806439) |
| **떠나** | 코스 장소에 도착하면 자동 촬영 알림이 뜨고, 하루가 끝나면 영상이 브이로그로 합성되는 여행 기록 앱 | 기획 · 디자인 · 서버 · iOS · Android · 웹 · 인프라 **전부** | REST API 56개 · 실서버 3대 · 3개국어 | [App Store](https://apps.apple.com/kr/app/id6767218543) · [Google Play](https://play.google.com/store/apps/details?id=com.seoktaedev.tteona) · [tteona.kr](https://tteona.kr) |
| **토스 미니앱 5종** | 헬로 · 내차여기 · 빨래요 · 레드볼 · 미룰래. 토스 앱 안에서 도는 독립 서비스 5개 | 5개 전부 기획 · 프론트 · **백엔드 각각 별도 구축** · 심사 · 출시 | 미니앱마다 독립 Express·TypeScript 서버 + JWT 인증 | 토스 앱 내 |

### 웹

| 서비스 | 무엇 | 특징 |
|:--|:--|:--|
| **[tteona.kr](https://tteona.kr)** | 떠나 공식 사이트 · 코스 공유 페이지 · PWA 탐색 앱 | 딥링크(AASA·assetlinks) 연동, robots·sitemap·JSON-LD SEO, 스토어 전환 픽셀 직접 구현 |
| **aeron-web** | 개인 스튜디오 홈페이지 | 프레임워크·의존성 0. 스크롤 리빌과 `data-i18n` 다국어 전환을 직접 구현 |

### 팀 · 학교 프로젝트

| 프로젝트 | 무엇 | 내가 한 것 |
|:--|:--|:--|
| **라즈베리파이 화재 감지** | 불꽃 감지 시 WS2812 링 LED로 발화 위치를 알리는 장치 | C + wiringPi + rpi_ws281x. 불꽃센서 2개를 100ms로 폴링하고 링 LED 인덱스를 층(2F·3F)에 매핑 |

<br/>

## Engineering Highlights

배지보다 이쪽을 봐주시면 좋겠습니다. 프로젝트별로 실제 부딪힌 문제와 해결입니다.

<details open>
<summary><b>티처스노크</b> — 인증 · 권한 · 데이터 정합성</summary>

<br/>

- **인증 취약점 제거 + 무중단 계정 마이그레이션**
  초기 카카오 로그인이 `kakao_pw_<카카오ID>` 형태의 **예측 가능한 비밀번호** 계정으로 우회 구현돼 있었습니다.
  서버가 카카오 access token을 직접 검증하고 Firebase **Custom Token**을 발급하는 방식으로 바꿔 비밀번호 자체를 없앴습니다.
  진짜 어려웠던 건 UID 변경이었습니다 — 하위 컬렉션 8종 배치 복사, 친구 관계 **양방향** 교체, 진행 중인 요청의 발신·수신 UID 교체까지
  **업데이트 후 첫 로그인 시 자동 실행**되게 만들고 결과를 `migration_logs`에 남겨 이관 성공률을 추적했습니다.

- **보안 규칙과 기능의 충돌 → 규칙을 푸는 대신 신뢰 경계를 옮김**
  친구 수락은 상대방 문서에도 써야 하는데, 규칙을 풀면 누구나 남의 친구 목록을 조작할 수 있게 됩니다.
  규칙은 deny-by-default 그대로 두고 **해당 연산만 Callable Function으로 승격**해 Admin SDK 트랜잭션으로 처리했습니다.

- **기기 간 진행도 롤백 해결**
  `last-write-wins` 덮어쓰기를 **경험치 최댓값 병합**으로 바꿨습니다. exp는 단조 증가하므로
  어느 쪽이 최신인지 몰라도 진행도가 보존됩니다. 저장 실패 시 재시도까지 붙였습니다.

- **개인정보보호법 대응 탈퇴 파이프라인** — 남은 참조가 다른 사용자 화면에 유령 데이터로 남지 않도록 7단계 순차 삭제로 구현했습니다.

</details>

<details>
<summary><b>떠나</b> — 서버 운영 · 실시간 · 미디어</summary>

<br/>

- **실서버 3대 직접 운영** — nginx 리버스 프록시, certbot TLS 자동 갱신, PM2 무중단 재시작, 백업 크론, logrotate까지 직접 구성하고 장애도 직접 복구합니다.
- **단일 서비스 REST API 56개** — 인증·코스·세션·채팅·결제·통계를 한 서버(4,234줄)에서 운영 중이며, 지금 이걸 **Spring Boot로 스트랭글러 패턴 점진 이관**하고 있습니다.
- **실시간 통신** — Socket.IO 그룹 채팅·위치 공유. 단일 프로세스라 서버를 늘리면 깨진다는 걸 알기에 **Redis Pub/Sub 수평 확장**을 다음 과제로 잡아뒀습니다.
- **푸시 2경로** — 서버 직접 APNs(HTTP/2 + JWT)와 Firebase FCM을 병행하고, sandbox 폴백과 수신자 언어별 문구를 처리합니다.
- **영상 자동 합성** — AVFoundation으로 클립·지도 핀·자막을 병렬 합성해 편집 없이 브이로그를 만듭니다.
- **다국어 3개국어** — 한국어·영어·일본어를 iOS(xcstrings)·Android(strings.xml)·서버 푸시 문구까지 일관되게 운영합니다.

</details>

<details>
<summary><b>토스 미니앱 5종</b> — 플랫폼 위에서 5번 반복한 것</summary>

<br/>

- **미니앱 하나당 백엔드 하나** — 5개 모두 별도의 Express · TypeScript 서버를 세우고 **JWT 인증과 토스 로그인 연동**을 각각 구현했습니다. 같은 구조를 5번 반복하며 무엇이 공통이고 무엇이 도메인인지 구분하게 됐습니다.
- **플랫폼 제약 대응** — 토스 푸시는 동의문(`termsId`)별로 동의가 갈려서, 발송 시점의 동의문이 다르면 **전량 차단**됩니다. 이런 플랫폼 고유 제약을 문서만으로 알기 어려워 운영하며 찾아냈습니다.
- **LLM 연동** — 일부 미니앱에 Anthropic · OpenAI · Gemini SDK를 붙여 이미지·텍스트 판별 기능을 넣었습니다.
- **디자인 시스템 준수** — 토스 TDS(`@toss/tds-mobile`)를 그대로 써서 토스 앱 안에서 이질감 없게 맞췄습니다. React · TypeScript · Vite · Emotion.

</details>

<br/>

## Tech Stack

**Backend** — 주력으로 전환 중인 영역

![Java](https://img.shields.io/badge/Java-0D1117?style=flat-square&logo=openjdk&logoColor=E9EFF6)
![Spring Boot](https://img.shields.io/badge/Spring_Boot-0D1117?style=flat-square&logo=springboot&logoColor=6DB33F)
![Node.js](https://img.shields.io/badge/Node.js-0D1117?style=flat-square&logo=nodedotjs&logoColor=339933)
![Express](https://img.shields.io/badge/Express-0D1117?style=flat-square&logo=express&logoColor=E9EFF6)
![TypeScript](https://img.shields.io/badge/TypeScript-0D1117?style=flat-square&logo=typescript&logoColor=3178C6)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-0D1117?style=flat-square&logo=postgresql&logoColor=4169E1)
![Firebase](https://img.shields.io/badge/Firebase-0D1117?style=flat-square&logo=firebase&logoColor=FFCA28)
![Socket.io](https://img.shields.io/badge/Socket.io-0D1117?style=flat-square&logo=socketdotio&logoColor=E9EFF6)

**Mobile**

![Swift](https://img.shields.io/badge/Swift-0D1117?style=flat-square&logo=swift&logoColor=F05138)
![SwiftUI](https://img.shields.io/badge/SwiftUI-0D1117?style=flat-square&logo=swift&logoColor=F05138)
![Kotlin](https://img.shields.io/badge/Kotlin-0D1117?style=flat-square&logo=kotlin&logoColor=7F52FF)
![Jetpack Compose](https://img.shields.io/badge/Jetpack_Compose-0D1117?style=flat-square&logo=jetpackcompose&logoColor=4285F4)

**Web**

![React](https://img.shields.io/badge/React-0D1117?style=flat-square&logo=react&logoColor=61DAFB)
![Vite](https://img.shields.io/badge/Vite-0D1117?style=flat-square&logo=vite&logoColor=646CFF)
![HTML5](https://img.shields.io/badge/HTML5-0D1117?style=flat-square&logo=html5&logoColor=E34F26)

**Infra & Ops**

![Linux](https://img.shields.io/badge/Linux-0D1117?style=flat-square&logo=linux&logoColor=FCC624)
![NGINX](https://img.shields.io/badge/NGINX-0D1117?style=flat-square&logo=nginx&logoColor=009639)
![PM2](https://img.shields.io/badge/PM2-0D1117?style=flat-square&logo=pm2&logoColor=2B037A)
![Let's Encrypt](https://img.shields.io/badge/Let's_Encrypt-0D1117?style=flat-square&logo=letsencrypt&logoColor=E9EFF6)
![Git](https://img.shields.io/badge/Git-0D1117?style=flat-square&logo=git&logoColor=F05032)

**Embedded**

![C](https://img.shields.io/badge/C-0D1117?style=flat-square&logo=c&logoColor=A8B9CC)
![Raspberry Pi](https://img.shields.io/badge/Raspberry_Pi-0D1117?style=flat-square&logo=raspberrypi&logoColor=A22846)

<br/>

## Currently

- **Java · Spring Boot 이관** — 티처스노크 백엔드를 스트랭글러 패턴으로 옮기는 중입니다
- **[cs-study](https://github.com/seoktae-lee/cs-study)** — 컴퓨터구조 · 알고리즘 · 네트워크 · 데이터베이스 · 운영체제를 골고루 정리하고 있습니다
- **알고리즘** — 자료구조부터 그래프까지 순서대로 (`cs-study/02_algorithm`)

<br/>

## Repositories

| 저장소 | 내용 |
|:--|:--|
| [TeachersKnock-ios](https://github.com/seoktae-lee/TeachersKnock-ios) | 티처스노크 iOS — SwiftUI · Firebase · Cloud Functions · WidgetKit |
| [TeachersKnock-android](https://github.com/seoktae-lee/TeachersKnock-android) | 티처스노크 Android — Room 로컬 DB · Firestore 동기화 |
| [tteona](https://github.com/seoktae-lee/tteona) | 떠나 iOS — SwiftUI · MapKit · CoreLocation · AVFoundation |
| [tteona-android](https://github.com/seoktae-lee/tteona-android) | 떠나 Android — Kotlin · Jetpack Compose · Socket.IO |
| [tteona-web](https://github.com/seoktae-lee/tteona-web) | tteona.kr — 랜딩 · 코스 공유 · PWA 탐색 앱 |
| [aeron-web](https://github.com/seoktae-lee/aeron-web) | 스튜디오 홈페이지 — 의존성 없는 순수 HTML/CSS/JS |
| [cs-study](https://github.com/seoktae-lee/cs-study) | CS 전공 5과목 공부 기록 |

<br/>

## Contact

<a href="https://tteona.kr"><img src="https://img.shields.io/badge/tteona.kr-0D1117?style=flat-square&logo=safari&logoColor=E9EFF6"></a>
<a href="https://github.com/seoktae-lee"><img src="https://img.shields.io/badge/GitHub-0D1117?style=flat-square&logo=github&logoColor=E9EFF6"></a>
