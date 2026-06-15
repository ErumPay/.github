# 💳 ErumPay

<div align='center'>
  <img width="658" height="242" alt="image" src="https://github.com/user-attachments/assets/0de0ae22-8391-454d-abfc-3b9a31430628" />
</div>

<br>

## 👩🏻‍💻 프로젝트 소개
여러 장의 카드를 보유하고 있어도 결제 순간 어떤 카드가 가장 유리한지 판단하기는 쉽지 않습니다.
<br>
하지만 ErumPay는 결제 데이터를 기반으로 카드 혜택과 실적 조건을 분석하여 최적의 결제 방식을 추천합니다.
<br>
사용자의 결제 **의사결정을 자동화**하고, 분할결제·더치페이·원격결제를 통해 편리한 결제 경험을 제공하는 금융 결제 플랫폼입니다.

<br>

## ✨ 주요 기능
<table>
  <tr>
    <td width="50%">
      <h3>🤖 지능형 카드 추천</h3>
      <p>
        결제 요청 시 카드혜택, 실적, MCC를 분석하여
        사용자에게 가장 높은 혜택을 제공하는 카드를 추천합니다.
      </p>
    </td>
    <td width="50%">
      <h3>➗ 분할결제</h3>
      <p>
       하나의 결제 금액을 여러 카드에 나누어 결제하여
        카드별 혜택 한도나 실적 조건을 더욱 효율적으로 활용합니다.
      </p>
    </td>
  </tr>
  <tr>
    <td width="50%">
      <h3>👥 원격결제</h3>
      <p>
        결제 요청자와 승인자를 분리하여
        보호자가 대신 온라인 결제를 승인할 수 있는 기능을 제공합니다.
      </p>
    </td>
    <td width="50%">
      <h3>🤝 더치페이</h3>
      <p>
        대표자 가승인 후 참여자별 결제를 진행하여 
        각 참여자가 자신의 카드 혜택을 극대화합니다.
      </p>
    </td>
  </tr>
</table>
<br>

## 📱 시연 영상 


<br>

## 🏛️ 시스템 아키텍처
```text
Pay App
    │
    ▼
API Gateway
    │
    ▼
payment-service
    │
    ├── OpenFeign → auth-service
    │                 (PIN 검증)
    │
    ├── OpenFeign → card-service
    │                 (카드 조회)
    │
    ├── OpenFeign → recommendation-service
    │                 (혜택 계산)
    │
    ├── OpenFeign → pg-payment-service
    │                 (승인 요청)
    │
    └── Kafka
          ├── notification-service
          └── recommendation-service

notification-service
    └── Firebase FCM
```
### 인프라 아키텍처
<img width="2948" height="1768" alt="--8 drawio" src="https://github.com/user-attachments/assets/ede2e234-9853-4043-b61c-9608870f15e4" />


<br>
<br>

## 🛠️ 기술 스택
#### Frontend & Mobile
[![Frontend](https://skillicons.dev/icons?i=react,ts,tailwind,firebase)](https://skillicons.dev)

#### Backend
[![Backend](https://skillicons.dev/icons?i=java,spring,mysql,redis,kafka)](https://skillicons.dev)

#### AI/OCR
[![AI](https://skillicons.dev/icons?i=py,fastapi)](https://skillicons.dev)

#### Infra & DevOps
[![Infra](https://skillicons.dev/icons?i=docker,kubernetes,terraform,jenkins,github,aws,gcp)](https://skillicons.dev)

#### Monitoring
[![Monitoring](https://skillicons.dev/icons?i=prometheus,grafana,elasticsearch,kibana)](https://skillicons.dev)


<br>

## 🗄️ ERD
#### ERD 요약
| DB | 주요 테이블 |
|------|--------|
| auth_db | auth_users, friend_relations |
| card_db | card_registered, card_benefit | 
| recommend_db | recommend_mcc_mapping, recommend_results | 
| payment_db | payment_orders, payemnt_events, payment_remote_requests, dutch_pay_sessions | 
| pg_payment_db | pg_payment_group, pg_payment_ledger |
| pg_auth_db | pg_admin_accounts, pd_admin_audit_logs |
| pg_merchant_db | pg_settlements, pg_merchants |
| notification_db | notifications, notification_preferences |
| simulator_db | simulator_card, simulator_card_token | 
| pg_billing_db | pg_billing_keys |
<img width="5730" height="3482" alt="v3 (1)" src="https://github.com/user-attachments/assets/a2d49c74-53f3-4984-b818-18e036ccf4f3" />
<br>
<a href="https://www.erdcloud.com/d/DpXuj4uDqWf8h7THW">ERD</a>

<br>
<br>

## 📦 레포지토리 구성
| 레포지토리 | 설명 | 메인 담당 |
|-----------|------------------|-------|
| [api-gateway](https://github.com/ErumPay/api-gateway) | BFF + JWT 인증 + SSE + 라우팅 | 하지혁 |
| [auth-service](https://github.com/ErumPay/auth-service) | 회원 인증 및 인가 서비스 | 고민균 |
| [card-service](https://github.com/ErumPay/card-service) | 사용자 카드 등록 및 관리  | 이준혁 | 
| [recommendation-service](https://github.com/ErumPay/recommendation-service) | 결제 상황에 가장 적합한 카드를 추천 | 이준혁 |
| [card-ocr-service](https://github.com/ErumPay/card-ocr-service) | 카드 이미지 OCR 처리 | 이준혁 |
| [payment-service](https://github.com/ErumPay/payment-service) | 결제 도메인의 핵심 오케스트레이션 담당 | 김다윤, 나영은 |
| [notification-service](https://github.com/ErumPay/notification-service) | Kafka 이벤트 기반 알림 서비스 | 은종혁 |
| [pg-payment-service](https://github.com/ErumPay/pg-payment-service) | PG 결제 처리 및 원장 관리 | 은종혁 |
| [pg-auth-service](https://github.com/ErumPay/pg-auth-service) | PG 관리자 인증  | 나혜빈 |
| [pg-merchant-service](https://github.com/ErumPay/merchant-service) | 가맹점 정보 관리 | 조보름 |
| [billing-key-service](https://github.com/ErumPay/billing-key-service) | 정기결제 및 간편결제를 위한 빌링키 발급 | 하지혁 |
| [card-simulator-service](https://github.com/ErumPay/card-simulator-service) | 테스트용 카드사 서비스 | 하지혁 |
| [mobile-app](https://github.com/ErumPay/mobile-app) | React Native 기반 사용자 모바일 애플리케이션 | 조보름, 나혜빈 |
| [web](https://github.com/ErumPay/web-client) | React 기반 가맹점 / PG 관리자 웹 애플리케이션 | 조보름, 나혜빈 |
| [sdk](https://github.com/ErumPay/erumpay-sdk) | 외부 가맹점 연동을 위한 SDK | 나영은 |
| [mcp-server](https://github.com/ErumPay/erumpay-mcp-server) | AI Agent와 ErumPay 서비스 연동을 위한 MCP 서버 | 나영은 |
| [infra](https://github.com/ErumPay/erumpay-infra) | AWS 기반 클라우드 인프라 구축 및 GitOps 기반 CI/CD 운영 환경 관리 | 나영은, 은종혁 |


<br>

## 👥 팀원
| 이름 | GitHub | 담당 |
|-----------|-----------|-----------|
|고민균| [고민균](https://github.com/alsrbs915-jpg) | BE, FE |
|김다윤| [김다윤](https://github.com/kdayun) | BE, FE |
|나영은| [나영은](https://github.com/Yeongeunn) | BE, Infra |
|나혜빈| [나혜빈](https://github.com/nahyebin) | BE, FE |
|이준혁| [이준혁](https://github.com/LeeJuneHyuck) | BE, FE |
|은종혁| [은종혁](https://github.com/0chotona) | BE, Infra |
|조보름| [조보름](https://github.com/choboreum) | BE, FE |
|하지혁| [하지혁](https://github.com/hajihyeok) | BE |

<br>

## 🤝 협업 방식
- 브랜치 전략: Git Flow (```main```, ```develop```, ```feature```)
- 커밋 컨벤션: feat / fix / refactor 등 통일
- MSA 에러 응답 표준화 (```status```, ```error```, ```code```, ```reason```, ```message``` 구조 통일)
- 일정 관리: Notion, Jira
- 실시간 소통: Discord
- 통합 테스트: Docker Compose로 전체 6개 서비스 로컬 통합 테스트 후 EKS 배포

<br>
<br>

## 📑 발표 자료
