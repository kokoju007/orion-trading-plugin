---
description: BTC 현재 방향성 신호 즉시 분석 (/orion:btc-signal)
---

# /orion:btc-signal

btc_direction 알고리즘 기준으로 현재 BTC 방향성을 분석하고 판단 근거와 함께 보고한다.

## Step 1: ACP에서 현재 신호 가져오기

```bash
cd /root/.openclaw/workspace/skills/virtuals-protocol-acp
timeout 20 npx tsx bin/acp.ts serve logs 2>&1 | grep -A5 "btc_direction"
```

## Step 2: 오라클 최신 신호 확인

```bash
tail -20 /root/.openclaw/workspace/orion-oracle/oracle.log | grep -E "(btc_direction|signal|confidence)"
```

## Step 3: 분석 프레임워크 적용

`skills/btc-analysis.md`의 체크리스트 기준으로:
1. 현재 타임프레임별 신호 (5m / 1h / 4h)
2. 신뢰도 비교 → 가장 신뢰할 수 있는 타임프레임 결론
3. 멀티타임프레임 일치 여부
4. 현재 시장 국면 (Regime)
5. 주의사항 (있으면)

## 보고 포맷

```
📊 BTC 방향성 신호 [타임스탬프]

🎯 결론: UP / DOWN / NEUTRAL
신뢰도: XX% | Score: XX.X

타임프레임별:
  5m: [방향] (신뢰도 XX%)
  1h: [방향] (신뢰도 XX%)  ← 주력
  4h: [방향] (신뢰도 XX%)

시장 국면: up/down/ranging
F&G: XX ([상태])

💡 판단: [한 줄 요약]
⚠️ 주의: [있으면]
```
