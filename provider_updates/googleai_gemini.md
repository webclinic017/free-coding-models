# Google AI Studio + Gemini CLI — Audit de validité des modèles

**Date de vérification :** 2026-05-26
**Source :** ai.google.dev/gemini-api/docs/models + ai.google.dev/gemini-api/docs/deprecations

---

## Résumé
| Stat | Nombre | Détails |
|------|--------|---------|
| ✅ Confirmés existants | 4 | gemini-3.1-pro-preview, gemini-3-flash-preview, gemini-2.5-pro, gemini-2.5-flash |
| 🗑️ Dépréciés — à marquer | 3 | gemini-2.5-pro, gemini-2.5-flash, gemini-2.5-flash-lite (shutdown Oct 16, 2026) |
| ❌ Supprimés — à retirer | 1 | gemini-3.1-flash-lite-preview (shut down May 25, 2026) |
| ➕ Nouveaux — à ajouter | 2 | gemini-3.5-flash (Stable), gemini-3.1-flash-lite (Stable) |
| 🔄 Preview → GA | 1 | gemini-3.1-flash-lite-preview → gemini-3.1-flash-lite (May 7, 2026) |

---

## ❌ Modèles SUPPRIMÉS (endpoint mort)

### 1. `gemini-3.1-flash-lite-preview`
| Champ | Valeur |
|-------|--------|
| Tier actuel | A+ |
| Shutdown Date | **May 25, 2026** |
| Remplaçant officiel | `gemini-3.1-flash-lite` (Stable) |
| Action | **RETIRER** de sources.js — l'endpoint ne répond plus |

---

## 🗑️ Modèles DÉPRÉCIÉS (encore actifs, shutdown programmé Oct 16, 2026)

| Model ID | Remplaçant officiel | Action |
|----------|-------------------|--------|
| `gemini-2.5-pro` | `gemini-3.1-pro-preview` | ⚠️ Garder avec marqueur deprecated |
| `gemini-2.5-flash` | `gemini-3.5-flash` | ⚠️ Garder avec marqueur deprecated |
| `gemini-2.5-flash-lite` | `gemini-3.1-flash-lite` | ⚠️ Garder avec marqueur deprecated |

---

## ➕ Nouveaux modèles à ajouter

### 1. `gemini-3.5-flash` 🆕
| Champ | Valeur |
|-------|--------|
| Status | **Stable** (GA depuis May 19, 2026 — Google I/O 2026) |
| Context | 1M |
| Benchmarks | 76.2% Terminal-Bench 2.1, 83.6% MCP Atlas |
| Capabilities | Text, Image, Video, Audio, PDF. Thinking, Code Execution, Function Calling, Search Grounding |
| Tier suggéré | **S+** — Bat 3.1 Pro sur 11/15 benchmarks coding/agent |
| Action | **AJOUTER** aux deux providers (googleai + gemini) |

### 2. `gemini-3.1-flash-lite` 🆕 (graduated from Preview)
| Champ | Valeur |
|-------|--------|
| Status | **Stable** (GA depuis May 7, 2026) |
| Context | 1M |
| Prix | $0.15 input / $0.75 output per M tokens |
| Tier suggéré | **A+** (même tier que la version preview) |
| Action | **AJOUTER** — remplace le preview defunct |

---

## ✅ Modèles CONFIRMÉS opérationnels

| Model ID | Display Name | Type | Context | Status | Notes |
|----------|-------------|------|---------|--------|-------|
| `gemini-3.5-flash` | Gemini 3.5 Flash | **Stable** | 1M | ✅ 🆕 | Bat 3.1 Pro sur coding |
| `gemini-3.1-pro-preview` | Gemini 3.1 Pro Preview | Preview | 1M | ✅ Actif | 80.6% SWE-bench |
| `gemini-3-flash-preview` | Gemini 3 Flash Preview | Preview | 1M | ✅ Actif | Remplacement recommandé: 3.5-flash |
| `gemini-3.1-flash-lite` | Gemini 3.1 Flash Lite | **Stable** | 1M | ✅ 🆕 | Graduated from preview |
| `gemini-2.5-pro` | Gemini 2.5 Pro | Stable | 1M | ⚠️ Déprécié | Shutdown Oct 16, 2026 |
| `gemini-2.5-flash` | Gemini 2.5 Flash | Stable | 1M | ⚠️ Déprécié | Shutdown Oct 16, 2026 |
| `gemini-2.5-flash-lite` | Gemini 2.5 Flash Lite | Stable | 1M | ⚠️ Déprécié | Shutdown Oct 16, 2026 |

---

## 📝 Modifications à appliquer dans sources.js

### RETIRER (endpoint mort) — googleai ET gemini

```javascript
// RETIRER (shutdown May 25, 2026):
['gemini-3.1-flash-lite-preview',             'Gemini 3.1 Flash Lite Preview','A+', '55.0%', '1M'],
```

### AJOUTER — googleai ET gemini

```javascript
// Tier S+ — nouveau modèle
['gemini-3.5-flash',                          'Gemini 3.5 Flash',             'S+', '—',     '1M'],
// Tier A+ — graduated from preview
['gemini-3.1-flash-lite',                     'Gemini 3.1 Flash Lite',        'A+', '55.0%', '1M'],
```

### MARQUER comme dépréciés (toujours actifs, shutdown Oct 2026)

```javascript
// ⚠️ DEPRECATED — shutdown Oct 16, 2026
['gemini-2.5-pro',                            'Gemini 2.5 Pro',               'S+', '63.2%', '1M'],
['gemini-2.5-flash',                          'Gemini 2.5 Flash',             'A+', '50.0%', '1M'],
['gemini-2.5-flash-lite',                     'Gemini 2.5 Flash Lite',        'A',  '42.0%', '1M'],
```

### RÉSULTAT FINAL proposé (googleai et gemini)

```javascript
// === Tier S+ — Frontier ===
['gemini-3.5-flash',                          'Gemini 3.5 Flash',             'S+', '—',     '1M'],  // 🆕 May 2026, Stable
['gemini-3.1-pro-preview',                    'Gemini 3.1 Pro Preview',      'S+', '78.0%', '1M'],
// === Tier S ===
['gemini-3-flash-preview',                    'Gemini 3 Flash Preview',      'S',  '65.0%', '1M'],
// === Tier A+ ===
['gemini-3.1-flash-lite',                     'Gemini 3.1 Flash Lite',        'A+', '55.0%', '1M'],  // 🆕 Stable May 2026
// ⚠️ DEPRECATED — shutdown Oct 16, 2026
['gemini-2.5-pro',                            'Gemini 2.5 Pro',               'S+', '63.2%', '1M'],
['gemini-2.5-flash',                          'Gemini 2.5 Flash',             'A+', '50.0%', '1M'],
['gemini-2.5-flash-lite',                     'Gemini 2.5 Flash Lite',        'A',  '42.0%', '1M'],
```

---

## Sources

- [Google AI Models](https://ai.google.dev/gemini-api/docs/models)
- [Google AI Deprecations](https://ai.google.dev/gemini-api/docs/deprecations)
- [Gemini 3.5 Flash Model Card](https://ai.google.dev/gemini-api/docs/models/gemini-3.5-flash)
