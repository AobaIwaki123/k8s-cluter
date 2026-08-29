# LLM GPU 推論基盤 (6-llm-gpu-service)

WSL2 / NVIDIA GPU (GeForce GTX 1650 Ti) 上で稼働するローカル LLM 推論基盤（`llama-server` / `Meta Llama-3.2-3B-Instruct`）を k0s クラスタへ統合し、OpenAI 互換 API として公開するためのマニフェスト集です。

---

## 構成概要

- **GPU ホスト LAN IP**: `192.168.11.15`
- **推論 API ポート**: `8080` (OpenAI 互換 `/v1/chat/completions`)
- **ベンチマーク メタデータ API ポート**: `8088` (`/api/benchmarks`)
- **クラスタ内 DNS**: `http://llm-gpu-service.ai.svc:8080`

---

## デプロイ手順 (ArgoCD)

```bash
kubectl apply -f argocd/llm-gpu-service.app.yaml
```

または手動適用:

```bash
kubectl apply -f manifests/namespace.yaml
kubectl apply -f manifests/service.yaml
kubectl apply -f manifests/ingress.yaml
```

---

## クラスタ内 Pod からの利用例 (Python)

```python
from openai import OpenAI

client = OpenAI(
    base_url="http://llm-gpu-service.ai.svc:8080/v1",
    api_key="not-needed"
)

response = client.chat.completions.create(
    model="default-llm",
    messages=[{"role": "user", "content": "こんにちは！"}],
)
print(response.choices[0].message.content)
```
