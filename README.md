# Umark

Gestion des notes universitaires : sessions, cours, évaluations pondérées, moyenne, lettre et GPA.

```
umark-app/
├── docs/                  ← l'app elle-même (c'est ce dossier qui est mis en ligne)
│   ├── index.html
│   ├── manifest.webmanifest
│   ├── sw.js              ← mode hors ligne
│   ├── favicon.svg
│   └── icons/
├── assets/                ← icône 1024 px et écran de démarrage pour Android/iOS
├── capacitor.config.json  ← réglages de l'app native
└── package.json
```

> Les notes sont enregistrées **sur l'appareil**. Avant de désinstaller l'app ou de changer de téléphone,
> fais **Réglages → Exporter en JSON**, puis **Importer** sur le nouvel appareil.

---

## Étape 1 — Mettre Umark en ligne (gratuit, ~10 min)

1. Crée un compte sur <https://github.com> (gratuit).
2. En haut à droite : **+ → New repository**. Nom : `umark`. Coche **Public**. Clique **Create repository**.
3. Sur la page du dépôt : **uploading an existing file**. Glisse **tout le contenu** du dossier `umark-app`
   (le dossier `docs`, `assets`, `README.md`, `package.json`…). Clique **Commit changes**.
4. **Settings → Pages**. Sous *Build and deployment* : Source = **Deploy from a branch**,
   Branch = **main**, dossier = **/docs**. Clique **Save**.
5. Attends 1 à 2 minutes. L'adresse s'affiche en haut de la page Pages :
   `https://TON-PSEUDO.github.io/umark/`

## Étape 2 — L'installer sur ton téléphone

Ouvre l'adresse ci-dessus sur ton téléphone, puis :

- **iPhone** : dans **Safari**, bouton **Partager → Sur l'écran d'accueil → Ajouter**.
- **Android** : dans **Chrome**, menu **⋮ → Installer l'application** (ou « Ajouter à l'écran d'accueil »).

Umark apparaît avec son icône, s'ouvre en plein écran et fonctionne sans Internet.
Pour faire essayer l'app à quelqu'un, envoie-lui simplement l'adresse : chacun garde ses propres notes.

**Mettre à jour l'app plus tard :** remplace `docs/index.html` sur GitHub, et dans `docs/sw.js`
change `umark-v1` en `umark-v2` (puis v3…). Les téléphones récupèrent la nouvelle version à la prochaine ouverture.

---

## Étape 3 (optionnelle) — Version Android / iPhone « native »

C'est la version qu'on enverrait plus tard sur Google Play ou l'App Store.
**Ce guide s'arrête volontairement avant la publication sur les stores.**

### Ce qu'il faut sur ton ordi

- **Node.js** 22 ou plus récent : <https://nodejs.org>
- **Android** : **Android Studio** (Windows, Mac ou Linux) : <https://developer.android.com/studio>
- **iPhone** : un **Mac** avec **Xcode** (App Store du Mac). Impossible de construire l'app iPhone sur Windows.

### Avant de commencer

Dans `capacitor.config.json`, remplace `com.umark.app` par un identifiant à toi, par exemple
`com.tonnom.umark` (minuscules, sans espaces). Il doit être unique et ne pourra plus changer une fois l'app publiée.

### Commandes (dans un terminal ouvert dans le dossier `umark-app`)

```bash
npm install                 # installe Capacitor
npx cap add android         # crée le projet Android (dossier android/)
npx cap add ios             # crée le projet iPhone (dossier ios/) — Mac seulement
npm run icons               # génère toutes les icônes et l'écran de démarrage depuis assets/
```

### Essayer sur un téléphone Android

```bash
npm run android             # copie l'app et ouvre Android Studio
```

1. Sur le téléphone : **Paramètres → À propos → appuie 7 fois sur « Numéro de build »**,
   puis **Options pour les développeurs → Débogage USB** activé.
2. Branche le téléphone en USB, choisis-le en haut d'Android Studio et clique **▶ Run**.
3. Pour obtenir un fichier à installer/partager : **Build → Build App Bundle(s) / APK(s) → Build APK(s)**.

### Essayer sur un iPhone (Mac)

```bash
npm run ios                 # copie l'app et ouvre Xcode
```

1. Dans Xcode : clique **App** (à gauche) → onglet **Signing & Capabilities** → **Team** :
   ajoute ton identifiant Apple (gratuit pour essayer sur ton propre iPhone).
2. Branche l'iPhone, choisis-le en haut de Xcode, clique **▶**.
3. Sur l'iPhone, si demandé : **Réglages → Général → VPN et gestion de l'appareil** → faire confiance au développeur,
   et activer le **Mode développeur** (Réglages → Confidentialité et sécurité).

### Après une modification de `docs/`

```bash
npx cap sync                # recopie l'app dans les projets Android et iPhone
```

---

## 🛑 Arrêt ici : publication sur Google Play / App Store

La suite (compte développeur, fiche de l'app, captures d'écran, politique de confidentialité,
signature de la version finale, envoi en vérification) n'est pas faite.
Reviens vers Claude quand tu veux passer à cette étape.
