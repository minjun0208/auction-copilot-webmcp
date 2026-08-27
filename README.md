# AuctionCopilot — WebMCP 협업 데모

사람이 목표를 말하면, 에이전트가 탐색·비교·시뮬레이션을 수행하는 **단일 파일 WebMCP 데모**입니다.
"리스트 + 상세 + 비교 + 추천 + 시뮬레이션" 6개 툴은 특정 서비스 전용이 아니라, 데이터 소스만 바꾸면
부동산 경매·중고장비·B2B 조달에 재사용되는 패턴입니다.

**Live demo:** https://minjun0208.github.io/auction-copilot-webmcp/

> Human sets the goal; the agent explores, compares, and simulates. Six reusable WebMCP tools
> ("list + detail + compare + recommend + simulate") for any auction/marketplace.

## 등록되는 WebMCP 툴 (6)

| Tool | 역할 |
|---|---|
| `search_listings` | 조건 검색 + 목록 갱신 |
| `get_listing` | 매물 상세 조회 + 선택 표시 |
| `estimate_value` | 연식·주행·상태 기반 가치 추정 (read-only) |
| `compare_lots` | 다중 매물 비교 + 비교 트레이 갱신 |
| `recommend_strategy` | 예산·용도·리스크 기반 Top 3 + 대안 |
| `simulate_bid` | 입찰가별 낙찰확률·기대이익 계산 |

모든 `execute`는 화면의 실제 상태(DATA/state/DOM)를 조작합니다 — mock 응답이 아닙니다.
반환은 `{content:[{type:'text',text}]}` 형식으로 래핑됩니다 (WebMCP `execute` 반환형은 `Promise<any>`라 필수는 아니며, 에이전트·인스펙터가 일관되게 읽도록 하는 편의 래핑입니다).

## 직접 테스트하기 (Chrome 149+)

1. `chrome://flags` → `#enable-webmcp-testing` + `#devtools-webmcp-support` → **Enabled** → 재시작
2. 라이브 URL 접속 → 헤더 배지가 **"WebMCP 6/6 tools registered"** (초록)인지 확인
3. `F12` → **Application** → **WebMCP** → Available Tools 6개 확인
4. `recommend_strategy` 선택 → 아래 입력 → **Run tool**

```json
{ "budgetManwon": 2000, "purpose": "가족", "riskTolerance": "낮음" }
```

→ 02 패널에 Top 3가 렌더링되고, 하단 활동 로그에 `에이전트` 태그로 기록되면 정상입니다.

## 주의

모든 차량·수치·추정식·확률은 데모용 임의값이며 실제 투자·입찰 판단의 근거가 아닙니다.

## License

MIT
