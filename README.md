# JMCONNECTED Online AI School — 배포 가이드

## 📦 패키지 구성

```
deploy/
├── index.html         # 메인 웹페이지 (이미지 모두 임베드, 977KB)
├── og_thumbnail.jpg   # 카카오톡/SNS 공유용 썸네일 (1200×630, 138KB)
└── README.md          # 이 가이드
```

`index.html` 한 파일에 모든 디자인, 이미지, CSS, JavaScript가 통합되어 있어
어떤 호스팅에 올려도 동일하게 작동합니다.

---

## 🚀 배포 방법 5가지 (난이도 순)

### ⭐ 1. Netlify Drop (가장 쉬움 · 무료)

1. 브라우저에서 https://app.netlify.com/drop 접속
2. 위 `deploy` 폴더 전체를 페이지에 **드래그 앤 드롭**
3. 30초 후 자동 발급 URL 확인 (예: `dazzling-curie-a1b2c3.netlify.app`)
4. 그 URL이 바로 본인 페이지

**장점**: 가입도 필요 없고, 즉시 HTTPS · 모바일 지원
**단점**: URL이 자동 생성됨 (커스텀 도메인은 회원가입 후 연결 가능)

---

### ⭐ 2. Vercel (가장 깔끔 · 무료)

1. https://vercel.com 가입 (GitHub 계정 추천)
2. 대시보드에서 **Add New → Project → Deploy without Git**
3. `deploy` 폴더 드래그 업로드 → **Deploy** 클릭
4. 약 20초 후 URL 발급 (예: `jmconnected.vercel.app`)
5. Settings → Domains 에서 본인 도메인 연결 가능

**장점**: 빠른 CDN, 자동 SSL, 한국 응답속도 우수
**단점**: 회원가입 필요

---

### ⭐ 3. GitHub Pages (가장 무료에 가까움)

1. https://github.com 가입
2. New Repository 생성 → 이름 `jmconnected-ai-school` (Public)
3. `index.html`과 `og_thumbnail.jpg` 업로드
4. Repository → **Settings → Pages**
5. Source = `main` branch / `/ (root)` 선택 → Save
6. 1~2분 후 URL 발급: `https://[username].github.io/jmconnected-ai-school/`

**장점**: 완전 무료, 영구 유지
**단점**: Git 사용 익숙해야 편함

---

### ⭐ 4. 카페24 / 가비아 / 호스팅케이알 등 한국 호스팅

이미 도메인이 있고 한국 호스팅을 사용 중이라면:

1. **FTP 프로그램** (FileZilla, ALFTP 등) 실행
2. 호스팅사에서 받은 FTP 정보로 접속
3. `public_html` 또는 `www` 폴더로 이동
4. `index.html`과 `og_thumbnail.jpg`를 같은 폴더에 업로드
5. 끝. 본인 도메인 (`jmconnected.kr` 등)으로 접속

**장점**: 본인 도메인 그대로 사용
**단점**: 호스팅 비용 발생

---

### ⭐ 5. Cloudflare Pages (가장 빠른 글로벌 CDN · 무료)

1. https://pages.cloudflare.com 가입
2. **Create a project → Upload assets**
3. `deploy` 폴더 압축 ZIP 업로드
4. 프로젝트 이름 지정 → Deploy
5. URL 발급: `jmconnected.pages.dev`

**장점**: 글로벌 CDN, 무제한 트래픽, 자동 HTTPS
**단점**: 한글 UI 부족

---

## 🔁 배포 후 권장 작업

### A. OG 썸네일 URL 절대 경로로 변경 (소셜 공유 안정성)

배포된 도메인이 정해지면, `index.html`의 OG 메타 태그에서
`./og_thumbnail.jpg` 을 절대 URL로 변경해주세요.

**변경 전:**
```html
<meta property="og:image" content="./og_thumbnail.jpg" />
```

**변경 후 (예시):**
```html
<meta property="og:image" content="https://jmconnected.kr/og_thumbnail.jpg" />
```

수정 위치: HTML 파일 상단 `<head>` 안 3곳
- `og:image`
- `twitter:image`
- `image_src`

### B. 카카오톡 공유 디버거로 캐시 갱신

이미 한 번이라도 카카오톡으로 링크를 공유한 적이 있다면 캐시가 남아있어
새 썸네일이 안 보일 수 있습니다.

1. https://developers.kakao.com/tool/debugger/sharing 접속
2. 배포된 URL 입력 → **디버그**
3. **캐시 초기화** 버튼 클릭
4. 카카오톡에서 새로 링크 공유하면 새 썸네일 적용됨

### C. 페이스북 공유 디버거

https://developers.facebook.com/tools/debug/

URL 입력 후 **Scrape Again** 클릭하면 즉시 갱신됩니다.

---

## ❓ 자주 묻는 질문

### Q1. 도메인은 어떻게 등록하나요?
- **가비아** (https://www.gabia.com) - 한국 가장 보편적
- **Cloudflare Registrar** (https://www.cloudflare.com/products/registrar/) - 가장 저렴
- 보통 `.com`은 연 15,000~20,000원, `.kr`은 22,000원 내외

### Q2. 모아폼 링크는 어떻게 바꾸나요?
`index.html`에서 `https://answer.moaform.com/answers/E66JJL`을 찾아 새 URL로 교체.
총 4곳 (히어로 CTA, 최종 CTA, 모바일 고정 바, QR 카드 링크) 모두 같은 URL이라
**Ctrl + H** 로 일괄 교체 가능합니다.

### Q3. 강사 사진/내용을 나중에 바꿀 수 있나요?
가능합니다. 다만 이미지가 Base64로 임베드되어 있어서 HTML 편집은 어렵습니다.
변경이 필요할 때 알려주시면 새 버전을 만들어 드릴 수 있습니다.

### Q4. 무료 배포는 안정적인가요?
- Netlify, Vercel, Cloudflare Pages는 **월 100GB 트래픽** 무료
- 일반 교육 안내 페이지로는 평생 무료 사용 가능

---

## 📞 문의

배포 중 막히는 부분이 있으면 단계별로 도와드릴 수 있습니다.
