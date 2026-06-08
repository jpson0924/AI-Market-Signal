# AI Monitoring Desk 배포 가이드

이 앱을 매일 아침 자동 갱신되는 공개 웹 대시보드로 쓰려면 GitHub Pages와 GitHub Actions를 사용합니다.

## 1. GitHub 저장소 만들기

1. GitHub에서 새 repository를 만듭니다.
2. 이 프로젝트 폴더를 GitHub Desktop으로 열고 `Publish repository`를 누릅니다.
3. 공개 공유가 목적이면 repository를 `Public`으로 두는 것이 가장 단순합니다.

터미널에서 `git`이 Xcode 라이선스 문제로 막히는 경우 GitHub Desktop을 쓰면 더 편합니다.

## 2. GitHub Pages 켜기

1. GitHub repository로 이동합니다.
2. `Settings > Pages`로 들어갑니다.
3. `Build and deployment`의 `Source`를 `GitHub Actions`로 선택합니다.

## 3. 첫 배포 실행

1. repository의 `Actions` 탭으로 이동합니다.
2. `Daily AI Monitoring Desk` 워크플로를 선택합니다.
3. `Run workflow`를 누릅니다.

실행되면 아래 작업이 자동으로 진행됩니다.

- `node scripts/update-agenda-data.mjs` 실행
- `agenda-data.js`, `agenda-data.json`, `history/YYYY-MM-DD.json` 갱신
- 최신 정적 파일을 GitHub Pages로 배포

## 4. 공유 URL

배포가 끝나면 GitHub Pages URL은 보통 아래 형식입니다.

```text
https://<github-id>.github.io/<repository-name>/
```

이 URL은 다른 사람이 일반 브라우저에서 열 수 있습니다.

## 5. 매일 자동 갱신

`.github/workflows/daily-update-and-deploy.yml`은 매일 `08:00 KST`에 실행되도록 설정되어 있습니다.

```yaml
schedule:
  - cron: "0 23 * * *"
```

GitHub Actions의 cron은 UTC 기준이라 `23:00 UTC`가 한국시간 다음 날 `08:00 KST`입니다.

## 6. 수동 갱신

급하게 최신 뉴스로 다시 갱신하고 싶으면 GitHub의 `Actions > Daily AI Monitoring Desk > Run workflow`를 누르면 됩니다.
