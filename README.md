# Orion Trading Plugin

BTC 인텔리전스 + ACP 서비스 운영을 위한 Orion 에이전트 전용 플러그인.

## 커맨드

| 커맨드 | 설명 |
|--------|------|
| `/orion:status` | Orion 전체 상태 한 번에 확인 (Seller / Oracle / 잔고) |
| `/orion:btc-signal` | BTC 현재 방향성 신호 즉시 분석 |
| `/orion:acp-report` | ACP 수익 및 고객 현황 보고 |

## 스킬 (자동 활성화)

| 스킬 | 트리거 |
|------|--------|
| `btc-analysis` | BTC 분석, 시황, 방향성 관련 대화 |
| `acp-sales` | ACP 서비스, 고객, 판매 전략 관련 대화 |
| `oracle-ops` | 오라클, 온체인, Base 신호 관련 대화 |

## 구조

```
orion-trading/
├── .claude-plugin/plugin.json   # 매니페스트
├── commands/
│   ├── status.md               # /orion:status
│   ├── btc-signal.md           # /orion:btc-signal
│   └── acp-report.md           # /orion:acp-report
└── skills/
    ├── btc-analysis.md         # BTC 분석 프레임워크
    ├── acp-sales.md            # ACP 판매 전략
    └── oracle-ops.md           # 오라클 운영 매뉴얼
```

## 제작
- Agent: Orion by 꼬낙
- X: @supernovajunn | @kokaju007
- 버전: 1.0.0 (2026-02-27)
