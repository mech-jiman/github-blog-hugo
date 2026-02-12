---
title: "Next.js 15: 최신 React 프레임워크 완벽 가이드"
date: 2026-02-12T16:20:00+09:00
draft: false
tags: ["JavaScript", "React", "Frontend", "Framework"]
categories: ["Web Framework"]
keywords: ["Next.js tutorial", "React framework", "SSR", "SEO", "Vercel"]
description: "Next.js 15의 핵심 기능과 개발 방법을 완벽하게 설명합니다. 서버 사이드 렌더링, 파일 기반 라우팅, 최적화된 빌드까지 한 번에 배우세요."
---

## Next.js란 무엇인가?

Next.js는 **Vercel**에서 개발한 React 기반 프레임워크입니다. 정적 사이트 생성(SSG), 서버 사이드 렌더링(SSR), 증분 정적 재생성(ISR) 등 다양한 렌더링 방식을 지원하여 SEO와 성능을 최적화합니다.

### 핵심 장점

- 🚀 **서버 사이드 렌더링**: SEO 친화적인 웹사이트 구축
- 📦 **자동 코드 스플리팅**: 번들 크기 최적화
- 🎨 **파일 기반 라우팅**: 직관적인 URL 구조
- ⚡ **이미지 최적화**: 자동 WebP 변환 및 레이지 로딩
- 🔄 **증분 정적 재생성**: 정적 + 동적 렌더링의 장점 결합

## 설치 방법

```bash
# 새 프로젝트 생성
npx create-next-app@latest my-app

# 프로젝트 디렉토리로 이동
cd my-app

# 개발 서버 시작
npm run dev
```

## 기본 프로젝트 구조

```
my-app/
├── app/              # App Router (Next.js 13+)
│   ├── page.tsx      # 메인 페이지
│   ├── layout.tsx    # 공통 레이아웃
│   └── globals.css   # 글로벌 스타일
├── public/           # 정적 파일
├── package.json
└── next.config.js
```

## 첫 번째 페이지 만들기

`app/page.tsx` 파일을 생성하면 자동으로 라우팅됩니다:

```tsx
// app/page.tsx
export default function Home() {
  return (
    <main>
      <h1>안녕, Next.js!</h1>
      <p>첫 번째 Next.js 페이지입니다.</p>
    </main>
  );
}
```

## 데이터 패칭

### 서버 컴포넌트 (기본)

```tsx
// app/posts/page.tsx
async function PostsPage() {
  // 서버 측에서 데이터 패칭
  const res = await fetch('https://api.example.com/posts');
  const posts = await res.json();

  return (
    <ul>
      {posts.map(post => (
        <li key={post.id}>{post.title}</li>
      ))}
    </ul>
  );
}

export default PostsPage;
```

### 클라이언트 컴포넌트

```tsx
'use client';

import { useState } from 'react';

export function Counter() {
  const [count, setCount] = useState(0);

  return (
    <button onClick={() => setCount(count + 1)}>
      클릭: {count}
    </button>
  );
}
```

## API 라우트

Next.js에서 REST API를 간단하게 만들 수 있습니다:

```tsx
// app/api/hello/route.ts
import { NextResponse } from 'next/server';

export async function GET() {
  return NextResponse.json({ message: 'Hello, API!' });
}
```

## 정적 사이트 생성(SSG)

```tsx
// app/blog/[slug]/page.tsx
// 빌드 시점에 정적 페이지 생성
export async function generateStaticParams() {
  const posts = await getPosts();
  return posts.map(post => ({ slug: post.slug }));
}

export default function BlogPost({ params }: { params: { slug: string } }) {
  return <div>Post: {params.slug}</div>;
}
```

## 증분 정적 재생성(ISR)

```tsx
// 60초마다 재검증
export const revalidate = 60;

export default function Post({ params }: { params: { slug: string } }) {
  return <div>ISR Post: {params.slug}</div>;
}
```

## 최적화 팁

### 1. 이미지 최적화

```tsx
import Image from 'next/image';

export default function Page() {
  return (
    <Image
      src="/photo.jpg"
      alt="사진"
      width={500}
      height={300}
      priority // LCP 이미지
    />
  );
}
```

### 2. 폰트 최적화

```tsx
import { Inter } from 'next/font/google';

const inter = Inter({ subsets: ['latin'] });

export default function RootLayout({ children }) {
  return (
    <html lang="ko">
      <body className={inter.className}>{children}</body>
    </html>
  );
}
```

### 3. 메타 태그 설정

```tsx
import { Metadata } from 'next';

export const metadata: Metadata = {
  title: 'Next.js Tutorial',
  description: 'Next.js 완벽 가이드',
  openGraph: {
    title: 'Next.js Tutorial',
    description: 'Next.js 완벽 가이드',
  },
};
```

## 배포 방법

### Vercel (추천)

```bash
# Vercel CLI 설치
npm i -g vercel

# 배포
vercel
```

### Docker

```dockerfile
# Dockerfile
FROM node:20-alpine
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build
EXPOSE 3000
CMD ["npm", "start"]
```

```bash
# Docker 빌드 및 실행
docker build -t nextjs-app .
docker run -p 3000:3000 nextjs-app
```

## 관련 도구

- **Vercel**: [클라우드 배포 플랫폼](https://vercel.com) (추천)
- **DigitalOcean**: [개발자 친화적 클라우드](https://www.digitalocean.com/?refcode=example)
- **Railway**: [빠른 배포](https://railway.app)
- **GitHub**: [소스 코드](https://github.com/vercel/next.js)

## 결론

Next.js는 React 개발자를 위한 **완벽한 프레임워크**입니다. SEO, 성능, 개발자 경험 모든 면에서 우수한 선택입니다.

🚀 **지금 시작하고 프로젝트를 배포해보세요!**

---

*이 포스트는 [GitHub API](https://api.github.com)에서 자동으로 생성되었습니다.*
