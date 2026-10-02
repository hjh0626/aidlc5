# Unit Test Instructions

## Test Strategy

**Strategy**: Minimal (POC scope)
**Methodology**: test-after
**Volume**: Requirement-driven tests (1 test per requirement, happy-path floor per component)
**Target**: ~12-15 tests total

## Test Framework Setup

### Backend (Node.js + Express)
- **Framework**: Jest
- **Test Types**: Unit tests
- **Location**: `backend/src/__tests__/`

### Frontend (React Native)
- **Framework**: Jest + React Native Testing Library
- **Test Types**: Component tests
- **Location**: `mobile/src/__tests__/`

## How to Run Tests

### Backend Tests (Stage-level Scoped Command)

```bash
cd backend && npm test -- --testPathPattern="src/__tests__"
```

This command:
- Runs from the backend directory
- Uses Jest's testPathPattern to scope tests to this stage's test files
- Does NOT run project-wide tests from other stages

### Frontend Tests (Stage-level Scoped Command)

```bash
cd mobile && npm test -- --testPathPattern="src/__tests__"
```

## Expected Coverage Targets

Per Minimal test strategy:
- **No explicit coverage floor** (poc scope adds no extra coverage requirement)
- **Happy-path floor**: Each component must have at least 1 happy-path unit test
- **Requirement coverage**: Each FR requirement should have at least 1 verifiable test

## Test Structure

### Backend Test Files

```
backend/src/__tests__/
├── models/
│   └── entities.test.ts         # Data model tests (FR1.1, FR2.1, FR3.2, FR4.1)
├── repositories/
│   └── repositories.test.ts     # Repository tests (FR1.1, FR2.1, FR4.1, FR4.2)
├── services/
│   └── services.test.ts         # Business logic tests (FR1.1, FR2.1, FR4.1, FR4.3, FR5.1)
└── routes/
    └── routes.test.ts           # API endpoint tests (FR1.1, FR2.1, FR2.2, FR4.1, FR4.2, FR5.1)
```

### Frontend Test Files

```
mobile/src/__tests__/
├── components/
│   └── components.test.tsx      # Component render tests (FR1.1, FR2.1, FR4.1)
```

## Mocking/Stubbing Guidance

### Database Mocking
- Use in-memory SQLite for repository tests
- Mock repositories in service tests

### API Mocking
- Use supertest for API endpoint testing
- Mock services in route tests

### React Native Mocking
- Mock navigation with `@react-navigation/native`
- Mock API calls with Jest mock functions

## Test Data Management

### Sample Test Data

```typescript
// User test data
const testUser = {
  email: 'test@example.com',
  password: 'Test1234!',
  name: '테스트유저',
  isAdultVerified: false
};

// Liquor test data
const testLiquor = {
  name: '테스트 위스키',
  brand: '테스트브랜드',
  type: 'whiskey',
  volume: 700,
  alcoholContent: 40,
  price: 50000
};

// Store test data
const testStore = {
  name: '테스트 리쿼샵',
  address: '서울시 강남구 테헤란로 123',
  phone: '02-1234-5678',
  openTime: '10:00',
  closeTime: '22:00'
};

// Reservation test data
const testReservation = {
  userId: 1,
  storeId: 1,
  liquorId: 1,
  quantity: 1,
  pickupDate: '2026-09-15',
  pickupTime: '14:00',
  status: 'pending'
};
```

## Test Assertions

Each test should verify:
1. **Happy path**: Normal operation completes successfully
2. **Return value**: Expected data structure is returned
3. **Side effects**: Database/state changes are correct (where applicable)

## Running Individual Test Suites

```bash
# Run only model tests
cd backend && npm test -- --testPathPattern="models"

# Run only service tests
cd backend && npm test -- --testPathPattern="services"

# Run only route tests
cd backend && npm test -- --testPathPattern="routes"

# Run frontend component tests
cd mobile && npm test -- --testPathPattern="components"
```
