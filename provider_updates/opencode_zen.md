# OpenCode Zen — Audit de validité des modèles

**Date de vérification :** 2026-05-26
**Source :** opencode.ai/docs/zen + API /zen/v1/models + pi.dev/models

---

## Résumé
| Stat | Nombre | Détails |
|------|--------|---------|
| ✅ Confirmés existants | 2 | `big-pickle`, `minimax-m2.5-free` |
| ⚠️ Config à corriger | 1 | `nematron-3-super-free` (1M → 200k) |
| ⚠️ Pas gratuit (payant ultra-bon marché) | 1 | `gpt-5-nano` ($0.05/$0.40 per 1M tokens) |
| 🗑️ Supprimés — à retirer | 4 | `hy3-preview-free`, `ling-2.6-flash-free`, `trinity-mini-free`, `trinity-large-preview-free` |
| ➕ Nouveaux — à ajouter | 2 | `deepseek-v4-flash-free`, `qwen3.6-plus-free` |

---

## 🗑️ Modèles SUPPRIMÉS — à RETIRER

Ces 4 modèles n'existent plus sur OpenCode Zen (absents de l'API `/zen/v1/models`) :

```javascript
['hy3-preview-free',                'HY3 Preview Free',    'A+', '-',     '128k'],
['ling-2.6-flash-free',             'Ling 2.6 Flash Free',  'S',  '-',     '128k'],
['trinity-mini-free',               'Trinity Mini Preview', 'A',  '-',     '128k'],
['trinity-large-preview-free',      'Trinity Large Preview','S',  '-',     '128k'],
```

---

## ✅ Modèles CONFIRMÉS existants

### `big-pickle` — Big Pickle ✅
- **Context :** 200k (confirmé)
- **Prix :** Free
- **Reasoning :** Oui
- **Aucun changement nécessaire**

### `minimax-m2.5-free` — MiniMax M2.5 Free ✅
- **Context :** 200k (confirmé)
- **SWE-bench :** 80.2%
- **Prix :** Free
- **Aucun changement nécessaire**

---

## ⚠️ Config à corriger

### `nemotron-3-super-free` — Nemotron 3 Super Free
- **Context sources.js :** 1M
- **Context réel Zen :** **204,800 (~200k)** — Zen bride le modèle natif NVIDIA (1M) à ~200k
- **Action :** Corriger `'1M'` → `'200k'`

### `gpt-5-nano` — GPT 5 Nano
- **Context :** 400k (confirmé)
- **⚠️ Prix :** **$0.05/$0.40 per 1M tokens** — PAS GRATUIT
- **Action :** Décision du mainteneur — garder ou retirer

---

## ➕ Nouveaux modèles à ajouter

### `deepseek-v4-flash-free` — DeepSeek V4 Flash Free
- **Context :** 200k
- **Max Output :** 128k
- **Reasoning :** Oui (format DeepSeek)
- **Prix :** Free (durée limitée)
- **SWE-bench estimé :** ~79.0%
- **Tier suggéré :** S+

```javascript
['deepseek-v4-flash-free', 'DeepSeek V4 Flash Free', 'S+', '79.0%', '200k'],
```

### `qwen3.6-plus-free` — Qwen3.6 Plus Free
- **Context :** 1M
- **Max Output :** 64k
- **Reasoning :** Oui
- **Prix :** Free
- **SWE-bench estimé :** ~78.8%
- **Tier suggéré :** S+

```javascript
['qwen3.6-plus-free', 'Qwen3.6 Plus Free', 'S+', '78.8%', '1M'],
```

---

## 📝 Modifications à appliquer dans sources.js

### RETIRER (4 modèles)

```javascript
['hy3-preview-free',                'HY3 Preview Free',    'A+', '-',     '128k'],
['ling-2.6-flash-free',             'Ling 2.6 Flash Free',  'S',  '-',     '128k'],
['trinity-mini-free',               'Trinity Mini Preview', 'A',  '-',     '128k'],
['trinity-large-preview-free',      'Trinity Large Preview','S',  '-',     '128k'],
```

### CORRIGER (1 modèle)

```javascript
// AVANT
['nemotron-3-super-free',           'Nemotron 3 Super Free','A+', '52.0%', '1M'],
// APRÈS
['nemotron-3-super-free',           'Nemotron 3 Super Free','A+', '52.0%', '200k'],
```

### AJOUTER (2 modèles)

```javascript
['deepseek-v4-flash-free',          'DeepSeek V4 Flash Free', 'S+', '79.0%', '200k'],
['qwen3.6-plus-free',              'Qwen3.6 Plus Free',      'S+', '78.8%', '1M'],
```

### Liste finale proposée

```javascript
export const opencodeZen = [
  ['big-pickle',                       'Big Pickle',              'S+', '72.0%', '200k'],
  ['minimax-m2.5-free',                'MiniMax M2.5 Free',      'S+', '80.2%', '200k'],
  ['deepseek-v4-flash-free',           'DeepSeek V4 Flash Free',  'S+', '79.0%', '200k'],
  ['qwen3.6-plus-free',                'Qwen3.6 Plus Free',       'S+', '78.8%', '1M'],
  ['nemotron-3-super-free',            'Nemotron 3 Super Free',   'A+', '52.0%', '200k'],
  ['gpt-5-nano',                       'GPT 5 Nano',              'S',  '65.0%', '400k'],  // ⚠️ pas gratuit
]
```

---

## Sources

- [OpenCode Zen Docs](https://opencode.ai/docs/zen/)
- [Zen API /v1/models](https://opencode.ai/zen/v1/models) — 42 modèles actifs
- [pi.dev/models/opencode/](https://pi.dev/models/opencode) — Specs détaillées
