# 🚀 Railway 배포 가이드

## 필수 환경 변수 설정

Railway 대시보드에서 다음 환경 변수들을 설정해야 합니다:

### Firebase 설정
- `FIREBASE_SERVICE_ACCOUNT_KEY`: Firebase 서비스 계정 JSON 키 (문자열로 변환)
- `FIREBASE_PROJECT_ID`: Firebase 프로젝트 ID
- `FIREBASE_AUTH_EMULATOR_HOST`: (선택) 로컬 개발용

### Google AI 설정
- `GOOGLE_AI_API_KEY`: Google Generative AI API 키
- `GOOGLE_APPLICATION_CREDENTIALS`: (선택) 서비스 계정 키 파일 경로

### CORS 설정 (프론트엔드 연결용)
- `ALLOWED_ORIGINS`: 허용할 프론트엔드 도메인들 (쉼표로 구분)
  - 예: `http://localhost:5173,https://your-frontend.com`
  - 개발 환경: `http://localhost:5173`
  - 배포 환경: `https://your-frontend-domain.com`

### 기타 설정
- `PORT`: Railway에서 자동 설정됨
- `NODE_ENV`: `production` (자동 설정)

## 배포 단계

1. **Railway CLI 설치**
   ```bash
   npm install -g @railway/cli
   ```

2. **로그인 및 프로젝트 연결**
   ```bash
   railway login
   railway link
   ```

3. **환경 변수 설정**
   - Railway 대시보드 → Variables 탭
   - 위의 환경 변수들을 추가
   - **중요**: `ALLOWED_ORIGINS`에 프론트엔드 도메인 추가

4. **배포**
   ```bash
   railway up
   ```

## CORS 설정 예시

### 개발 환경
```
ALLOWED_ORIGINS=http://localhost:5173
```

### 배포 환경 (프론트엔드 도메인이 정해진 후)
```
ALLOWED_ORIGINS=http://localhost:5173,https://your-frontend.com
```

## 주의사항

- `FIREBASE_SERVICE_ACCOUNT_KEY`는 JSON 파일의 내용을 문자열로 변환해서 입력
- `ALLOWED_ORIGINS`에 프론트엔드 도메인을 반드시 추가해야 함
- `requirements.txt`가 루트 디렉토리에 있는지 확인
- 환경 변수 설정 후 재배포 필요
