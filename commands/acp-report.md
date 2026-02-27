---
description: ACP 수익 및 고객 현황 보고 (/orion:acp-report)
---

# /orion:acp-report

Orion ACP 서비스의 수익, 고객, 서비스별 성과를 분석하고 개선 포인트를 제시한다.

## Step 1: 완료된 job 전체 조회

```bash
cd /root/.openclaw/workspace/skills/virtuals-protocol-acp
timeout 20 npx tsx bin/acp.ts job completed --json 2>&1 | python3 -c "
import json, sys
from collections import Counter
data = json.load(sys.stdin)
jobs = data.get('jobs', [])
MY_WALLET = '0x6896dcaa787b120bf41b5066a2a3f78ca56cce13'
ext = [j for j in jobs if j.get('clientAddress','').lower() != MY_WALLET]
services = Counter(j.get('serviceId','unknown') for j in ext)
clients = Counter(j.get('clientAddress','')[:10] for j in ext)
print(f'외부 job 총계: {len(ext)}건')
print(f'서비스별: {dict(services)}')
print(f'고객 수: {len(clients)}명')
print(f'재구매 고객: {[(k,v) for k,v in clients.items() if v>1]}')
"
```

## Step 2: 고객 리스트 파일 확인

```bash
cat /root/.openclaw/workspace/memory/acp-customer-list.md 2>/dev/null || echo "파일 없음"
```

## Step 3: 셀러 성공률 확인

```bash
cd /root/.openclaw/workspace/skills/virtuals-protocol-acp
timeout 15 npx tsx bin/acp.ts profile show --json 2>&1 | python3 -c "
import json, sys
data = json.load(sys.stdin)
print(json.dumps(data.get('offerings', []), indent=2, ensure_ascii=False))
" 2>/dev/null
```

## 보고 포맷

```
💰 Orion ACP 수익 보고 [날짜]

📦 외부 job: N건 / 고객 N명
💵 추정 수익: $X.XX

서비스별 수요:
  1위: [서비스명] - N건
  2위: [서비스명] - N건
  ...

재구매 고객: N명

📈 개선 포인트:
  - [가장 팔리는 서비스 집중 여부]
  - [업셀 기회]
  - [성공률 이슈]

🎯 다음 액션: [구체적 제안 1개]
```

## 분석 기준 (acp-sales.md 참조)
- 재구매율 높은 서비스 → 품질 유지 우선
- btc_direction 구매자 → btc_signal_pack 업셀 시도 여부 확인
- 성공률 80% 미만 → 실패 원인 분석 필요
