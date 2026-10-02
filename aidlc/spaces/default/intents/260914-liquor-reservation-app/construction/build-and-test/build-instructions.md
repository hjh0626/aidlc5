# Build Instructions

## 개요

주류예약앱 POC의 빌드 및 실행 지침.

## 사전 요구사항

| 구성요소 | 요구 버전 | 비고 |
|---------|----------|------|
| Node.js | 18.x - 22.x | Node 24.x는 better-sqlite3와 비호환 (C++20 필요) |
| npm | 9.x 이상 | |
| Python | 3.x | better-sqlite3 네이티브 빌드용 |
| C++ Compiler | C++20 지원 필요 | GCC 10+, Clang 10+ |

## 환경 호환성 주의사항

**Node.js 24.x 비호환 문제:**
- `better-sqlite3` 패키지가 Node.js 24.x의 V8 엔진 변경사항과 호환되지 않음
- 에러: `#error "C++20 or later required."` 
- 해결책: Node.js 18.x ~ 22.x 버전 사용 (nvm 권장)

```bash
# nvm으로 Node.js 버전 변경
nvm install 20
nvm use 20
```

## Backend 빌드

### 1. 의존성 설치

```bash
cd backend
npm install
```

**주의사항:**
- `better-sqlite3`는 네이티브 모듈로 컴파일 필요
- 빌드 도구 (python3, make, g++) 필요
- 실패 시 `npm rebuild better-sqlite3` 시도

### 2. 환경 설정

```bash
cp .env.example .env
```

`.env` 파일 설정:
```
PORT=3000
JWT_SECRET=your-secret-key-here
NODE_ENV=development
```

### 3. TypeScript 컴파일

```bash
npm run build
```

출력 디렉토리: `dist/`

### 4. 빌드 검증

```bash
# 컴파일된 파일 확인
ls -la dist/
# 필수 파일: app.js, routes/, services/, repositories/, models/, database/
```

## Mobile 빌드

### 1. 의존성 설치

```bash
cd mobile
npm install
```

### 2. React Native 환경 설정

**iOS (macOS only):**
```bash
cd ios && pod install && cd ..
```

**Android:**
- Android Studio 설치
- SDK, NDK 설정
- `local.properties` 설정

### 3. Metro Bundler 실행

```bash
npm start
```

## 개발 서버 실행

### Backend 개발 모드

```bash
cd backend
npm run dev
```

서버: `http://localhost:3000`

### Mobile 개발 모드

```bash
cd mobile
npm run ios    # iOS
npm run android # Android
```

## 빌드 트러블슈팅

### better-sqlite3 빌드 실패

1. **Node.js 버전 확인**: 18.x ~ 22.x 사용
2. **빌드 도구 설치**:
   ```bash
   # Ubuntu/Debian
   sudo apt-get install python3 build-essential
   
   # macOS
   xcode-select --install
   ```
3. **캐시 정리 후 재설치**:
   ```bash
   rm -rf node_modules package-lock.json
   npm cache clean --force
   npm install
   ```

### TypeScript 컴파일 에러

```bash
# 타입 정의 재설치
npm install --save-dev @types/node @types/express
```

## 빌드 출력물

| 디렉토리 | 설명 |
|---------|------|
| `backend/dist/` | 컴파일된 JavaScript |
| `backend/data/` | SQLite DB 파일 (자동 생성) |
| `mobile/ios/build/` | iOS 빌드 산출물 |
| `mobile/android/app/build/` | Android APK/AAB |
