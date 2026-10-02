# Requirements Analysis Questions

## Sources

- [upstream:intent-statement] `aidlc/spaces/default/intents/260914-liquor-reservation-app/ideation/intent-capture/intent-statement.md`

## Q1. POC에서 구현할 핵심 기능의 범위는 어디까지인가요?

데일리샷 스타일의 주류 예약 앱에서 POC로 검증할 기능을 선택해 주세요.

A. 주류 목록 조회만 (카탈로그 기능)
B. 주류 검색 + 상세 정보 조회
C. 주류 검색 + 예약 기능 (핵심 플로우)
D. 주류 검색 + 예약 + 결제 연동
E. 전체 플로우 (검색, 예약, 결제, 픽업 확인)
X. Other (please specify)

[Answer]: X. 주류 검색, 예약, 결제, 평점 기능 포함

## Q2. 사용자 인증이 필요한가요?

A. 필요 없음 (게스트로 예약 가능)
B. 간단한 회원가입/로그인만
C. 소셜 로그인 (카카오, 네이버 등)
D. 본인 인증 필요 (주류 판매 규정상 성인 인증)
E. 아직 정의되지 않음
X. Other (please specify)

[Answer]: X. 로그인 및 성인 인증 모두 필요

## Q3. 주류 데이터는 어떻게 관리하나요?

A. 하드코딩된 샘플 데이터 사용 (POC용)
B. 로컬 JSON/CSV 파일
C. 자체 데이터베이스 구축
D. 외부 주류 API 연동
E. 아직 정의되지 않음
X. Other (please specify)

[Answer]: C. 자체 데이터베이스 구축

## Q4. 가맹점(리쿼샵) 관련 기능이 POC에 포함되나요?

A. 포함 안 함 (소비자 앱만)
B. 가맹점 목록 조회만
C. 가맹점별 재고 확인
D. 가맹점 관리자 기능 포함
E. 아직 정의되지 않음
X. Other (please specify)

[Answer]: X. 가맹점 관리 기능 포함 필요 - 매장의 가격 부풀리기, 불친절, 잘못된 재고 판매 등에 대한 신고/관리 기능

## Q5. 선호하는 기술 스택이 있나요?

A. 특별히 없음 (추천에 따름)
B. 웹 앱 (React, Vue 등)
C. 모바일 앱 (React Native, Flutter)
D. 네이티브 앱 (iOS Swift, Android Kotlin)
E. 백엔드만 (API 서버)
X. Other (please specify)

[Answer]: C. 모바일 앱 (React Native, Flutter)

## Q6. 알림/푸시 기능이 필요한가요?

A. 필요 없음 (POC에서는 제외)
B. 이메일 알림만
C. SMS 알림
D. 앱 푸시 알림
E. 아직 정의되지 않음
X. Other (please specify)

[Answer]: A. 필요 없음 (POC에서는 제외) 

## Consolidated Summary Confirmation

정리된 요구사항:

- **핵심 기능**: 주류 검색, 예약, 결제, 평점 기능
- **사용자 인증**: 로그인 및 성인 인증 모두 필요
- **데이터 관리**: 자체 데이터베이스 구축
- **가맹점 기능**: 가맹점 관리 기능 포함 (가격 부풀리기, 불친절, 잘못된 재고 판매 신고/관리)
- **기술 스택**: 모바일 앱 (React Native 또는 Flutter)
- **알림**: POC에서는 제외

[Answer]: Looks correct 