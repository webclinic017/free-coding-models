# ZAI (Z.ai) — Audit de validité des modèles

**Date de vérification :** 2026-05-26
**Source :** docs.z.ai (pricing, model docs, release notes), OpenLM SWE-bench leaderboard

---

## Résumé
| Stat | Nombre | Détails |
|------|--------|---------|
| ✅ Confirmés existants | 2 | GLM-4.7-Flash, GLM-4.5-Flash |
| 🗑️ Dépréciés — à retirer | 0 | Aucun modèle déprécié |
| ➕ Nouveaux — à ajouter | 0 | Aucun nouveau modèle gratuit |
| ⚠️ À vérifier | 2 | SWE-bench scores non confirmés officiellement |

---

## ✅ Modèles CONFIRMÉS opérationnels

### `zai/glm-4.7-flash` — GLM-4.7-Flash

| Attribut | sources.js | Officiel (2026-05-26) | Statut |
|----------|-----------|----------------------|--------|
| Model ID | `zai/glm-4.7-flash` | `glm-4.7-flash` | ✅ Correct |
| Display Name | GLM-4.7-Flash | GLM-4.7-Flash | ✅ Correct |
| Tier | S | — | ✅ Justifié |
| SWE-bench | 59.2% | ~59.2% (communauté) | ⚠️ Approximatif |
| Context | 200k | 200K | ✅ Correct |
| Prix | — | **Gratuit** | ✅ Confirmé free |

### `zai/glm-4.5-flash` — GLM-4.5-Flash

| Attribut | sources.js | Officiel (2026-05-26) | Statut |
|----------|-----------|----------------------|--------|
| Model ID | `zai/glm-4.5-flash` | `glm-4.5-flash` | ✅ Correct |
| Display Name | GLM-4.5-Flash | GLM-4.5-Flash | ✅ Correct |
| Tier | S | — | ⚠️ Potentiellement surévalué (modèle plus ancien) |
| SWE-bench | 59.2% | Non confirmé | ⚠️ Non vérifié |
| Context | 128k | 128K | ✅ Correct |
| Prix | — | **Gratuit** | ✅ Confirmé free |

---

## ➕ Nouveaux modèles (payants — ne pas ajouter)

| Modèle | Prix Input/Output | Context | SWE-bench |
|--------|-------------------|---------|-----------|
| GLM-5.1 | $1.40/$4.40 | 200K | 74.4% |
| GLM-5 | $1.00/$3.20 | 200K | 72.8% |
| GLM-4.7 | $0.60/$2.20 | 200K | 73.8% |
| GLM-4.7-FlashX | $0.07/$0.40 | 200K | — |
| GLM-4.5 | $0.60/$2.20 | 128K | 64.2% |
| GLM-4.5-Air | $0.20/$1.10 | 128K | 57.6% |

**Verdict :** ❌ Tous payants, ne pas ajouter.

---

## 📝 Modifications à appliquer dans sources.js

**Aucune modification nécessaire.** Les deux modèles sont toujours actifs et gratuits.

### Recommandations optionnelles :
- **GLM-4.5-Flash** : Le tier `S` pourrait être rétrogradé à `A+` vu qu'il est moins performant que GLM-4.7-Flash
- **SWE-bench** : Les scores de 59.2% ne sont pas confirmés officiellement par Z.ai

---

## Sources

- **Z.ai Pricing** : [docs.z.ai/guides/overview/pricing](https://docs.z.ai/guides/overview/pricing)
- **Z.ai GLM-4.7 Docs** : [docs.z.ai/guides/llm/glm-4.7](https://docs.z.ai/guides/llm/glm-4.7)
- **Z.ai GLM-4.5 Docs** : [docs.z.ai/guides/llm/glm-4.5](https://docs.z.ai/guides/llm/glm-4.5)
- **OpenLM SWE-bench** : [openlm.ai/swe-bench](https://openlm.ai/swe-bench)
