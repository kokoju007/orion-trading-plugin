---
description: ACP 서비스 판매 전략 및 고객 응대 시 자동 활성화. Orion의 12개 서비스 포지셔닝과 업셀 전략 포함.
triggers:
  - ACP 서비스
  - 고객 유입
  - 서비스 판매
  - Orion 서비스
---

# Orion ACP 서비스 운영 전략

## 핵심 원칙
**서비스 1개 집중 > 12개 분산**
- 참고: Ethy (swap 1개) → 113만건 달성
- Orion 현재: 12개 분산 → 외부 매출 9건/$0.87 (개선 필요)

## 서비스 라인업 & 포지셔닝

### 엔트리 (트래픽 유입용)
| 서비스 | 가격 | 역할 |
|--------|------|------|
| btc_direction | $0.01 | 미끼 상품. 써보게 만들기 |
| evaluator | $0.02 | 신뢰도 체크용 |

### 코어 수익 (업셀 타겟)
| 서비스 | 가격 | 포지셔닝 |
|--------|------|---------|
| btc_signal_pack | $0.20 | btc_direction 업셀 ("5배 더 정확") |
| whale_alert | $0.30 | 고래 추적 니즈 타겟 |
| korean_alpha | $0.50 | 한국 독점 데이터 (차별점) |
| polymarket_oracle | $0.50 | 예측시장 데이터 (독점) |
| trading_signal | $0.50 | 종합 트레이딩 신호 |
| agent_consensus_signal | $0.50 | 멀티에이전트 컨센서스 |
| market_intel | $0.15 | 시장 인텔리전스 |

### 번들 (객단가 극대화)
| 서비스 | 가격 | 내용 |
|--------|------|------|
| alpha_bundle | $0.60 | 핵심 알파 패키지 |
| agent_daily_intel | $0.75 | 일일 인텔 (구독 유도) |
| signal_bundle | $1.50 | 전체 패키지 |

## 업셀 경로
```
btc_direction ($0.01)
    ↓ "더 정확한 신호 필요하면"
btc_signal_pack ($0.20)
    ↓ "한국 시장 데이터까지"
alpha_bundle ($0.60)
    ↓ "매일 받고 싶으면"
agent_daily_intel ($0.75)
    ↓ "전부 다"
signal_bundle ($1.50)
```

## 트래픽 전략

### Butler 없이 트래픽 만드는 법 (현재 상황)
1. **Cowork 플러그인 등록** → Claude 유저 자연 유입
2. **블로그/X 포스팅** → @supernovajunn / @kokaju007
3. **ACP 마켓에서 검색 노출** → 키워드: BTC, signal, Korea, alpha
4. **타 에이전트와 협업** → 상호 job 생성으로 노출

### Butler 연결 후 (승인 대기 중)
- Butler = ACP의 게이트키퍼. 연결되면 자동 트래픽 발생
- 최우선 과제. Virtuals 팀 DM 계속 팔로우

## 고객 응대 원칙
- 외부 고객 job 들어오면 **즉시 jun에게 보고**
- 반복 구매 고객은 `memory/acp-customer-list.md` 업데이트
- 실패한 job은 원인 분석 후 핸들러 개선 검토

## 현재 성과 (2026-02-26)
- 외부 매출: 9건 / $0.87
- 플랫폼 표시: Buyers 12명, $3.14, Jobs 48건
- 성공률: 66.67% → 목표 80%+
- 최대 병목: Butler 미연결, 트래픽 부족
