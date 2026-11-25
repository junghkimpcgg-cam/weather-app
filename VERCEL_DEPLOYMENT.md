# Vercel 배포 및 업데이트 가이드

이 문서는 Vercel을 사용하여 날씨 검색 웹사이트를 배포하고 업데이트하는 방법을 설명합니다.

## 목차
1. [초기 배포](#초기-배포)
2. [자동 배포 설정](#자동-배포-설정)
3. [업데이트 방법](#업데이트-방법)
4. [빌드 설정](#빌드-설정)
5. [트러블슈팅](#트러블슈팅)

---

## 초기 배포

### 1단계: Vercel 가입
- [https://vercel.com](https://vercel.com)에 접속
- **Sign Up** 버튼 클릭
- GitHub 계정으로 로그인 (추천) 또는 이메일로 가입

### 2단계: GitHub 리포지토리 연결
1. Vercel 대시보드에서 **Add New...** > **Project** 선택
2. **Import Git Repository** 클릭
3. GitHub 계정 선택 및 인증
4. `weather-app` 리포지토리 선택

### 3단계: 프로젝트 설정
```
Framework Preset: Other (or Next.js if you want to upgrade later)
Root Directory: ./
Build Command: (Leave empty for static sites)
Output Directory: (Leave empty)
Environment Variables: (Optional)
```

### 4단계: 배포
- **Deploy** 버튼 클릭
- 배포 완료까지 기다림 (약 1-2분)
- 배포 완료 후 자동으로 생성된 URL 확인

---

## 자동 배포 설정

### Git Push 시 자동 배포
Vercel은 기본적으로 GitHub 리포지토리와 연결되면 자동으로 배포됩니다.

**자동 배포 작동 방식:**
- `master` 또는 `main` 브랜치에 Push → 프로덕션 배포
- Pull Request 생성 → 프리뷰 배포 (테스트 URL 생성)
- Pull Request 병합 → 프로덕션 배포

---

## 업데이트 방법

### 방법 1: Git으로 자동 배포 (권장) ⭐

#### 로컬에서 변경 후 푸시
```powershell
# 1. 파일 수정
# (index.html, CSS, JavaScript 등 편집)

# 2. 변경 사항 스테이징
git add .

# 3. 커밋
git commit -m "날씨 앱 업데이트: 새로운 기능 추가"

# 4. GitHub에 푸시
git push origin master
```

#### 자동 배포 확인
1. Vercel 대시보드 접속
2. 프로젝트 선택
3. **Deployments** 탭에서 배포 상태 확인
4. 배포 완료 후 웹사이트 접속하여 변경 사항 확인

### 방법 2: Vercel 대시보드에서 수동 배포

1. Vercel 대시보드 접속
2. 프로젝트 클릭
3. 최신 배포 선택 후 **Redeploy** 클릭
4. 재배포 완료 대기

### 방법 3: Vercel CLI 사용

#### Vercel CLI 설치
```powershell
npm install -g vercel
# 또는
scoop install vercel-cli
```

#### 배포
```powershell
# 프로젝트 디렉토리로 이동
cd C:\Users\Claude\Desktop\git_test1

# Vercel에 배포
vercel

# 프로덕션에 배포
vercel --prod
```

---

## 빌드 설정

### 정적 사이트 호스팅 (현재 프로젝트)
이 프로젝트는 HTML/CSS/JavaScript만 사용하므로 별도의 빌드 설정이 필요 없습니다.

Vercel은 자동으로 `index.html`을 감지하고 정적 사이트로 배포합니다.

### 환경 변수 설정 (선택사항)
Vercel 대시보드에서:
1. 프로젝트 선택
2. **Settings** > **Environment Variables**
3. 필요한 환경 변수 추가

현재 프로젝트는 API 키가 필요 없으므로 설정 불필요합니다.

---

## 도메인 설정

### 커스텀 도메인 연결
1. **Settings** > **Domains** 접속
2. **Add Domain** 클릭
3. 도메인명 입력
4. DNS 설정 가이드 따라하기

### 기본 Vercel 도메인
배포 후 자동으로 제공되는 도메인:
```
https://weather-app.vercel.app
```

---

## 트러블슈팅

### 배포 실패
**증상:** 배포가 빨간 ❌ 로 표시됨

**해결방법:**
1. Vercel 대시보드의 **Deployments** 탭에서 실패한 배포 클릭
2. 빌드 로그 확인
3. 에러 메시지 읽기
4. 로컬에서 문제 수정 후 재 Push

### 변경 사항이 반영되지 않음
**해결방법:**
1. GitHub 푸시 완료 확인
2. Vercel 대시보드에서 새로운 배포 대기 (1-2분)
3. 브라우저 캐시 삭제 (Ctrl+Shift+Delete)
4. 프리뷰 URL 대신 실제 도메인 접속

### OpenMeteo API 접근 불가
**원인:** CORS 오류

**해결방법:**
- OpenMeteo API는 공개 API이므로 CORS 설정이 되어있습니다
- 브라우저 콘솔에서 에러 확인
- 네트워크 연결 확인

---

## 모니터링

### 실시간 모니터링
Vercel 대시보드에서 확인할 수 있는 항목:
- **Analytics:** 방문자 수, 성능
- **Logs:** 배포 로그, 에러 로그
- **Deployments:** 배포 이력

### 성능 최적화
- 이미지 최적화 (필요시)
- CSS/JavaScript 최소화
- 캐싱 정책 설정

---

## 요약: 배포 후 업데이트 플로우

```
코드 수정
   ↓
git add .
   ↓
git commit -m "메시지"
   ↓
git push origin master
   ↓
Vercel 자동 배포 (1-2분 대기)
   ↓
배포 완료 → 웹사이트 접속하여 확인
```

**가장 간단한 방법:** Git에 Push하면 Vercel이 자동으로 배포합니다! 🚀

---

## 유용한 링크

- [Vercel 공식 문서](https://vercel.com/docs)
- [Vercel 대시보드](https://vercel.com/dashboard)
- [GitHub 연동 설정](https://vercel.com/docs/concepts/git/vercel-for-github)
- [OpenMeteo API 문서](https://open-meteo.com/en/docs)

---

**Last Updated:** 2026-11-25
