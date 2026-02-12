# GitHub Pages "Site not found" 에러 해결 가이드

## 문제 상황
- 설정: Deploy from a branch
- 브랜치: main
- 에러: Site not found
- 원인: GitHub Pages 캐싱 또는 Hugo 빌드 실패

## 해결 단계

### 1단계: GitHub Actions 실행 로그 확인

```bash
# 최신 workflow 실행 상태 확인
curl -s https://api.github.com/repos/mech-jiman/github-blog-hugo/actions/workflows/deploy.yml/runs | jq -r '.[] | {name, status, conclusion, created_at} | [.conclusion,.status,.name,.created_at] | @tsv' | head -1
```

### 2단계: 로컬에서 Hugo 빌드 테스트

```bash
# 로컬에서 직접 Hugo 빌드
cd /home/jiman/.openclaw/workspace/github-blog-hugo
hugo --minify --logLevel debug

# 빌드 결과 확인
ls -la public/ | head -20
```

### 3단계: GitHub Pages Source 설정 재확인

1. https://github.com/mech-jiman/github-blog-hugo/settings/pages 접속
2. **Source**: `GitHub Actions` ✅
3. **Build and deployment**: `Static files` 선택 (경우에 따라)
4. **Branch**: `main`
5. **Folder**: `/` (root) 또는 `/` (공백)
6. **Custom domain**: (없으면 비워둠)
7. **Save**

### 4단계: 강제 재배포

```bash
# 변경사항 commit 후 push (workflow 트리거)
cd /home/jiman/.openclaw/workspace/github-blog-hugo
echo "Force rebuild at $(date)" > .nojekyll
git add .nojekyll
git commit -m "Force rebuild: $(date)"
git push origin main
```

### 5단계: 캐시 클리어 (필요시)

```bash
# GitHub Pages 캐시 클리어
# 1. https://github.com/mech-jiman/github-blog-hugo/settings/pages 접속
# 2. "About" 메뉴 → "Pages" → "Custom domain"
# 3. "Clear cache" → "Clear cache"
```

## 진행 순서

### 우선 순서 (빠른 해결)
1. ✅ **로컬 Hugo 빌드 테스트**: `hugo --minify`
2. ✅ **public/ 생성 확인**: `ls -la public/`
3. ✅ **GitHub Pages 설정 재확인**: Source, Branch, Folder
4. ✅ **강제 재배포**: `.nojekyll` 추가 후 push
5. ✅ **캐시 클리어**: 필요시

### 2차 순서 (1단계 실패시)
1. ⏳ **GitHub Actions 로그 확인**: workflow 실행 상태
2. ⏳ **수동 Hugo 빌드 및 커밋**: GitHub Actions 워크플로우에서 직접 실행
3. ⏳ **다른 branch로 배포 시도**: `gh-pages` 브랜치로

## 확인 항목

| 항목 | 기대값 | 실제값 | 상태 |
|-------|--------|--------|------|
| **GitHub Actions 실행** | ✅ 성공 | ? | 확인 필요 |
| **Hugo 빌드 (로컬)** | ✅ `public/` 생성 | ? | 확인 필요 |
| **사이트 접속** | ✅ 200 OK | ❌ 404 | 확인 필요 |
| **Source 설정** | `GitHub Actions` | ? | 확인 필요 |
| **Branch 설정** | `main` | ? | 확인 필요 |

## 1단계: 로컬 Hugo 빌드 테스트 (우선 실행)

```bash
# 1. 로컬에서 Hugo 빌드
cd /home/jiman/.openclaw/workspace/github-blog-hugo

# 2. 빌드 실행
hugo --minify --logLevel debug

# 3. 결과 확인
echo "=== Build Results ==="
echo "Public directory:"
ls -la public/ | head -20

echo "=== Checking for index.html ==="
if [ -f "public/index.html" ]; then
    echo "✅ index.html exists"
    head -20 public/index.html
else
    echo "❌ index.html NOT FOUND"
fi

echo "=== Checking for sitemap.xml ==="
if [ -f "public/sitemap.xml" ]; then
    echo "✅ sitemap.xml exists"
else
    echo "⚠️ sitemap.xml NOT FOUND (may be normal for small sites)"
fi

echo "=== Build completed at $(date) ==="
```

### 2단계: GitHub Pages 설정 재확인

1. 저장소 설정 페이지 접속:
   https://github.com/mech-jiman/github-blog-hugo/settings/pages

2. 설정 재확인:
   - Source: `GitHub Actions` ✅
   - Branch: `main` ✅
   - Folder: `/` (root) ✅
   - Build and deployment: `Static files` ✅

3. 문제 해결:
   - Source가 `Deploy from a branch`가 아니라면 변경
   - Folder가 `/github-blog-hugo/`가 아니라면 `/`로 변경

### 3단계: 강제 재배포

GitHub Pages 캐시 문제인 경우 강제 재배포를 시도해볼까요?

```bash
# 변경사항 commit 후 push
cd /home/jiman/.openclaw/workspace/github-blog-hugo
echo "Force rebuild at $(date)" > .nojekyll
git add .nojekyll
git commit -m "Force rebuild: $(date)"
git push origin main
```

## 진행 제안

### 옵션 1: 로컬 Hugo 빌드 테스트 후 보고 (추천)

현재 상태를 먼저 확인하고 보고를 제안하겠습니다.

### 옵션 2: 강제 재배포 (긴급)

사이트가 긴급하게 필요하다면 강제 재배포를 시도해볼까요?

### 옵션 3: GitHub Actions 로그 분석 (심측)

GitHub Actions 실행 로그를 상세히 분석하여 문제 원인을 파악해볼까요?

---

**어떤 옵션을 선택하시겠어요?**
