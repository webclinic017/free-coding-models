# Cerebras — Audit de validité des modèles

**Date de vérification :** 2026-05-26
**Source :** https://inference-docs.cerebras.ai/models/overview + individual model pages

---

## Résumé

| Stat | Nombre | Détails |
|------|--------|---------|
| ✅ Confirmés existants | 2 | `gpt-oss-120b`, `zai-glm-4.7` |
| 🗑️ Dépréciés — à retirer | 2 | `qwen-3-235b-a22b-instruct-2507`, `llama3.1-8b` (May 27, 2026 = DEMAIN) |
| ❌ 404 / Supprimés | 0 | — |
| ➕ Nouveaux — à ajouter | 0 | Aucun nouveau modèle public |
| ⚠️ Config à corriger | 3 | Context windows incorrects pour 3 modèles |

### ⚠️ Note critique : dépréciation imminente

> `llama3.1-8b` and `qwen-3-235b-a22b-instruct-2507` will be deprecated on **May 27, 2026**.

La date d'audit étant le 2026-05-26, ces deux modèles seront **dépréciés demain**. Ils doivent être retirés immédiatement.

---

## 🗑️ Modèles DÉPRÉCIÉS

### 1. `qwen-3-235b-a22b-instruct-2507` — Qwen3 235B

| Champ | Valeur |
|-------|--------|
| Model ID | `qwen-3-235b-a22b-instruct-2507` |
| Display Name | Qwen3 235B |
| Tier dans sources.js | `S+` |
| Statut | 🗑️ **DÉPRÉCIÉ — dépréciation officielle le May 27, 2026** |
| Remplacement recommandé | Aucun remplacement direct sur le free tier |
| Action | **Retirer de sources.js** |

### 2. `llama3.1-8b` — Llama 3.1 8B

| Champ | Valeur |
|-------|--------|
| Model ID | `llama3.1-8b` |
| Display Name | Llama 3.1 8B |
| Tier dans sources.js | `B` |
| Statut | 🗑️ **DÉPRÉCIÉ — dépréciation officielle le May 27, 2026** |
| Remplacement recommandé | Aucun remplacement direct sur le free tier |
| Remarque | Context réel = 8k (free) / 32k (paid) — le `128k` dans sources.js était **incorrect** |
| Action | **Retirer de sources.js** |

---

## ➕ Nouveaux modèles à ajouter

**Aucun nouveau modèle public.** Les modèles additionnels sur Cerebras sont exclusivement disponibles via **Dedicated Endpoints** (payants).

---

## ✅ Modèles CONFIRMÉS opérationnels

| Model ID | Display Name | Tier | Context (Free) | Context (Paid) | Max Output (Free) | Speed | Statut |
|----------|-------------|------|-----------------|----------------|-------------------|-------|--------|
| `gpt-oss-120b` | GPT OSS 120B | S | 65k | 131k | 32k | ~3000 tok/s | ✅ Production, rate limits réduits |
| `zai-glm-4.7` | GLM 4.7 | S+ | 64k | 131k | 40k | ~1000 tok/s | ✅ Preview, rate limits réduits |

---

## 📝 Modifications à appliquer dans sources.js

### RETIRER ces lignes (modèles dépréciés le 27 mai 2026) :

```javascript
// ❌ RETIRER — déprécié May 27, 2026
['qwen-3-235b-a22b-instruct-2507',       'Qwen3 235B',         'S+', '70.0%', '128k'],
// ❌ RETIRER — déprécié May 27, 2026
['llama3.1-8b',                          'Llama 3.1 8B',       'B',  '28.8%', '128k'],
```

### CORRIGER le contexte de ces modèles :

```javascript
// AVANT :
['gpt-oss-120b',                         'GPT OSS 120B',       'S',  '60.0%', '128k'],
['zai-glm-4.7',                          'GLM 4.7',            'S+', '73.8%', '200k'],

// APRÈS :
['gpt-oss-120b',                         'GPT OSS 120B',       'S',  '60.0%', '131k'],
['zai-glm-4.7',                          'GLM 4.7',            'S+', '73.8%', '131k'],
```

### Bloc Cerebras final après modifications :

```javascript
export const cerebras = [
  ['gpt-oss-120b',                         'GPT OSS 120B',       'S',  '60.0%', '131k'],
  ['zai-glm-4.7',                          'GLM 4.7',            'S+', '73.8%', '131k'],
  // 🗑️ Retiré 2026-05-26 (dépréciation Cerebras May 27, 2026) :
  // ['llama3.1-8b',                       'Llama 3.1 8B',       'B',  '28.8%', '128k'],
  // ['qwen-3-235b-a22b-instruct-2507',    'Qwen3 235B',         'S+', '70.0%', '128k'],
]
```

---

## Sources

- **Cerebras Models Overview** : [inference-docs.cerebras.ai/models/overview](https://inference-docs.cerebras.ai/models/overview)
- **GLM 4.7 Migration Guide** : [inference-docs.cerebras.ai/resources/glm-47-migration](https://inference-docs.cerebras.ai/resources/glm-47-migration)
