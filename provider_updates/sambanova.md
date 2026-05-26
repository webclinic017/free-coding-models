# SambaNova — Audit de validité des modèles

**Date de vérification :** 2026-05-26
**Source :** https://docs.sambanova.ai/docs/en/models/sambacloud-models + https://docs.sambanova.ai/docs/en/models/deprecations + https://docs.sambanova.ai/docs/en/models/rate-limits

---

## Résumé
| Stat | Nombre | Détails |
|------|--------|---------|
| ✅ Confirmés existants | 4 | DeepSeek-V3.1, DeepSeek-V3.2, gpt-oss-120b, Meta-Llama-3.3-70B-Instruct |
| 🗑️ Dépréciés — à retirer | 1 | MiniMax-M2.5 (remplacé par MiniMax-M2.7) |
| ❌ 404 / Supprimés | 0 | — |
| ➕ Nouveaux — à ajouter | 2 | MiniMax-M2.7, gemma-3-12b-it |
| ⚠️ Changement de config | 1 | Llama-4-Maverick context window (1M → 128k) |

---

## 🗑️ Modèles DÉPRÉCIÉS

| Modèle ID | Display Name | Tier actuel | Statut | Remplacement | Date de suppression | Action |
|-----------|-------------|-------------|--------|--------------|-------------------|--------|
| `MiniMax-M2.5` | MiniMax M2.5 | S+ | 🗑️ Déprécié, retiré | `MiniMax-M2.7` | 18/05/2026 | RETIRER de sources.js |

---

## ➕ Nouveaux modèles à ajouter

| Modèle ID | Display Name suggéré | Tier suggéré | Context Window | Statut | Action |
|-----------|---------------------|--------------|----------------|--------|--------|
| `MiniMax-M2.7` | MiniMax M2.7 | S+ | 192k | Production | AJOUTER — Remplacement direct de MiniMax-M2.5 |
| `gemma-3-12b-it` | Gemma 3 12B IT | B+ | 128k | Preview | AJOUTER — Nouveau modèle Google Gemma 3 multimodal |

---

## ✅ Modèles CONFIRMÉS opérationnels

| Modèle ID | Display Name | Tier | SWE Score | Context (sources.js) | Context (SambaNova) | Statut |
|-----------|-------------|------|-----------|----------------------|---------------------|--------|
| `DeepSeek-V3.1` | DeepSeek V3.1 | S | 62.0% | 128k | 128k | ✅ Concordant |
| `DeepSeek-V3.2` | DeepSeek V3.2 | S+ | 70.0% | 32k | 32k | ✅ Concordant |
| `gpt-oss-120b` | GPT OSS 120B | S | 60.0% | 128k | 128k | ✅ Concordant |
| `Meta-Llama-3.3-70B-Instruct` | Llama 3.3 70B | A- | 39.5% | 128k | 128k | ✅ Concordant |
| `Llama-4-Maverick-17B-128E-Instruct` | Llama 4 Maverick | S | 62.0% | **1M** ⚠️ | **128k** ⚠️ | ⚠️ Voir section config |

---

## ⚠️ Changements de configuration

### Context Window — Llama-4-Maverick-17B-128E-Instruct

| Champ | Valeur dans sources.js | Valeur confirmée SambaNova |
|-------|----------------------|---------------------------|
| Context Window | **1M** | **128k** |

**Explication :** Le modèle Llama 4 Maverick supporte théoriquement 1M tokens nativement, mais **SambaNova ne propose que 128k tokens de contexte** sur SambaCloud.

**Action recommandée :** Changer `'1M'` → `'128k'` pour ce modèle.

---

## 📝 Modifications à appliquer dans sources.js

### Lignes à RETIRER

```diff
-  ['MiniMax-M2.5',                         'MiniMax M2.5',       'S+', '74.0%', '160k'],
```

### Lignes à AJOUTER

```diff
+  ['MiniMax-M2.7',                         'MiniMax M2.7',       'S+', '56.2%', '192k'],
+  ['gemma-3-12b-it',                        'Gemma 3 12B IT',     'B+', '46.0%', '128k'],
```

### Lignes à MODIFIER

```diff
-  ['Llama-4-Maverick-17B-128E-Instruct',   'Llama 4 Maverick',   'S',  '62.0%', '1M'],
+  ['Llama-4-Maverick-17B-128E-Instruct',   'Llama 4 Maverick',   'S',  '62.0%', '128k'],
```

---

## 📋 Dépréciations historiques SambaNova (hors liste sources.js — pour référence)

| Modèle ID | Date de suppression | Remplacement |
|-----------|-------------------|--------------|
| `DeepSeek-V3-0324` | 14/04/2026 | DeepSeek-V3.1 |
| `DeepSeek-R1-0528` | 14/04/2026 | gpt-oss-120b |
| `Meta-Llama-3.1-8B-Instruct` | 14/04/2026 | Meta-Llama-3.3-70B-Instruct |
| `DeepSeek-V3.1-Terminus` | 06/04/2026 | DeepSeek-V3.1 |
| `Qwen3-235B-A22B-Instruct-2507` | 06/04/2026 | MiniMax-M2.5 (puis M2.7) |
| `Qwen3-32B` | 06/04/2026 | MiniMax-M2.5 (puis M2.7) |
| `DeepSeek-R1-Distill-Llama-70B` | 20/03/2026 | gpt-oss-120b |

---

## Sources

- **SambaCloud models** : https://docs.sambanova.ai/docs/en/models/sambacloud-models
- **Deprecations** : https://docs.sambanova.ai/docs/en/models/deprecations
- **Rate limits** : https://docs.sambanova.ai/docs/en/models/rate-limits
