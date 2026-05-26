# Groq — Audit de validité des modèles

**Date de vérification :** 2026-05-26
**Source :** console.groq.com / Groq API

---

## Résumé
| Stat | Nombre | Détails |
|------|--------|---------|
| ✅ Confirmés existants | 8 | Tous les modèles listés sont toujours actifs |
| 🗑️ Dépréciés — à retirer | 0 | Aucun modèle de la liste n'est déprécié |
| ❌ 404 / Supprimés — à retirer | 0 | Aucun modèle de la liste n'est supprimé |
| ➕ Nouveaux — à ajouter | 0 | Aucun nouveau modèle de chat LLM pertinent |
| ⚠️ Corrections de config | 4 | Changements de fenêtre de contexte (128k → 131k) |
| 📊 Corrections de score | 1-2 | Scores SWE-bench à vérifier/mettre à jour |

---

## ✅ Modèles CONFIRMÉS opérationnels

| Modèle (sources.js) | ID Groq | Statut Groq | Tier actuel | Score actuel | CTX actuel | CTX réel | Note |
|---|---|---|---|---|---|---|---|
| `llama-3.3-70b-versatile` | llama-3.3-70b-versatile | ✅ Production | A- | 39.5% | 128k | **131,072** | ⚠️ CTX à corriger |
| `meta-llama/llama-4-scout-17b-16e-instruct` | meta-llama/llama-4-scout-17b-16e-instruct | ✅ **Preview** | A | 44.0% | 131k | 131,072 | Toujours en Preview |
| `llama-3.1-8b-instant` | llama-3.1-8b-instant | ✅ Production | B | 28.8% | 128k | **131,072** | ⚠️ CTX à corriger |
| `openai/gpt-oss-120b` | openai/gpt-oss-120b | ✅ Production | S | 60.0% | 128k | **131,072** | ⚠️ CTX à corriger ; SWE-bench = 62.4% |
| `openai/gpt-oss-20b` | openai/gpt-oss-20b | ✅ Production | A | 42.0% | 128k | **131,072** | ⚠️ CTX à corriger ; SWE-bench = 60.7% |
| `qwen/qwen3-32b` | qwen/qwen3-32b | ✅ **Preview** | A+ | 50.0% | 131k | 131,072 | Toujours en Preview |
| `groq/compound` | groq/compound | ✅ Production System | A | 45.0% | 131k | 131,072 | GPT-OSS 120B + Llama 4 Scout |
| `groq/compound-mini` | groq/compound-mini | ✅ Production System | B+ | 32.0% | 131k | 131,072 | GPT-OSS 120B + Llama 3.3 70B |

---

## 🗑️ Modèles DÉPRÉCIÉS / ❌ SUPPRIMÉS

**Aucun modèle de la liste n'est déprécié ou supprimé.** Tous les 8 modèles restent actifs sur la plateforme Groq.

### Modèles dépréciés récents (PAS dans notre liste — pour référence)

| Modèle déprécié | Date de shutdown | Remplacement recommandé | Était dans notre liste ? |
|---|---|---|---|
| `moonshotai/kimi-k2-instruct-0905` | 2026-04-15 | `openai/gpt-oss-120b` | ❌ Non |
| `meta-llama/llama-4-maverick-17b-128e-instruct` | 2026-03-09 | `openai/gpt-oss-120b` | ❌ Non |
| `meta-llama/llama-guard-4-12b` | 2026-03-05 | `openai/gpt-oss-safeguard-20b` | ❌ Non |
| `gemma2-9b-it` | 2025-10-08 | `llama-3.1-8b-instant` | ❌ Non |
| `deepseek-r1-distill-llama-70b` | 2025-10-02 | `llama-3.3-70b-versatile` | ❌ Non |
| `qwen-qwq-32b` | 2025-07-14 | `qwen/qwen3-32b` | ❌ Non |

---

## ➕ Nouveaux modèles à ajouter

**Aucun nouveau modèle de chat/coding LLM pertinent.** Les modèles suivants sont disponibles sur Groq mais ne sont pas pertinents pour free-coding-models :

| Modèle | Type | Pertinence pour coding | Note |
|---|---|---|---|
| `openai/gpt-oss-safeguard-20b` | Preview — Modération/Sécurité | ❌ Non pertinent | Modèle de sécurité, pas de coding |
| `meta-llama/llama-prompt-guard-2-22m` | Preview — Sécurité | ❌ Non pertinent | 512 ctx, modèle de garde |
| `meta-llama/llama-prompt-guard-2-86m` | Preview — Sécurité | ❌ Non pertinent | 512 ctx, modèle de garde |
| `canopylabs/orpheus-v1-english` | Production — TTS | ❌ Non pertinent | Synthèse vocale |
| `canopylabs/orpheus-arabic-saudi` | Preview — TTS | ❌ Non pertinent | Synthèse vocale arabe |
| `whisper-large-v3` | Production — ASR | ❌ Non pertinent | Transcription vocale |
| `whisper-large-v3-turbo` | Production — ASR | ❌ Non pertinent | Transcription vocale |

### Modèles Enterprise-only (non disponibles sur le plan gratuit)

| Modèle | Note |
|---|---|
| `minimax-m2.5` | Enterprise uniquement, pas sur le free tier |
| `qwen3-vl-32b` | Enterprise uniquement, pas sur le free tier |

---

## 📝 Modifications à appliquer dans sources.js

### 1. Corrections de fenêtre de contexte (128k → 131k)

Tous les modèles Groq ont une fenêtre de contexte de 131,072 tokens (soit 131K). Quatre entrées affichent incorrectement '128k'.

```javascript
// ❌ AVANT (actuel)
['llama-3.3-70b-versatile',              'Llama 3.3 70B',      'A-', '39.5%', '128k'],
['llama-3.1-8b-instant',                 'Llama 3.1 8B',       'B',  '28.8%', '128k'],
['openai/gpt-oss-120b',                  'GPT OSS 120B',       'S',  '60.0%', '128k'],
['openai/gpt-oss-20b',                   'GPT OSS 20B',        'A',  '42.0%', '128k'],

// ✅ APRÈS (corrigé)
['llama-3.3-70b-versatile',              'Llama 3.3 70B',      'A-', '39.5%', '131k'],
['llama-3.1-8b-instant',                 'Llama 3.1 8B',       'B',  '28.8%', '131k'],
['openai/gpt-oss-120b',                  'GPT OSS 120B',       'S',  '60.0%', '131k'],
['openai/gpt-oss-20b',                   'GPT OSS 20B',        'A',  '42.0%', '131k'],
```

### 2. Scores SWE-bench — Vérification recommandée

Les scores officiels SWE-bench Verified des pages de modèle Groq :

| Modèle | Score actuel (sources.js) | Score officiel Groq | Action recommandée |
|---|---|---|---|
| `openai/gpt-oss-120b` | 60.0% | **62.4%** (SWE-Bench Verified) | ⚠️ Vérifier et potentiellement mettre à jour vers 62.4% |
| `openai/gpt-oss-20b` | 42.0% | **60.7%** (SWE-Bench Verified) | ⚠️ Écart significatif — investiguer et mettre à jour |
| `qwen/qwen3-32b` | 50.0% | **65.7%** (LiveCodeBench, pas SWE-bench) | Note : benchmark différent |

> **⚠️ Note importante sur les scores** : Les scores dans `sources.js` peuvent provenir de benchmarks différents ou avoir été mesurés à des moments différents. Le projet doit décider si ces scores doivent être mis à jour avec les benchmarks officiels de Groq. L'écart pour GPT-OSS 20B (42.0% vs 60.7%) est particulièrement notable.

### 3. Pas de suppressions nécessaires

Aucun modèle de la liste n'a été déprécié ou supprimé. **Aucune ligne à retirer.**

### 4. Pas d'ajouts nécessaires

Aucun nouveau modèle de coding/chat LLM gratuit n'a été ajouté à la plateforme Groq depuis la dernière mise à jour.

---

## 📋 Détails techniques par modèle (depuis console.groq.com)

### Production Models

| Model ID | Vitesse | Prix (in/out per 1M) | CTX | Max Output | Statut |
|---|---|---|---|---|---|
| `llama-3.1-8b-instant` | 560 tps | $0.05 / $0.08 | 131,072 | 131,072 | Production |
| `llama-3.3-70b-versatile` | 280 tps | $0.59 / $0.79 | 131,072 | 32,768 | Production |
| `openai/gpt-oss-120b` | 500 tps | $0.15 / $0.60 | 131,072 | 65,536 | Production |
| `openai/gpt-oss-20b` | 1000 tps | $0.075 / $0.30 | 131,072 | 65,536 | Production |

### Production Systems

| Model ID | Vitesse | CTX | Max Output | Underlying Models | Statut |
|---|---|---|---|---|---|
| `groq/compound` | ~450 tps | 131,072 | 8,192 | GPT-OSS 120B + Llama 4 Scout | Production System |
| `groq/compound-mini` | ~450 tps | 131,072 | 8,192 | GPT-OSS 120B + Llama 3.3 70B | Production System |

### Preview Models (text LLM)

| Model ID | Vitesse | Prix (in/out per 1M) | CTX | Max Output | Statut |
|---|---|---|---|---|---|
| `meta-llama/llama-4-scout-17b-16e-instruct` | 750 tps | $0.11 / $0.34 | 131,072 | 8,192 | ⚠️ Preview |
| `qwen/qwen3-32b` | 400 tps | $0.29 / $0.59 | 131,072 | 40,960 | ⚠️ Preview |

---

## 🔔 Changements notables sur la plateforme Groq

1. **Kimi K2 déprécié** — `moonshotai/kimi-k2-instruct-0905` arrêté le 15 avril 2026
2. **Llama 4 Maverick déprécié** — `meta-llama/llama-4-maverick-17b-128e-instruct` arrêté le 9 mars 2026
3. **Groq Compound** est maintenant un système de production — GPT-OSS 120B + Llama 4 Scout avec recherche web, exécution de code, automatisation de navigateur
4. **Groq Compound Mini** — GPT-OSS 120B + Llama 3.3 70B, 3x plus rapide que Compound

---

## Sources

- **Modèles Groq supportés** : [console.groq.com/docs/models](https://console.groq.com/docs/models)
- **Dépréciations Groq** : [console.groq.com/docs/deprecations](https://console.groq.com/docs/deprecations)
- **Tarification Groq** : [groq.com/pricing](https://groq.com/pricing)
