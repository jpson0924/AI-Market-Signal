# 테크 시그널 데스크

Signal Desk 정적 대시보드입니다. 브라우저에서 `index.html`을 열면 `agenda-data.js`를 먼저 읽고, 데이터 파일이 없거나 비어 있으면 `app.js`의 내장 샘플 데이터로 렌더링합니다.

## Daily Update

매일 아침 자동화가 아래 스크립트를 실행해 최신 RSS/테크 블로그 기반 데이터 파일을 갱신합니다.

```bash
node scripts/update-agenda-data.mjs
```

생성 파일:

- `agenda-data.js`: `file://`로 열리는 앱이 바로 읽는 데이터
- `agenda-data.json`: 서버/API 연동용 최신 3일치 JSON
- `history/YYYY-MM-DD.json`: 날짜별 원본 스냅샷

수동으로 최신화한 뒤 열린 브라우저에서 새로고침하면 새 데이터가 반영됩니다.

최근 뉴스 브리핑 데이터는 LLM/API 연동을 염두에 두고 `rank`, `title`, `score`, `reason`, `keywords`, `related_companies`, `sources` 필드를 포함합니다. `sources`는 `{ title, url, media }` 배열이며, 화면에서는 카드 안이 아니라 Deep Dive 모달에서만 원문 링크로 노출됩니다.

## Sources

수집 스크립트는 RSS가 있는 곳은 RSS를 읽고, RSS가 불안정한 국내 포털/매체는 링크 감시 대상으로 노출합니다. 현재 포함된 주요 소스는 AI Times, DigitalToday AI, Bloter IT, ZDNet Korea AI, Naver IT, Daum Digital, The Verge AI, TechCrunch AI, OpenAI News, Google AI Blog, MIT Technology Review, WIRED AI, VentureBeat AI, Hacker News입니다.

키워드별 타임라인에서 기사 제목 카드를 클릭하면 원문이 새 탭으로 열리고, `AI Briefing ⚡` 버튼을 누르면 Deep Dive 브리핑이 열립니다.
