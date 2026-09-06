<a href="#gh-light-mode-only">
  <img alt="Seoktae Lee — I ship apps, and I run the servers behind them." src="./assets/header-light.svg" width="100%">
</a>
<a href="#gh-dark-mode-only">
  <img alt="Seoktae Lee — I ship apps, and I run the servers behind them." src="./assets/header-dark.svg" width="100%">
</a>

기획부터 배포·운영까지 혼자 굴려본 앱 개발자입니다.
iOS·Android 앱 2종과 미니앱 5종을 **실제로 스토어에 올렸고**, 그 뒤의 서버·결제·푸시 인프라도 직접 운영하고 있습니다.
지금은 그 운영 경험을 **Java · Spring Boot** 위에 다시 세우는 중입니다.

<br/>

## Shipped Products

실제로 출시되어 사용자가 쓰고 있는 서비스입니다.

| 제품 | 한 줄 소개 | 내 역할 | 플랫폼 | 링크 |
|:--|:--|:--|:--|:--|
| **떠나** | 코스 장소에 도착하면 자동으로 촬영 알림이 뜨고, 하루가 끝나면 영상이 브이로그로 합성되는 여행 기록 앱 | 기획 · iOS · Android · 서버 · 인프라 **전부** | iOS / Android / Web | [App Store](https://apps.apple.com/kr/app/id6767218543) · [Google Play](https://play.google.com/store/apps/details?id=com.seoktaedev.tteona) · [tteona.kr](https://tteona.kr) |
| **티처스노크** | 교대생·임용고시 준비생을 위한 학습 관리 앱 (플래너 · 과목별 타이머 · 통계 · 스터디 그룹) | 기획 · iOS · Android · 서버 **전부** | iOS | [App Store](https://apps.apple.com/kr/app/id6757806439) |
| **AERON** | 위 서비스들을 만드는 1인 개발 스튜디오. App Store 개발자명이기도 합니다 | 운영 · 홈페이지 직접 제작 | Web | [aeron.kr](https://aeron.kr) |
| **앱인토스 미니앱 5종** | 헬로 · 내차여기 · 빨래요 · 레드볼 · 미룰래 — 토스 앱 안에서 도는 미니앱 | 기획 · 개발 · 출시 **전부** | Toss | 토스 앱 내 검색 |

<br/>

## Engineering Highlights

배지보다 이쪽을 봐주시면 좋겠습니다.

| 무엇을 | 어떻게 |
|:--|:--|
| **서버 3대 직접 운영** | nginx 리버스 프록시 · TLS(certbot) 자동 갱신 · PM2 무중단 재시작 · 백업 크론 · logrotate까지 직접 구성하고 장애도 직접 복구합니다 |
| **REST API 56개 · 단일 서비스** | 인증 · 코스 · 세션 · 채팅 · 결제 · 통계까지 한 서버에서 굴리며, 지금은 이걸 Spring Boot로 **스트랭글러 패턴 점진 이관** 중입니다 |
| **실시간 통신** | Socket.IO 기반 그룹 채팅과 위치 공유. 단일 프로세스 한계를 알기에 다음 과제로 **Redis Pub/Sub 수평 확장**을 잡아뒀습니다 |
| **푸시 2경로 운영** | 서버 직접 APNs(HTTP/2 + JWT) · Firebase Functions FCM 병행. sandbox 폴백과 수신자 언어별 문구까지 처리합니다 |
| **결제 · 구독** | PG 연동 결제와 RevenueCat 구독(entitlement 게이팅)을 실서비스에서 운영 중입니다 |
| **영상 자동 합성** | AVFoundation으로 클립 · 지도 핀 · 자막을 병렬 합성해 편집 없이 브이로그를 만듭니다 |
| **다국어 3개국어** | 한국어 · 영어 · 일본어를 iOS(xcstrings) · Android(strings.xml) · 서버 푸시 문구까지 일관되게 운영합니다 |

<br/>

## Tech Stack

**Backend** — 지금 주력으로 전환 중인 영역

![Java](https://img.shields.io/badge/Java-0D1117?style=flat-square&logo=openjdk&logoColor=E9EFF6)
![Spring Boot](https://img.shields.io/badge/Spring_Boot-0D1117?style=flat-square&logo=springboot&logoColor=6DB33F)
![Node.js](https://img.shields.io/badge/Node.js-0D1117?style=flat-square&logo=nodedotjs&logoColor=339933)
![Express](https://img.shields.io/badge/Express-0D1117?style=flat-square&logo=express&logoColor=E9EFF6)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-0D1117?style=flat-square&logo=postgresql&logoColor=4169E1)
![Firebase](https://img.shields.io/badge/Firebase-0D1117?style=flat-square&logo=firebase&logoColor=FFCA28)
![Socket.io](https://img.shields.io/badge/Socket.io-0D1117?style=flat-square&logo=socketdotio&logoColor=E9EFF6)

**Mobile**

![Swift](https://img.shields.io/badge/Swift-0D1117?style=flat-square&logo=swift&logoColor=F05138)
![SwiftUI](https://img.shields.io/badge/SwiftUI-0D1117?style=flat-square&logo=swift&logoColor=F05138)
![Kotlin](https://img.shields.io/badge/Kotlin-0D1117?style=flat-square&logo=kotlin&logoColor=7F52FF)
![Jetpack Compose](https://img.shields.io/badge/Jetpack_Compose-0D1117?style=flat-square&logo=jetpackcompose&logoColor=4285F4)

**Infra & Ops**

![Linux](https://img.shields.io/badge/Linux-0D1117?style=flat-square&logo=linux&logoColor=FCC624)
![NGINX](https://img.shields.io/badge/NGINX-0D1117?style=flat-square&logo=nginx&logoColor=009639)
![PM2](https://img.shields.io/badge/PM2-0D1117?style=flat-square&logo=pm2&logoColor=2B037A)
![Let's Encrypt](https://img.shields.io/badge/Let's_Encrypt-0D1117?style=flat-square&logo=letsencrypt&logoColor=E9EFF6)
![Git](https://img.shields.io/badge/Git-0D1117?style=flat-square&logo=git&logoColor=F05032)

<br/>

## Currently

- **Java · Spring Boot 이관** — 티처스노크 백엔드를 스트랭글러 패턴으로 옮기는 중입니다
- **[cs-study](https://github.com/seoktae-lee/cs-study)** — 컴퓨터구조 · 알고리즘 · 네트워크 · 데이터베이스 · 운영체제를 골고루 정리하고 있습니다
- **알고리즘** — 자료구조부터 그래프까지 순서대로 (`cs-study/02_algorithm`)

<br/>

## Repositories

| 저장소 | 내용 |
|:--|:--|
| [tteona](https://github.com/seoktae-lee/tteona) | 떠나 iOS — SwiftUI · MapKit · CoreLocation · AVFoundation |
| [tteona-android](https://github.com/seoktae-lee/tteona-android) | 떠나 Android — Kotlin · Jetpack Compose · Socket.IO |
| [tteona-web](https://github.com/seoktae-lee/tteona-web) | tteona.kr — 랜딩 · 코스 공유 · PWA 탐색 앱 |
| [TeachersKnock-ios](https://github.com/seoktae-lee/TeachersKnock-ios) | 티처스노크 iOS — SwiftUI · Firebase · WidgetKit |
| [TeachersKnock-android](https://github.com/seoktae-lee/TeachersKnock-android) | 티처스노크 Android — Room · Firestore 동기화 |
| [aeron-web](https://github.com/seoktae-lee/aeron-web) | aeron.kr — 의존성 없는 순수 HTML/CSS/JS |
| [cs-study](https://github.com/seoktae-lee/cs-study) | CS 전공 5과목 공부 기록 |

<br/>

## Contact

<a href="https://aeron.kr"><img src="https://img.shields.io/badge/aeron.kr-0D1117?style=flat-square&logo=safari&logoColor=E9EFF6"></a>
<a href="https://github.com/seoktae-lee"><img src="https://img.shields.io/badge/GitHub-0D1117?style=flat-square&logo=github&logoColor=E9EFF6"></a>
