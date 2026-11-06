# AppsVerything 웹사이트

Play Console 조직 계정의 "조직 웹사이트"로 쓰는 정적 사이트. 빌드 없이 HTML 그대로 배포한다.

| 파일 | 역할 |
|---|---|
| `index.html` | 이력서 (AI 경험, 경력, 도구, 교육과 병역, 연락처). Hallmark로 디자인 |
| `tokens.css`, `base.css` | 이력서 페이지의 색·글꼴·간격 토큰과 기본 규칙 (Hallmark Ultraviolet 테마, night 컬러웨이). 색은 여기서만 바꾼다 |
| `apps/index.html` | 사업자 소개 + 앱 목록 (`/apps/`) |
| `privacy/<앱>.html` | 앱별 개인정보처리방침 (스토어의 개인정보처리방침 URL) |
| `app-ads.txt` | AdMob 판매자 인증. **Play에 등록한 개발자 웹사이트 도메인의 루트**에 있어야 한다 |
| `images/` | 앱 아이콘 (256px) |

## 사업자 정보
- 상호: AppsVerything / 문의: contact@appsverything.com (사이트 도메인과 같은 도메인 — Play Console 요건)
- 바꿀 때는 `index.html`, `apps/index.html`, `privacy/*.html`을 같이 바꾼다
- `{시행일}`(방침)은 그 앱이 스토어에 공개되기 직전에 직접 채운다

## 앱 추가
1. `apps/index.html`의 `<article class="app">` 하나를 복사해 이름·설명·링크를 바꾼다
2. 아이콘: `sips -Z 256 <원본.png> --out images/<앱>.png`
3. 방침이 있으면 `privacy/<앱>.html`로 둔다 (`apps/`에서는 `../privacy/`로 링크)
4. 이력서 `index.html`에는 앱 목록이 없고 "출시한 앱 보기" 버튼으로 `apps/`에 연결한다. 앱 수가 바뀌면 "앱 7개"라고 적힌 세 곳을 같이 고친다: `<meta name="description">`, AI 경험의 "AI 에이전트로 앱 출시" 줄, 경력의 AppsVerything 항목 (`grep -n "앱 7개" index.html`로 찾기)

## 배포 (Vercel)
1. Vercel → New Project → 이 저장소 → Framework Preset `Other`, 빌드 명령 없음
2. Settings → Domains에 가진 도메인 추가 → 안내대로 DNS 레코드 입력 (도메인 업체 화면에서 사용자가 직접)
3. 확인: `curl -sI https://<도메인>/` 200, `curl -s https://<도메인>/app-ads.txt` 내용 일치
