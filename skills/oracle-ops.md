---
description: Orion 온체인 오라클 운영 관련 내용 처리 시 자동 활성화.
triggers:
  - 오라클
  - oracle
  - 온체인
  - Base 신호
  - push-signals
---

# Orion Oracle 운영 매뉴얼

## 인프라
- 컨트랙트: `0x755184570B80fF04463BFf53D59236F7ad5898E9` (Base Mainnet)
- 배포 지갑: `0x6EdC4f287DCCD7d16733539900Fde92DE3416978`
- 업데이트: 5분마다 자동 (push-signals.mjs)
- 로그: `/root/.openclaw/workspace/orion-oracle/oracle.log`

## 신호 종류 (온체인에 기록되는 것)
- `btc_direction_5m` — 5분봉 방향성
- `btc_direction_1h` — 1시간봉 방향성
- `btc_direction_4h` — 4시간봉 방향성
- `korean_alpha_top_movers` — 한국 시장 상위 변동 종목
- `market_intel_BTCUSDT` — BTC 시장 인텔
- `market_intel_ETHUSDT` — ETH 시장 인텔
- `polymarket_oracle_btc` — 예측시장 BTC 컨센서스
- `whale_alert_all` — 고래 이동 알림

## 상태 확인
```bash
# 최근 로그
tail -20 /root/.openclaw/workspace/orion-oracle/oracle.log

# 온체인 확인
# BaseScan: https://basescan.org/address/0x755184570B80fF04463BFf53D59236F7ad5898E9
```

## 문제 상황 대응

| 상황 | 원인 | 조치 |
|------|------|------|
| TX 실패 | ETH 가스 부족 | jun에게 즉시 보고 (ETH 잔고 0) |
| 신호 캐시 히트만 계속 | 파이프라인 정상 | 정상 동작 |
| push-signals 프로세스 없음 | 크래시 | 확인 후 jun 보고 |

## 주의사항
- ETH 잔고 0 → 가스비 없음 → TX 실패 → **오라클 업데이트 중단**
- 오라클 자동 재시작: **jun 승인 후에만**
- 니모닉/프라이빗키: 절대 로그에 출력하지 않음
