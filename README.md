# DOA · Espace enquêtes

Site de la Drug Observation Agency : tableaux d'enquête, plans d'assaut, organigrammes, cartographies de tunnels et rapports d'enquête, avec export PDF, PNG ou JPG.

## Contenu du dossier

| Fichier | Rôle |
|---|---|
| `index.html` | Le site complet (logo et images inclus). |
| `config.js` | La configuration Firebase, à remplir pour partager les tableaux en direct. |
| `firestore.rules` | Les règles de sécurité à coller dans Firebase. |
| `logo-doa.png` | Le logo, pour la page du dépôt. |

## 1. Mettre le site en ligne avec GitHub Pages

1. Connecte-toi sur [github.com](https://github.com) (ou crée un compte gratuit).
2. En haut à droite, clique sur **+** puis **New repository**.
3. Nom du dépôt : `doa-tool`. Coche **Public** (GitHub Pages gratuit demande un dépôt public), puis clique sur **Create repository**.
4. Sur la page du dépôt, clique sur **uploading an existing file** (ou **Add file → Upload files**).
5. Glisse les fichiers `index.html`, `config.js`, `firestore.rules`, `README.md` et `logo-doa.png`, puis clique sur **Commit changes**.
6. Va dans **Settings → Pages**. Sous **Build and deployment**, choisis **Source : Deploy from a branch**, branche **main**, dossier **/ (root)**, puis **Save**.
7. Attends une à deux minutes et recharge la page : l'adresse du site s'affiche en haut, du type `https://TON-PSEUDO.github.io/doa-tool/`.

À ce stade, le site marche déjà. Sans Firebase, **chaque personne garde ses propres tableaux dans son navigateur** : rien n'est partagé.

## 2. Activer le travail à plusieurs (Firebase, gratuit)

1. Va sur [console.firebase.google.com](https://console.firebase.google.com) et connecte-toi avec un compte Google.
2. **Créer un projet** → nom `doa-tableau` → tu peux désactiver Google Analytics → **Créer**.
3. Menu de gauche **Créer → Firestore Database** → **Créer une base de données** → emplacement `eur3 (europe-west)` → **mode production** → **Créer**.
4. Dans Firestore, onglet **Règles** : remplace tout par le contenu de `firestore.rules`, puis **Publier**.
5. Menu **Créer → Authentication** → **Commencer** → onglet **Mode de connexion** → **Anonyme** → **Activer** → **Enregistrer**.
6. Toujours dans Authentication, onglet **Paramètres → Domaines autorisés** → **Ajouter un domaine** → `TON-PSEUDO.github.io`.
7. Roue dentée en haut à gauche → **Paramètres du projet** → en bas, **Vos applications** → icône **`</>`** (Web) → surnom `doa` → **Enregistrer l'application**. Firebase affiche un bloc `const firebaseConfig = { ... }`.
8. Sur GitHub, ouvre `config.js` → icône crayon (**Edit**) → remplace `window.DOA_FIREBASE = null;` par :
   ```js
   window.DOA_FIREBASE = {
     apiKey: "...",
     authDomain: "...",
     projectId: "...",
     storageBucket: "...",
     messagingSenderId: "...",
     appId: "..."
   };
   ```
   avec les valeurs copiées depuis Firebase, puis **Commit changes**.
9. Une minute plus tard, recharge le site. Chaque personne donne son nom au premier passage, et en haut à droite tu vois **« En direct · à jour »** et les avatars des collègues connectés.

## Bon à savoir

- **Qui peut modifier :** avec ces règles, toute personne qui ouvre l'adresse du site peut lire et modifier les tableaux. Ne partage le lien qu'avec ton équipe.
- **La clé `apiKey` peut être publique :** chez Firebase, cette clé sert à identifier le projet, pas à le protéger. C'est normal qu'elle soit visible dans un dépôt public.
- **Gratuit :** l'offre gratuite de Firebase (plan Spark) suffit largement pour une équipe. Les curseurs en direct sont désactivés sur cette version pour rester dans ces limites. Tu vois toujours qui est connecté, l'élément que chacun sélectionne et le bloc de rapport que chacun écrit.
- **Images :** elles sont enregistrées dans les tableaux eux-mêmes et réduites automatiquement. Évite d'en mettre des dizaines très lourdes sur un seul tableau.
- **Mettre à jour le site :** remplace `index.html` sur GitHub (**Add file → Upload files**). Les tableaux enregistrés dans Firebase ne bougent pas.
