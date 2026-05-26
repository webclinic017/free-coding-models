# OVHcloud AI Endpoints — Audit de validité des modèles

**Date de vérification :** 2026-05-26
**Source :** endpoints.ai.cloud.ovh.net / OVHcloud AI docs

---

## Résumé
| Stat | Nombre | Détails |
|------|--------|---------|
| ✅ Confirmés existants | 5 | Qwen3-Coder-30B, gpt-oss-120b, gpt-oss-20b, Meta-Llama-3_3-70B, Qwen3-32B |
| 🗑️ Retiré du catalogue | 1 | Llama-3.1-8B-Instruct (delisted) |
| ⚠️ Config corrigée | 4 | Context window corrections |
| ➕ Nouveaux — à ajouter | 1 | Qwen3.5-397B-A17B (nouveau, tagged "New") |

---

## ✅ Modèles CONFIRMÉS opérationnels

| Model ID | Display Name | ctx sources.js | ctx OVHcloud | Note |
|----------|-------------|---------------|-------------|------|
| `Qwen3-Coder-30B-A3B-Instruct` | Qwen3 Coder 30B MoE | 256k | 256k | ✅ OK |
| `gpt-oss-120b` | GPT OSS 120B | 131k | 131k | ✅ OK |
| `gpt-oss-20b` | GPT OSS 20B | 131k | 131k | ✅ OK |
| `Meta-Llama-3_3-70B-Instruct` | Llama 3.3 70B | 131k | 131k | ✅ OK |
| `Qwen3-32B` | Qwen3 32B | 32k | 32k | ✅ OK |

---

## 🗑️ Modèle RETIRÉ du catalogue

### `Llama-3.1-8B-Instruct` — Llama 3.1 8B
- **Statut :** Retiré du catalogue public (detail page encore accessible mais modèle non listé)
- **Action :** RETIRER de sources.js

---

## ⚠️ Corrections de context window

| Model ID | ctx sources.js | ctx OVHcloud | Correction |
|----------|---------------|-------------|------------|
| `Qwen3.5-9B` | 128k | **262k** | ⚠️ Corriger → 262k |
| `Mistral-Small-3.2-24B-Instruct-2506` | 131k | **128k** | ⚠️ Corriger → 128k |
| `Mistral-Nemo-Instruct-2407` | 128k | **118k** | ⚠️ Corriger → 118k |
| `Mistral-7B-Instruct-v0.3` | 32k | **127k** (extended via RoPE) | ⚠️ Corriger → 127k |

---

## ➕ Nouveaux modèles à ajouter

| Model ID | Display Name | Tier suggéré | CTX | Notes |
|----------|-------------|-------------|-----|-------|
| `Qwen3.5-397B-A17B` | Qwen3.5 397B MoE | S | 262k | 🆕 Tagged "New", fp8, Function calling + Multimodal + Reasoning |

---

## 📝 Modifications à appliquer dans sources.js

### RETIRER

```javascript
['Llama-3.1-8B-Instruct', 'Llama 3.1 8B', 'B', '28.8%', '131k'],
```

### CORRIGER

```javascript
// AVANT → APRÈS
['Qwen3.5-9B', 'Qwen3.5 9B', 'B+', '30.0%', '128k'],  → ['Qwen3.5-9B', 'Qwen3.5 9B', 'B+', '30.0%', '262k'],
['Mistral-Small-3.2-24B-Instruct-2506', 'Mistral Small 3.2', 'B+', '34.0%', '131k'], → ['Mistral-Small-3.2-24B-Instruct-2506', 'Mistral Small 3.2', 'B+', '34.0%', '128k'],
['Mistral-Nemo-Instruct-2407', 'Mistral Nemo', 'B+', '30.0%', '128k'], → ['Mistral-Nemo-Instruct-2407', 'Mistral Nemo', 'B+', '30.0%', '118k'],
['Mistral-7B-Instruct-v0.3', 'Mistral 7B Instruct', 'B', '25.0%', '32k'], → ['Mistral-7B-Instruct-v0.3', 'Mistral 7B Instruct', 'B', '25.0%', '127k'],
```

### AJOUTER

```javascript
['Qwen3.5-397B-A17B', 'Qwen3.5 397B MoE', 'S', '-', '262k'],
```

---

## Sources

- **OVHcloud Supported Models** : [scaleway.com/en/docs/...](https://endpoints.ai.cloud.ovh.net)
- **OVHcloud AI Endpoints** : Public catalog scraped 2026-05-26
