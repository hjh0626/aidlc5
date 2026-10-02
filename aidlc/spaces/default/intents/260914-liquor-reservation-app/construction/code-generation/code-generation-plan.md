# Code Generation Plan

## Overview

**Project**: 주류예약앱 POC (Liquor Reservation App POC)
**Scope**: poc
**Test Strategy**: Minimal (test-after methodology)
**Project Type**: Greenfield

주류 예약 O2O 플랫폼의 핵심 플로우(주류 검색 → 예약 → 결제 → 픽업)를 기술적으로 검증하는 POC 애플리케이션.

## Tech Stack

- **Frontend**: React Native (크로스 플랫폼 iOS/Android)
- **Backend**: Node.js + Express
- **Database**: SQLite (POC용 간단한 로컬 DB)
- **Authentication**: JWT 기반 인증
- **Payment**: PG사 테스트 모드 연동 준비

## Testing Contract

```json
{
  "version": 1,
  "methodology": "test-after",
  "source": "org",
  "ordering": "implement each applicable testable layer, then write and run",
  "scope": "poc",
  "test_strategy": "minimal",
  "project_type": "greenfield",
  "applicable_notes": [
    {
      "layer": "org",
      "text": "We treat tests as a first-class deliverable in every Bolt. The specific\nmethodology (TDD, BDD, ATDD, or classic test-after) is affirmed at\npractices-discovery and recorded in `team.md` under this heading with explicit\n`Methodology` and `Ordering` fields; Code Generation resolves those fields\nindependently from coverage, tooling, and scope notes.\n\nWhen no posture has been affirmed, our default per scope is:\n- **Methodology**: test-after\n- **Ordering**: implement each applicable testable layer, then write and run\n  that layer's tests.\n- `mvp`, `enterprise`, `feature`, `infra`, `classic` add an 80% line-coverage\n  floor and CI execution before merge.\n- `bugfix`, `security-patch` add a targeted regression for the specific\n  bug/vulnerability and require the existing suite to remain green.\n- `express` uses the Minimal strategy: requirement-driven unit tests (one per\n  requirement, with a happy-path floor per component); existing tests remain\n  green.\n- `poc`, `refactor`, `workshop` add no extra new-test floor and require the\n  existing suite to remain green.\n\nThe active `Test Strategy` still applies in every scope and determines test\nvolume/types. Scope floors are additive; they never reduce or replace the\nselected strategy.\n\nBuild and Test verifies defined coverage floors and affirmed quality targets;\nthey may not be weakened to make a step pass.\n\nAffirm a stricter posture in `team.md` if the team commits to one."
    }
  ],
  "obligations": {
    "strategy": "minimal",
    "strategy_volume": [
      "One verifiable test per requirement at the narrowest effective level.",
      "At least one happy-path unit test per component.",
      "Unit tests are the default; a bugfix/security scope floor may require an integration or E2E regression when that is the narrowest level that reproduces the defect."
    ],
    "scope_floor": [
      "Keep the existing test suite green.",
      "This scope adds no extra new-test floor beyond the selected test strategy."
    ],
    "combination_rule": "Apply every selected-strategy obligation and every scope-floor obligation; neither replaces the other, and a targeted scope regression may add the narrowest necessary test type beyond the strategy default."
  },
  "plan_profile": {
    "methodology": "test-after",
    "runner_step": "Bootstrap the minimal test runner/configuration and record the exact unit-scoped command.",
    "runner_ready_before_first_test": true,
    "testable_layers": [
      "Data model / database behavior",
      "Repository / data access",
      "Business logic",
      "API / endpoint",
      "Frontend behavior"
    ],
    "steps": [
      "Project structure and production configuration skeleton.",
      "Bootstrap the minimal test runner/configuration and record the exact unit-scoped command.",
      "Data model / database behavior - implement.",
      "Data model / database behavior - write and run its tests after implementation.",
      "Repository / data access - implement.",
      "Repository / data access - write and run its tests after implementation.",
      "Business logic - implement.",
      "Business logic - write and run its tests after implementation.",
      "API / endpoint - implement.",
      "API / endpoint - write and run its tests after implementation.",
      "Frontend behavior - implement.",
      "Frontend behavior - write and run its tests after implementation.",
      "Environment/build configuration.",
      "Documentation and traceability."
    ]
  },
  "input_sha256": "sha256:c5db1280ba0333b655bcf97bdcaeaa0fd9cc0f50807a6ee879935b8aff3e17e0",
  "contract_sha256": "sha256:116f7b7b60f3495e1f814ea594d44676be223d5d1c91a56d80b1de85a15cd420"
}
```

## Implementation Steps

### Step 1: Project Structure and Configuration
- [x] Create backend project structure (Node.js + Express)
- [x] Create React Native project structure
- [x] Configure TypeScript for both projects
- [x] Setup package.json with dependencies

### Step 2: Test Runner Bootstrap
- [x] Configure Jest for backend testing
- [x] Configure Jest for React Native testing
- [x] Record exact unit-scoped test commands

### Step 3: Data Model / Database - Implementation
- [x] Create SQLite database schema (FR1.1, FR2.1, FR2.2, FR3.1, FR4.1)
  - users table (회원 정보)
  - liquors table (주류 카탈로그)
  - stores table (가맹점 정보)
  - store_inventory table (매장별 재고)
  - reservations table (예약 정보)
  - reviews table (리뷰/평점)
  - payments table (결제 내역)
- [x] Create TypeScript entity models

### Step 4: Data Model / Database - Tests
- [x] Test: User entity creation (FR1.1)
- [x] Test: Liquor catalog query (FR2.1)
- [x] Test: Store inventory check (FR3.2)
- [x] Test: Reservation entity creation (FR4.1)

### Step 5: Repository / Data Access - Implementation
- [x] UserRepository: 사용자 CRUD, 성인인증 상태 확인 (FR1.1, FR1.2)
- [x] LiquorRepository: 주류 검색/필터링/상세 조회 (FR2.1, FR2.2)
- [x] StoreRepository: 가맹점 조회/재고 확인 (FR3.1, FR3.2)
- [x] ReservationRepository: 예약 CRUD/상태 관리 (FR4.1, FR4.2, FR4.3)
- [x] ReviewRepository: 리뷰 작성/조회 (FR2.3, FR3.3)
- [x] PaymentRepository: 결제 내역 관리 (FR5.1, FR5.2)

### Step 6: Repository / Data Access - Tests
- [x] Test: User repository - 회원가입/로그인 (FR1.1)
- [x] Test: Liquor repository - 검색/필터링 (FR2.1)
- [x] Test: Reservation repository - 예약 생성/조회 (FR4.1, FR4.2)

### Step 7: Business Logic - Implementation
- [x] AuthService: 회원가입/로그인/JWT 발급 (FR1.1)
- [x] AdultVerificationService: 성인인증 처리 (FR1.2)
- [x] CatalogService: 주류 검색/필터링 로직 (FR2.1, FR2.2)
- [x] ReviewService: 리뷰/평점 관리 (FR2.3)
- [x] StoreService: 가맹점/재고 관리 (FR3.1, FR3.2, FR3.3)
- [x] ReservationService: 예약 플로우 처리 (FR4.1, FR4.2, FR4.3)
- [x] PaymentService: 결제 처리 (테스트 모드) (FR5.1, FR5.2)

### Step 8: Business Logic - Tests
- [x] Test: AuthService - 로그인/JWT 검증 (FR1.1)
- [x] Test: CatalogService - 검색 로직 (FR2.1)
- [x] Test: ReservationService - 예약 생성/상태 변경 (FR4.1, FR4.3)
- [x] Test: PaymentService - 결제 처리 (FR5.1)

### Step 9: API / Endpoint - Implementation
- [x] POST /api/auth/signup - 회원가입 (FR1.1)
- [x] POST /api/auth/login - 로그인 (FR1.1)
- [x] POST /api/auth/verify-adult - 성인인증 (FR1.2)
- [x] GET /api/liquors - 주류 목록/검색 (FR2.1)
- [x] GET /api/liquors/:id - 주류 상세 (FR2.2)
- [x] GET /api/liquors/:id/reviews - 주류 리뷰 목록 (FR2.3)
- [x] POST /api/liquors/:id/reviews - 리뷰 작성 (FR2.3)
- [x] GET /api/stores - 가맹점 목록 (FR3.1)
- [x] GET /api/stores/:id - 가맹점 상세 (FR3.1)
- [x] GET /api/stores/:id/inventory - 재고 현황 (FR3.2)
- [x] POST /api/stores/:id/report - 신고 (FR3.3)
- [x] POST /api/reservations - 예약 생성 (FR4.1)
- [x] GET /api/reservations - 내 예약 목록 (FR4.2)
- [x] GET /api/reservations/:id - 예약 상세 (FR4.2)
- [x] DELETE /api/reservations/:id - 예약 취소 (FR4.2)
- [x] POST /api/payments - 결제 처리 (FR5.1)
- [x] GET /api/payments - 결제 내역 (FR5.2)
- [x] POST /api/payments/:id/refund - 환불 요청 (FR5.2)

### Step 10: API / Endpoint - Tests
- [x] Test: Auth endpoints - 회원가입/로그인 (FR1.1)
- [x] Test: Liquor endpoints - 검색/상세 (FR2.1, FR2.2)
- [x] Test: Reservation endpoints - 예약 생성/조회 (FR4.1, FR4.2)
- [x] Test: Payment endpoints - 결제 처리 (FR5.1)

### Step 11: Frontend - Implementation
- [x] Navigation 구조 설정 (Bottom Tab + Stack)
- [x] 로그인/회원가입 화면 (FR1.1)
- [x] 성인인증 화면 (FR1.2)
- [x] 홈 화면 - 주류 목록/검색 (FR2.1)
- [x] 주류 상세 화면 (FR2.2, FR2.3)
- [x] 가맹점 목록/상세 화면 (FR3.1, FR3.2)
- [x] 예약 생성 화면 (FR4.1)
- [x] 내 예약 목록 화면 (FR4.2)
- [x] 결제 화면 (FR5.1)
- [x] 마이페이지 (결제 내역, 설정)

### Step 12: Frontend - Tests
- [x] Test: Login component render (FR1.1)
- [x] Test: Liquor list component render (FR2.1)
- [x] Test: Reservation form validation (FR4.1)

### Step 13: Environment / Build Configuration
- [x] Backend environment variables (.env.example)
- [x] React Native environment configuration
- [x] Build scripts and README

### Step 14: Documentation and Traceability
- [x] API documentation
- [x] Setup instructions
- [x] Traceability JSON

## Requirements Traceability

| Requirement | Implementation | Test |
|------------|----------------|------|
| FR1.1 회원가입/로그인 | AuthService, auth endpoints | Step 4, 6, 8, 10 |
| FR1.2 성인인증 | AdultVerificationService | Step 8 |
| FR2.1 주류검색 | CatalogService, liquor endpoints | Step 4, 6, 8, 10 |
| FR2.2 주류상세 | LiquorRepository, endpoints | Step 6, 10 |
| FR2.3 평점/리뷰 | ReviewService | Step 8 |
| FR3.1 가맹점조회 | StoreService, store endpoints | Step 6 |
| FR3.2 재고확인 | StoreRepository | Step 4, 6 |
| FR3.3 가맹점신고 | StoreService | - |
| FR4.1 예약생성 | ReservationService, endpoints | Step 4, 6, 8, 10 |
| FR4.2 예약관리 | ReservationRepository | Step 6, 10 |
| FR4.3 예약상태 | ReservationService | Step 8 |
| FR5.1 결제처리 | PaymentService | Step 8, 10 |
| FR5.2 결제내역 | PaymentRepository | Step 10 |
