# Estimation & négociation — Maison / Terrain (06)

Outil autonome d'aide à l'estimation et à la négociation d'un bien immobilier
(côté acheteur, Alpes-Maritimes), à héberger sur **GitHub Pages**.

Page unique (`index.html`), aucune dépendance, aucune donnée inventée :
tu saisis les chiffres réels, l'outil applique la méthode (décomposition,
charge foncière, comparables DVF), déroule la checklist et sort une
fourchette + une marge de négociation.

## Fonctions automatiques

| Fonction | Dépend de | Marche sur GitHub Pages ? |
|---|---|---|
| Calcul estimation / négo / premier jet | rien | Oui, toujours |
| Code INSEE depuis la commune | `geo.api.gouv.fr` (appel direct) | Oui |
| Lecture d'annonce (photo/texte → champs) | ton IA (clé) | Oui, si IA connectée |
| Analyse rédigée | ton IA (clé) | Oui, si IA connectée |
| Médianes DVF | API Tabular `data.gouv` (appel direct) | **Dépend du CORS de l'API** (voir plus bas) |
| Récupération d'une annonce par lien | — | **Non** (anti-bot / CORS des sites d'annonces) |

## Connecter son IA

Dans le panneau **« Connexion IA »** en haut de la page :

1. Choisis le fournisseur : **Anthropic (Claude)**, **OpenAI (ChatGPT)**,
   ou **Compatible OpenAI** (OpenRouter, Mistral, serveur local…).
2. Renseigne le **modèle** (ex. `claude-sonnet-4-5`, `gpt-4o-mini`) et,
   pour le mode compatible, l'**URL de base** (ex. `https://openrouter.ai/api/v1`).
3. Colle ta **clé API**, puis **Enregistrer** et **Tester**.

La clé est stockée **uniquement dans ton navigateur** (localStorage). Les
appels partent de ton navigateur vers le fournisseur choisi, directement.

## Sécurité des clés (important)

- **Ne mets JAMAIS ta clé API dans le code source** ni dans un commit.
  Elle se saisit à l'usage dans le panneau, pas dans un fichier du dépôt.
- La page peut être publique sans risque pour ta clé : elle n'est pas dans
  le dépôt, seulement dans TON navigateur.
- Évite les ordinateurs partagés : qui a accès à ce navigateur peut lire la clé.
- Les appels directs navigateur exposent la clé côté client (c'est le prix
  du « sans serveur »). Pour un usage sensible, mets une clé à budget limité.

## Déploiement GitHub Pages

1. Crée un dépôt (ex. `estimation-06`) et dépose `index.html` (et ce `README.md`) à la racine.
2. `Settings` → `Pages` → `Source : Deploy from a branch` → branche `main`, dossier `/ (root)`.
3. La page sera servie sur `https://<ton-user>.github.io/estimation-06/`.

## Limite DVF (CORS)

Les médianes DVF appellent l'API Tabular de data.gouv directement depuis le
navigateur. Si l'API ne renvoie pas les en-têtes CORS, l'appel échoue et
l'outil te le dit (repli : saisie manuelle de la médiane en méthode C, ou
récupération via une conversation Claude). C'est à valider une fois la page
en ligne.

## Avertissement

Outil d'aide à la décision. Ne remplace pas un certificat d'urbanisme, une
étude de sol, ni un devis d'artisan. Les coûts de rénovation sont indicatifs.
