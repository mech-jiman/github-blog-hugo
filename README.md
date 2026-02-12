# GitHub Projects Blog

GitHub 인기 프로젝트를 자동으로 소개하는 **Hugo 정적 사이트** 블로그입니다.

## 🎯 특징

- 🤖 **AI 자동화**: OpenAI GPT-4o-mini로 한국어 콘텐츠 생성
- 🔥 **인기 프로젝트**: GitHub Trending API로 자동 수집
- 🎨 **Hugo Awesome 테마**: 깔끔한 디자인 (다크/라이트 모드)
- 🚀 **GitHub Pages**: 무료 HTTPS 자동 배포
- 💰 **수익화**: 개발자 친화적 제휴 링크

## 🏗️ 기술 스택

| 구성 요소 | 기술 |
|-----------|-------|
| CMS | Hugo (정적 사이트 생성기) |
| 콘텐츠 생성 | OpenAI GPT-4o-mini (예정) |
| 데이터 소스 | GitHub API |
| 배포 | GitHub Pages + GitHub Actions |
| 테마 | Hugo Blog Awesome |

## 📦 로컬 개발

```bash
# 저장소 클론
git clone https://github.com/jiman/github-blog-hugo.git
cd github-blog-hugo

# Hugo 서버 실행
hugo server

# 브라우저에서 접속
# http://localhost:1313
```

## ✍️ 새 포스트 작성

```bash
# 새 포스트 생성
hugo new posts/your-post-title.md

# content/ko/posts/your-post-title.md 파일 수정
```

### 포스트 프론트매터 예시

```yaml
---
title: "포스트 제목"
date: 2026-02-12T16:20:00+09:00
draft: false
tags: ["tag1", "tag2"]
categories: ["Frontend"]
keywords: ["keyword1", "keyword2"]
description: "메타 설명"
---

콘텐츠 내용...
```

## 🚀 배포

### 자동 배포

`main` 브랜치에 푸시하면 자동으로 GitHub Pages에 배포됩니다.

```bash
git add .
git commit -m "Add new post"
git push origin main
```

### 수동 배포

```bash
# 정적 사이트 빌드
hugo --minify

# public/ 디렉토리를 GitHub Pages에 배포
```

## 📊 수익화

이 블로그의 수익은 다음 제휴 프로그램에서 발생합니다:

### 제휴 링크

- **Vercel**: React/Next.js 프로젝트 배포
- **DigitalOcean**: 클라우드 서버 호스팅
- **Railway**: 빠른 배포 플랫폼
- **JetBrains**: IDE 개발 도구

### 수익 목표

- Week 4: 100+ 방문자/일
- Week 8: $100-200 MRR
- Week 12: $300-500 MRR

## 🤖 자동화 시스템 (개발 중)

### 워크플로우

```
GitHub API (인기 프로젝트)
    ↓
OpenAI (콘텐츠 생성)
    ↓
Markdown 파일 생성
    ↓
Hugo 빌드
    ↓
GitHub Actions 자동 배포
```

### 자동화 기능

1. **GitHub Trending 수집**: 매 6시간마다 인기 프로젝트 수집
2. **AI 콘텐츠 생성**: GPT-4o-mini로 한국어 블로그 작성
3. **SEO 최적화**: 고 CPC 키워드 추출, 메타 태그 생성
4. **제휴 링크 삽입**: 자연스러운 배치로 수익화

## 📁 프로젝트 구조

```
github-blog-hugo/
├── content/
│   └── ko/
│       ├── posts/       # 블로그 포스트
│       └── about.md     # 소개 페이지
├── themes/
│   └── hugo-blog-awesome/  # 테마 (서브모듈)
├── .github/workflows/
│   └── deploy.yml    # GitHub Actions
├── assets/            # 정적 자원
├── hugo.toml         # Hugo 설정
└── public/            # 빌드 결과 (자동 생성)
```

## 🌐 라이브 사이트

[https://jiman.github.io/github-blog-hugo/](https://jiman.github.io/github-blog-hugo/)

## 📝 TODO

- [ ] Spring Boot 자동화 시스템 구축
- [ ] OpenAI API 연동
- [ ] GitHub API 연동
- [ ] 자동화 워크플로우 테스트
- [ ] Google Analytics 연동
- [ ] 제휴 링크 최적화
- [ ] 수익 트래킹 시스템

## 📄 라이선스

MIT

---

*Made with ❤️ by [Jiman](https://github.com/jiman)*
