# GitHub Models — Audit de validité des modèles

**Date de vérification :** 2026-05-26
**Source :** models.github.ai/catalog/models (REST API)

---

## Résumé
| Stat | Nombre | Détails |
|------|--------|---------|
| ✅ Confirmés existants | 15 | Tous les modèles actuels existent |
| 🗑️ Dépréciés — à retirer | 0 | Aucun |
| ➕ Nouveaux — à ajouter | 11 | Free-tier models disponibles (GPT-4o, Phi-4, Cohere, Jamba, etc.) |
| ⚠️ Corrections de config | 1 | `ministral-3b` context 32k → 128k |

---

## ✅ Modèles CONFIRMÉS opérationnels

| # | Model ID | Display Name | Tier | SWE | CTX | Statut |
|---|----------|-------------|------|-----|-----|--------|
| 1 | `openai/gpt-4.1` | GPT-4.1 | S+ | - | 1M | ✅ Free (high tier) |
| 2 | `openai/gpt-4.1-mini` | GPT-4.1 Mini | S | - | 1M | ✅ Free (low tier) |
| 3 | `openai/gpt-4.1-nano` | GPT-4.1 Nano | A | - | 1M | ✅ Free (low tier) |
| 4 | `deepseek/deepseek-v3-0324` | DeepSeek V3 0324 | S | 62.0% | 128k | ✅ Free (high tier) |
| 5 | `meta/meta-llama-3.1-405b-instruct` | Llama 3.1 405B | A | 44.0% | 128k | ✅ Free (high tier) |
| 6 | `meta/llama-4-maverick-17b-128e-instruct-fp8` | Llama 4 Maverick | S | 62.0% | 1M | ✅ Free (high tier) |
| 7 | `meta/llama-4-scout-17b-16e-instruct` | Llama 4 Scout | A | 44.0% | 10M | ✅ Free (high tier) |
| 8 | `meta/llama-3.3-70b-instruct` | Llama 3.3 70B | A- | 39.5% | 128k | ✅ Free (high tier) |
| 9 | `meta/llama-3.2-90b-vision-instruct` | Llama 3.2 90B Vision | A- | - | 128k | ✅ Free (high tier) |
| 10 | `meta/llama-3.2-11b-vision-instruct` | Llama 3.2 11B Vision | B | - | 128k | ✅ Free (low tier) |
| 11 | `meta/meta-llama-3.1-8b-instruct` | Llama 3.1 8B | B | 28.8% | 128k | ✅ Free (low tier) |
| 12 | `mistral-ai/codestral-2501` | Codestral 2501 | B+ | 34.0% | 256k | ✅ Free (high tier) |
| 13 | `mistral-ai/mistral-medium-2505` | Mistral Medium 2505 | A | 48.0% | 128k | ✅ Free (high tier) |
| 14 | `mistral-ai/mistral-small-2503` | Mistral Small 2503 | B+ | 30.0% | 128k | ✅ Free (high tier) |
| 15 | `mistral-ai/ministral-3b` | Ministral 3B | C | - | **128k** ⚠️ | ✅ Free (low tier) |

---

## ⚠️ Corrections de config

| Model ID | Champ | Ancien | Nouveau |
|----------|-------|--------|---------|
| `mistral-ai/ministral-3b` | context | 32k | **128k** (131,072 tokens) |

---

## ➕ Nouveaux modèles à ajouter (free-tier, pertinents pour coding)

### Free High Tier Models (8 nouveaux)

| Model ID | Display Name | Tier suggéré | CTX | Notes |
|----------|-------------|-------------|-----|-------|
| `openai/gpt-4o` | GPT-4o | S | 128k | Frontier multimodal, gratuit sur GitHub Models |
| `openai/gpt-4o-mini` | GPT-4o Mini | A | 128k | Version économique de GPT-4o |
| `microsoft/phi-4` | Phi-4 | A | 16k | 14B params, excellent reasoning |
| `microsoft/phi-4-mini` | Phi-4 Mini | B+ | 128k | Version mini de Phi-4 |
| `microsoft/phi-4-mini-reasoning` | Phi-4 Mini Reasoning | B+ | 128k | Variante reasoning |
| `cohere/command-r` | Cohere Command R | B+ | 128k | RAG-optimized |
| `cohere/command-r-plus` | Cohere Command R+ | A | 128k | Version avancée |
| `ai21/jamba-1.5-large` | Jamba 1.5 Large | B+ | 256k | MoE, long context |

### Free Low Tier Models (3 nouveaux)

| Model ID | Display Name | Tier suggéré | CTX | Notes |
|----------|-------------|-------------|-----|-------|
| `cohere/command-r7b` | Cohere Command R7B | B | 128k | Petit modèle RAG |
| `mistral-ai/mistral-nemo` | Mistral Nemo | B+ | 128k | 12B params |
| `ai21/jamba-1.5-mini` | Jamba 1.5 Mini | B | 256k | Version mini |

### Premium Models (Copilot Pro+ required — not free)

15 modèles premium sont disponibles mais nécessitent Copilot Pro+ (GPT-5 family, o1/o3/o4-mini, DeepSeek R1, Grok 3, etc.) — **non pertinents pour free-coding-models**.

---

## 📝 Modifications à appliquer dans sources.js

### CORRIGER

```javascript
// AVANT
['mistral-ai/ministral-3b',                     'Ministral 3B',        'C',  '-',     '32k'],
// APRÈS
['mistral-ai/ministral-3b',                     'Ministral 3B',        'C',  '-',     '128k'],
```

### AJOUTER (recommandé)

```javascript
// ── S tier ──
['openai/gpt-4o',                               'GPT-4o',              'S',  '-',     '128k'],
// ── A tier ──
['openai/gpt-4o-mini',                          'GPT-4o Mini',         'A',  '-',     '128k'],
['cohere/command-r-plus',                       'Cohere Command R+',   'A',  '-',     '128k'],
// ── B+ tier ──
['microsoft/phi-4',                             'Phi-4',               'A',  '-',     '16k'],
['microsoft/phi-4-mini',                        'Phi-4 Mini',          'B+', '-',     '128k'],
['cohere/command-r',                            'Cohere Command R',    'B+', '-',     '128k'],
['ai21/jamba-1.5-large',                        'Jamba 1.5 Large',     'B+', '-',     '256k'],
['mistral-ai/mistral-nemo',                     'Mistral Nemo',        'B+', '-',     '128k'],
```

---

## Sources

- **GitHub Models API** : `https://models.github.ai/catalog/models` — 41 chat-completion models + 4 embedding models
- Consulté le 2026-05-26
