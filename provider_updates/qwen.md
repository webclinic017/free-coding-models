# Alibaba DashScope (Qwen) — Audit de validité des modèles

**Date de vérification :** 2026-05-26
**Source :** dashscope-intl.aliyuncs.com / help.aliyun.com/zh/model-studio

---

## Résumé
| Stat | Nombre | Détails |
|------|--------|---------|
| ✅ Confirmés existants | 8 | Tous les modèles existent |
| 🗑️ À retirer / réévaluer | 1 | qwen2.5-coder-32b-instruct (legacy) |
| ➕ Nouveaux — à ajouter | 3 | qwen3.7-max, qwen3.6-plus, qwen3.6-flash |
| ⚠️ Config corrigée | 4 | Corrections de context window |
| 🔀 ID à corriger | 1 | qwen3-235b-a22b-instruct → qwen3-235b-a22b |

---

## ✅ Modèles CONFIRMÉS opérationnels

| Model ID | Display Name | ctx sources.js | ctx DashScope | Action |
|----------|-------------|---------------|--------------|--------|
| `qwen3-max` | Qwen3 Max | 1M | **256k** | ⚠️ Corriger ctx |
| `qwen3-235b-a22b-instruct` | Qwen3 235B | 256k | 256k | ⚠️ ID à corriger → `qwen3-235b-a22b` |
| `qwen3.5-plus` | Qwen3.5 Plus | 1M | 1M | ✅ OK |
| `qwen3-coder-plus` | Qwen3 Coder Plus | 256k | **1M** | ⚠️ Corriger ctx |
| `qwen3-coder-next` | Qwen3 Coder Next | 256k | 256k | ✅ OK |
| `qwen3.5-flash` | Qwen3.5 Flash | 1M | 1M | ✅ OK |
| `qwen3-coder-flash` | Qwen3 Coder Flash | 256k | **1M** | ⚠️ Corriger ctx |
| `qwen3-32b` | Qwen3 32B | 128k | **256k** | ⚠️ Corriger ctx |

---

## 🗑️ Modèles à retirer

### `qwen2.5-coder-32b-instruct` — Qwen2.5 Coder 32B
- **Statut :** Legacy (section "旧版"), plus dans les modèles recommandés
- **Remplacement :** `qwen3-coder-plus` ou `qwen3-coder-flash`
- **Action :** RETIRER

---

## ➕ Nouveaux modèles à ajouter

| Model ID | Display Name | Tier suggéré | Context | Notes |
|----------|-------------|-------------|---------|-------|
| `qwen3.7-max` | Qwen3.7 Max | S+ | 1M | 🆕 Nouveau flagship (mai 2026) |
| `qwen3.6-plus` | Qwen3.6 Plus | S+ | 1M | 🆕 Recommandé par Alibaba (avril 2026) |
| `qwen3.6-flash` | Qwen3.6 Flash | A | 1M | 🆕 Version économique de 3.6-plus |

---

## 📝 Modifications à appliquer dans sources.js

### RETIRER

```javascript
['qwen2.5-coder-32b-instruct', 'Qwen2.5 Coder 32B', 'A', '46.0%', '32k'],
```

### CORRIGER (context windows)

```javascript
// AVANT → APRÈS
['qwen3-max',          'Qwen3 Max',          'S+', '78.8%', '1M'],    → ['qwen3-max',          'Qwen3 Max',          'S+', '78.8%', '256k'],
['qwen3-coder-plus',   'Qwen3 Coder Plus',   'S',  '69.6%', '256k'], → ['qwen3-coder-plus',   'Qwen3 Coder Plus',   'S',  '69.6%', '1M'],
['qwen3-coder-flash',  'Qwen3 Coder Flash',  'A+', '55.0%', '256k'], → ['qwen3-coder-flash',  'Qwen3 Coder Flash',  'A+', '55.0%', '1M'],
['qwen3-32b',          'Qwen3 32B',           'A+', '50.0%', '128k'], → ['qwen3-32b',          'Qwen3 32B',           'A+', '50.0%', '256k'],
```

### CORRIGER (model ID)

```javascript
// AVANT
['qwen3-235b-a22b-instruct', 'Qwen3 235B', 'S+', '70.0%', '256k'],
// APRÈS — utiliser l'ID hybride thinking+instruct
['qwen3-235b-a22b', 'Qwen3 235B', 'S+', '70.0%', '256k'],
```

### AJOUTER

```javascript
['qwen3.7-max',       'Qwen3.7 Max',       'S+', '~80%', '1M'],
['qwen3.6-plus',      'Qwen3.6 Plus',      'S+', '~72%', '1M'],
['qwen3.6-flash',     'Qwen3.6 Flash',     'A',  '~60%', '1M'],
```

---

## ⚠️ Disponibilité par endpoint

| Endpoint | URL | Qwen-Coder | QwQ |
|---|---|---|---|
| **International (Singapore)** | dashscope-intl.aliyuncs.com | ❌ Non | ❌ Non |
| **China (Beijing)** | dashscope.aliyuncs.com | ✅ Oui | ✅ Oui |

Les modèles `qwen3-coder-plus`, `qwen3-coder-flash`, `qwen3-coder-next` ne sont disponibles que sur l'endpoint chinois.

---

## Sources

- [DashScope Text Generation Models](https://help.aliyun.com/zh/model-studio/text-generation-model)
- [DashScope OpenAI Compatibility](https://www.alibabacloud.com/help/en/model-studio/compatibility-of-openai-with-dashscope)
- [Alibaba Cloud Free Tier](https://www.alibabacloud.com/free)
