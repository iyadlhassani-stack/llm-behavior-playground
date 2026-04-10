# LLM Behavior Playground

Avant de comprendre les défauts d'un LLM, il faut comprendre comment il réfléchit.
Ce projet observe le comportement du modèle de l'intérieur — pas ses erreurs, ses mécanismes.

## Ce que j'ai exploré

**Notebook 01 — Sampling & Decoding**
Un LLM génère du texte token par token. À chaque étape, il calcule une distribution
de probabilités sur tout son vocabulaire et choisit le token suivant.

- **Greedy decoding** : à chaque étape, on prend le token le plus probable.
  Résultat : déterministe, stable, mais répétitif.
- **Sampling** : on tire au sort dans la distribution de probabilités.
  Résultat : varié, créatif, parfois incohérent.

Leçon : le modèle ne change pas — c'est la stratégie de décodage
qui change comment on explore ses probabilités.

**Notebook 02 — Temperature**
La température reshapes la distribution de probabilités avant le sampling.
Basse (0.1-0.3) → distribution pointue, le modèle est prévisible.
Haute (1.0+) → distribution plate, le modèle devient créatif mais instable.
C'est le curseur entre déterminisme et créativité.

**Notebook 03 — Top-k vs Top-p**
Deux façons de contraindre le vocabulaire à chaque étape :
- **Top-k** : garde uniquement les k tokens les plus probables (nombre fixe).
- **Top-p** : garde les tokens jusqu'à atteindre un seuil de probabilité cumulée (adaptatif).
Top-p s'adapte mieux quand la distribution est très plate ou très pointue.

**Notebook 04 — Seeds et déterminisme**
Quand on utilise le sampling, le modèle tire au sort — donc deux runs
donnent des résultats différents.

Un **seed** c'est la graine du générateur aléatoire. Fixer le seed fixe
le tirage au sort, ce qui rend les résultats reproductibles.
Sans seed fixé : chaque run est unique. Avec seed fixé : résultats identiques à chaque fois.

**Notebook 05 — Constraint following**
Est-ce que le modèle suit vraiment les instructions de format ?
Réponse : pas toujours. Le sampling augmente les violations.
Un LLM optimise des probabilités, pas des règles — d'où la nécessité
de validation et retry en production.

## Ce que j'ai compris en le buildant

Ces 5 notebooks ont posé les bases de tout ce qui a suivi.
Comprendre la température, les seeds et le constraint following
était nécessaire avant de mesurer pourquoi les LLMs échouent dans LLM-Reliability-Layer.

## Stack

Python · HuggingFace Transformers · Google Colab
