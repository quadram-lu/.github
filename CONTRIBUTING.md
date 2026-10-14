# Règles de contribution – Quadram

Ce document décrit comment l'équipe Quadram travaille avec Git et GitHub.
Il s'applique à tous les dépôts de l'organisation `quadram-lu`.

## 1. Les branches

| Branche | Rôle | Qui écrit dedans |
|---|---|---|
| `main` | Développement de la prochaine version. Doit toujours compiler. | Personne directement : uniquement par Pull Request |
| `release/x.y` | Version livrée aux clients (ex. `release/3.2`). Reçoit uniquement des correctifs. | Personne directement : uniquement par Pull Request |
| `feature/<n°>-<description>` | Développement d'une évolution | Le développeur concerné |
| `fix/<n°>-<description>` | Correction d'un bug | Le développeur concerné |

- `<n°>` = numéro de l'issue GitHub (ex. `feature/142-export-pdf`, `fix/150-calcul-tva`).
- Noms en minuscules, sans accents ni espaces, mots séparés par des tirets.
- Une branche = un sujet. Elle vit quelques jours, pas quelques semaines.

## 2. Développer une évolution

1. Partir d'une `main` à jour.
2. Créer la branche `feature/<n°>-<description>`.
3. Committer régulièrement.
4. Ouvrir une Pull Request vers `main` et demander la relecture de `@quadram-lu/lead-dev`.
5. Après approbation : fusion, puis suppression de la branche.

## 3. Corriger un bug

### Bug sur le développement en cours (pas encore livré)

Branche `fix/<n°>-<description>` créée depuis `main`, Pull Request vers `main`.

### Bug signalé par un client sur une version livrée (patch)

1. Créer `fix/<n°>-<description>` **depuis `release/x.y`** (la version du client).
2. Pull Request **vers `release/x.y`**.
3. Après fusion, le responsable pose le tag de patch (ex. `v3.2.1`).
4. **Reporter le correctif dans `main`** (cherry-pick via une Pull Request).
   Sans ce report, le bug réapparaîtra dans la version suivante.

## 4. Les Pull Requests

- Toute modification de `main` ou `release/*` passe par une Pull Request.
- 1 approbation obligatoire, par une autre personne que l'auteur.
- Toute nouvelle modification après approbation demande une nouvelle relecture.
- Tous les commentaires de relecture doivent être résolus avant la fusion.
- Lier l'issue dans la description : `Fixes #150` (l'issue se ferme automatiquement à la fusion dans `main`).
- Préférer de petites PR : plus faciles et plus rapides à relire.

## 5. Les messages de commit

- En français, à l'impératif, courts et explicites : `Corrige l'arrondi de TVA sur les avoirs`.
- Référencer l'issue si possible : `Corrige l'arrondi de TVA sur les avoirs (#150)`.
- À éviter : `wip`, `modif`, `correction`, `test`.

## 6. Versions et livraisons

- Numérotation `X.Y.Z` : `X` version majeure, `Y` version mineure, `Z` patch.
- Chaque version livrée reçoit un tag `vX.Y.Z` et une GitHub Release.
- Une nouvelle version mineure ou majeure crée une branche `release/X.Y` depuis `main`.
- Une branche `release/x.y` est conservée tant que des clients utilisent cette version.

## 7. Sécurité

- Double authentification obligatoire sur le compte GitHub.
- Ne jamais committer de mot de passe, clé d'API, chaîne de connexion ou certificat.
- Ne jamais mettre de données personnelles de clients dans une issue, un commit ou une PR.
