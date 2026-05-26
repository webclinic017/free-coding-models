# Mistral La Plateforme + Codestral — Audit de validité des modèles

**Date de vérification :** 2026-05-26
**Source :** docs.mistral.ai / Mistral API / Model Cards / SWE-bench

---

## Résumé
| Stat | Nombre | Détails |
|------|--------|---------|
| ✅ Confirmés existants (avec MAJ) | 4 | Tous ont évolué vers de nouvelles versions |
| 🗑️ Dépréciés — à retirer | 3 | `devstral-medium-latest`, `devstral-small-latest`, `magistral-small-latest` |
| ❌ Supprimés — à retirer | 0 | Aucun modèle totalement supprimé |
| ➕ Nouveaux — à ajouter | 4 | Mistral Large 3, Medium 3.5, Small 4, Devstral 2 |
| ⚠️ À mettre à jour (Codestral) | 1 | `codestral-latest` — contexte réduit 256k→128k |

---

## 🗑️ Modèles DÉPRÉCIÉS

### 1. `devstral-medium-latest` — Devstral Medium
| Champ | Valeur |
|-------|--------|
| Tier actuel | S+ |
| SWE-bench | 72.2% |
| **Statut** | 🗑️ **DÉPRÉCIÉ** — retrait le 31/05/2026 |
| Remplacement | **Devstral 2** (API: `devstral-2512`, 256k ctx) |
| Action | RETIRER et REMPLACER par Devstral 2 |

### 2. `devstral-small-latest` — Devstral Small
| Champ | Valeur |
|-------|--------|
| Tier actuel | A+ |
| **Statut** | 🗑️ **DÉPRÉCIÉ** — retrait le 31/05/2026 |
| Remplacement | **Devstral 2** (API: `devstral-2512`) — unifié, remplace les deux tailles |
| Action | RETIRER et REMPLACER par Devstral 2 |

### 3. `magistral-small-latest` — Magistral Small
| Champ | Valeur |
|-------|--------|
| Tier actuel | A |
| **Statut** | 🗑️ **DÉPRÉCIÉ** — retrait le 31/07/2026 |
| Remplacement | **Mistral Small 4** (API: `mistral-small-2603`) |
| Action | RETIRER |

---

## ➕ Nouveaux modèles à ajouter

### 1. Mistral Medium 3.5
| Champ | Valeur |
|-------|--------|
| API ID | `mistral-medium-3-5` |
| Contexte | **256k** |
| SWE-bench Verified | **77.6%** |
| Spécialité | Optimisé pour agentic & coding |
| Tier suggéré | **S+** (77.6% SWE-bench > Devstral 2) |
| Action | REMPLACER `mistral-medium-latest` |

### 2. Devstral 2
| Champ | Valeur |
|-------|--------|
| API ID | `devstral-2512` |
| Contexte | **256k** |
| SWE-bench Verified | **72.2%** |
| Architecture | 123B dense |
| Tier suggéré | **S+** |
| Action | REMPLACER les entrées `devstral-medium-latest` ET `devstral-small-latest` |

### 3. Mistral Large 3
| Champ | Valeur |
|-------|--------|
| API ID | `mistral-large-2512` |
| Contexte | 256k |
| Architecture | MoE 675B total, 41B actif |
| Tier suggéré | **S+** |
| Action | Mettre à jour nom + ID de `mistral-large-latest` |

### 4. Mistral Small 4
| Champ | Valeur |
|-------|--------|
| API ID | `mistral-small-2603` |
| Contexte | **256k** |
| Architecture | 119B total, 6.5B actif (MoE hybride) |
| Tier suggéré | **A** |
| Action | Mettre à jour nom + ID + ctx de `mistral-small-latest` |

---

## ⚠️ Codestral — Context window RÉDUIT

| Champ | Ancien | Nouveau |
|-------|--------|---------|
| API ID | `codestral-latest` | `codestral-2508` |
| Contexte | **256k** | **128k** ⬇️ |
| Action | METTRE À JOUR | ctx → 128k |

---

## ✅ Modèles CONFIRMÉS opérationnels

| Modèle (dans sources.js) | API ID actuel | Contexte réel | Statut | Action |
|---|---|---|---|---|
| mistral-large-latest | `mistral-large-2512` | 256k ✅ | ✅ Actif (Large 3) | màj nom + ID |
| mistral-medium-latest | `mistral-medium-3-5` | **256k** ⬆️ | ✅ Actif (Medium 3.5) | màj nom + ID + ctx |
| mistral-small-latest | `mistral-small-2603` | **256k** ⬆️ | ✅ Actif (Small 4) | màj nom + ID + ctx |
| magistral-medium-latest | `magistral-medium-2509` | 128k ✅ | ✅ Actif (Medium 1.2) | màj nom + ID |
| codestral-latest | `codestral-2508` | **128k** ⬇️ | ⚠️ Actif, ctx changé | màj ID + ctx |

---

## 📝 Modifications à appliquer dans sources.js

### Mistral provider — RÉSULTAT FINAL

```javascript
export const mistral = [
  // ── S+ tier ──
  ['mistral-large-2512',        'Mistral Large 3',     'S+', '70.0%', '256k'],
  ['mistral-medium-3-5',        'Mistral Medium 3.5',  'S+', '77.6%', '256k'],
  ['devstral-2512',             'Devstral 2',          'S+', '72.2%', '256k'],
  ['magistral-medium-2509',     'Magistral Medium 1.2','A+', '52.0%', '128k'],
  // ── A tier ──
  ['mistral-small-2603',        'Mistral Small 4',     'A',  '48.0%', '256k'],
  // 🗑️ Retiré 2026-05-26 (dépréciation Mistral) :
  // ['devstral-medium-latest',  'Devstral Medium',     'S+', '72.2%', '128k'],
  // ['devstral-small-latest',   'Devstral Small',      'A+', '55.0%', '128k'],
  // ['magistral-small-latest',  'Magistral Small',     'A',  '45.0%', '128k'],
]
```

### Codestral provider — RÉSULTAT FINAL

```javascript
export const codestral = [
  ['codestral-2508',            'Codestral',           'B+', '34.0%', '128k'],
]
```

---

## 🔑 Points clés

1. **Devstral unifié** : Devstral Medium et Small fusionnés en **Devstral 2** (123B dense, 256k, SWE-bench 72.2%)
2. **Mistral Medium 3.5 = nouveau roi du coding** : 77.6% SWE-bench, dépasse Devstral 2
3. **Context windows augmentent** : Tous les nouveaux modèles passent à **256k** (sauf Magistral Medium 128k)
4. **Codestral contexte réduit** : 256k → 128k pour la version v25.08
5. **IDs API changent** : Mistral n'utilise plus les alias `-latest`, IDs versionnés avec codes de date

---

## Sources

- [Mistral Models Overview](https://docs.mistral.ai/models/overview)
- [Devstral 2 Model Card](https://docs.mistral.ai/models/model-cards/devstral-2-25-12)
- [Mistral Medium 3.5 Model Card](https://docs.mistral.ai/models/model-cards/mistral-medium-3-5-26-04)
- [Mistral Small 4 Model Card](https://docs.mistral.ai/models/model-cards/mistral-small-4-0-26-03)
- [Codestral Model Card](https://docs.mistral.ai/models/model-cards/codestral-25-08)
