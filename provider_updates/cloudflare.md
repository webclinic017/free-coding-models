# Cloudflare Workers AI — Audit de validité des modèles

**Date de vérification :** 2026-05-26
**Source :** https://developers.cloudflare.com/workers-ai/models/

---

## Résumé
| Stat | Nombre | Détails |
|------|--------|---------|
| ✅ Confirmés existants | 13 | Tous actifs |
| 🗑️ N'existe pas — à retirer | 1 | `gemma-4-31b-it` (jamais existé sur CF) |
| ⚠️ Dépréciation imminente | 1 | `llama-3.1-8b-instruct` (30/05/2026) + contexte réel = 8k |
| ➕ Nouveaux — à ajouter | 1 | `deepseek-r1-distill-qwen-32b` |
| 📝 Config à corriger | 2 | kimi-k2.6 (256k→262k), llama-3.1-8b (128k→8k) |

---

## 🗑️ Modèles à RETIRER

### `@cf/google/gemma-4-31b-it` — Gemma 4 31B
- **Statut :** 404 — Ce modèle **n'a jamais existé** sur Cloudflare
- **Note :** Le seul modèle Gemma 4 sur CF est `gemma-4-26b-a4b-it`
- **Action :** RETIRER immédiatement

---

## ⚠️ Dépréciation imminente

### `@cf/meta/llama-3.1-8b-instruct` — Llama 3.1 8B
- **Dépréciation :** 30/05/2026 (dans 4 jours)
- **Contexte réel CF :** **7,968 tokens (~8k)** — PAS 128k !
- **Double problème :** (1) dépréciation imminente, (2) contexte est SEULEMENT 8k sur CF
- **Action :** RETIRER

---

## ✅ Modèles CONFIRMÉS opérationnels

| Model ID | Display Name | CTX sources.js | CTX Cloudflare | Note |
|----------|-------------|---------------|---------------|------|
| `@cf/moonshotai/kimi-k2.6` | Kimi K2.6 | 256k | **262,144** | ⚠️ Corriger → 262k |
| `@cf/zai-org/glm-4.7-flash` | GLM-4.7-Flash | 131k | 131,072 | ✅ |
| `@cf/openai/gpt-oss-120b` | GPT OSS 120B | 128k | 128,000 | ✅ |
| `@cf/qwen/qwq-32b` | QwQ 32B | 131k | ~131k | ✅ |
| `@cf/nvidia/nemotron-3-120b-a12b` | Nemotron 3 Super | 128k | ~128k | ✅ |
| `@cf/meta/llama-4-scout-17b-16e-instruct` | Llama 4 Scout | 131k | ~131k | ✅ |
| `@cf/qwen/qwen3-30b-a3b-fp8` | Qwen3 30B MoE | 128k | ~128k | ✅ |
| `@cf/qwen/qwen2.5-coder-32b-instruct` | Qwen2.5 Coder 32B | 32k | ~32k | ✅ |
| `@cf/openai/gpt-oss-20b` | GPT OSS 20B | 128k | 128,000 | ✅ |
| `@cf/meta/llama-3.3-70b-instruct-fp8-fast` | Llama 3.3 70B | 128k | ~128k | ✅ |
| `@cf/google/gemma-4-26b-a4b-it` | Gemma 4 26B MoE | 256k | 256,000 | ✅ |
| `@cf/mistralai/mistral-small-3.1-24b-instruct` | Mistral Small 3.1 | 128k | ~128k | ✅ |
| `@cf/ibm/granite-4.0-h-micro` | Granite 4.0 Micro | 128k | ~128k | ✅ |

---

## ➕ Nouveaux modèles à ajouter

| Model ID | Display Name | Tier suggéré | CTX | Notes |
|----------|-------------|-------------|-----|-------|
| `@cf/deepseek-ai/deepseek-r1-distill-qwen-32b` | DeepSeek R1 Distill 32B | A- | 80k | Modèle de raisonnement, contexte 80k |

---

## 📝 Modifications à appliquer dans sources.js

### RETIRER

```javascript
['@cf/google/gemma-4-31b-it',               'Gemma 4 31B',       'A',  '45.0%', '256k'],  // N'existe pas sur CF
['@cf/meta/llama-3.1-8b-instruct',          'Llama 3.1 8B',      'B',  '28.8%', '128k'],  // Dépréciation 30/05 + ctx = 8k
```

### CORRIGER

```javascript
// AVANT
['@cf/moonshotai/kimi-k2.6', 'Kimi K2.6', 'S+', '76.8%', '256k'],
// APRÈS
['@cf/moonshotai/kimi-k2.6', 'Kimi K2.6', 'S+', '76.8%', '262k'],
```

### AJOUTER

```javascript
['@cf/deepseek-ai/deepseek-r1-distill-qwen-32b', 'DeepSeek R1 Distill 32B', 'A-', '45.0%', '80k'],
```

---

## Sources

- **Cloudflare Workers AI Models** : [developers.cloudflare.com/workers-ai/models](https://developers.cloudflare.com/workers-ai/models/)
- Pages individuelles vérifiées : kimi-k2.6, glm-4.7-flash, gpt-oss-120b, gemma-4-26b-a4b-it, llama-3.1-8b-instruct
