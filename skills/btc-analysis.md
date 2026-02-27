---
description: BTC 시장 분석 시 자동 활성화. 멀티타임프레임 분석 프레임워크와 Orion btc_direction 알고리즘 로직을 포함.
triggers:
  - BTC 분석
  - 비트코인 시황
  - 방향성 판단
  - 신호 확인
---

# BTC 분석 프레임워크 (Orion v2)

## 알고리즘 구조 (btc_direction v2)

### 데이터 소스 (3개, 각 가중치)
| 소스 | 가중치 기본값 | 비고 |
|------|------------|------|
| Technical (RSI/EMA/BB/ADX) | 45% | 항상 활성 |
| Fear & Greed Index | 30% | 극단값 시 1.5× 부스트 |
| Polymarket 예측시장 | 25% | 연결 안 되면 0으로 재분배 |

### 타임프레임
- **5m**: 단기 노이즈 (신뢰도 낮음, 39% 수준)
- **1h**: 주력 판단 기준
- **4h**: 추세 확인용

### 신호 판단 기준
- **UP**: score > +15
- **DOWN**: score < -15
- **NEUTRAL**: -15 ≤ score ≤ +15 (임계값 구간)

### RSI 극단값 오버라이드
- RSI < 25 → 강제 DOWN 보정
- RSI > 78 → 강제 UP 제한 (과열 경고)
- RSI 기준: 4h 캔들 우선

### 시장 국면 감지 (Regime)
- `up`: ADX > 25 + EMA9 > EMA21 > EMA50
- `down`: ADX > 25 + EMA9 < EMA21 < EMA50
- `ranging`: ADX < 20

### 분석 시 체크리스트
1. 현재 BTC 가격 + 24h 변동률
2. RSI (5m / 1h / 4h) → 극단값 체크
3. EMA 배열 상태 (9/21/50) → Regime 판단
4. Fear & Greed 지수 → 극단 공포/탐욕 여부
5. 볼린저밴드 위치 (BB%)
6. 거래량 비율 (현재 / 평균)
7. 최종 score 계산 → UP/DOWN/NEUTRAL

### 보고 포맷
```
📊 BTC 시황 [타임스탬프]
현재가: $XX,XXX | 24h: ±X.XX%

🎯 방향: UP/DOWN/NEUTRAL
신뢰도: XX% | Score: XX.X

📈 기술적: RSI XX | BB XX% | Regime: up/down/ranging
😱 F&G: XX (상태) | 가중치 부스트: 있음/없음

⚠️ 주의사항 (있을 경우)
```

## 해석 원칙

**믿을 것:**
- 멀티타임프레임 일치 신호 (5m + 1h + 4h 모두 같은 방향)
- ADX > 30 + 명확한 EMA 배열
- F&G 극단값 + RSI 과매도/과매수 일치

**주의할 것:**
- 소스 2개 이하 활성 시 (polymarket 없을 때)
- 신뢰도 60% 미만
- 5m 단독 신호

**절대 믿지 말 것:**
- 횡보장(ADX < 20)에서의 방향성 신호
- 신뢰도 50% 이하
- 단일 지표 기반 판단

## 현재 성능 기록
- 정확도: 14.7% (2026-02-26 기준)
- 주 원인: 시장 역행 구간 (F&G 11 = Extreme Fear이지만 가격은 상승)
- 개선 방향: 시장 국면별 가중치 동적 조정
