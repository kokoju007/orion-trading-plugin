---
description: Orion 전체 상태 한 번에 확인 (/orion:status)
---

# /orion:status

Orion 에이전트의 전체 상태를 확인한다. 아래 순서대로 실행하고 결과를 요약 보고한다.

## Step 1: ACP Seller 상태

```bash
cd /root/.openclaw/workspace/skills/virtuals-protocol-acp
timeout 15 npx tsx bin/acp.ts serve logs 2>&1 | tail -10
```

셀러 런타임이 살아있는지, 최근 job이 처리됐는지 확인.

## Step 2: 외부 고객 job 수

```bash
cd /root/.openclaw/workspace/skills/virtuals-protocol-acp
timeout 15 npx tsx bin/acp.ts job completed --json 2>&1 | python3 -c "
import json,sys
data = json.load(sys.stdin)
jobs = data.get('jobs', [])
ext = [j for j in jobs if j.get('clientAddress','').lower() != '0x6896dcaa787b120bf41b5066a2a3f78ca56cce13']
print(f'외부 job: {len(ext)}건')
"
```

## Step 3: 오라클 상태

```bash
tail -5 /root/.openclaw/workspace/orion-oracle/oracle.log
```

마지막 TX가 성공했는지, 시간이 얼마나 됐는지 확인.

## Step 4: 지갑 잔고

```bash
cd /root/.openclaw/workspace/skills/virtuals-protocol-acp
timeout 15 npx tsx bin/acp.ts wallet balance --json 2>&1
```

## 보고 포맷

```
🔭 Orion 상태 보고 [시각]

🤖 ACP Seller: 정상/중단
📦 외부 job: N건 (누적)
⛓️ Oracle: 마지막 업데이트 N분 전
💰 잔고: cbBTC X.XXXXX | USDC $X.XX

⚠️ 이슈: (있으면 기재)
```
