# Héberger ton app web gratuitement (Render)

Ton application **Spam Detector** (Flask + interface web) peut être hébergée gratuitement sur **Render.com**. Une seule URL servira à la fois l’interface web et l’API.

---

## Option 1 : Tout héberger sur Render (recommandé)

### Étape 1 : Préparer le dépôt Git

Dans le dossier **spam detector** :

```bash
cd "C:\Users\USER\Desktop\Projet ML M2\spam detector"
git init
git add .
git commit -m "Spam detector - prêt pour déploiement"
```

**Important :** Les fichiers `models/spam_model.pkl` et `models/vectorizer.pkl` doivent être inclus (pas dans un `.gitignore` qui les exclut), sinon Render ne pourra pas lancer l’API.

### Étape 2 : Créer un dépôt sur GitHub

1. Va sur [github.com](https://github.com) et crée un nouveau dépôt (ex. `spam-detector`).
2. Ne coche pas « Add a README » si tu pousses un projet existant.
3. Associe ton projet local et pousse le code :

```bash
git remote add origin https://github.com/TON-USERNAME/spam-detector.git
git branch -M main
git push -u origin main
```

Remplace `TON-USERNAME` par ton identifiant GitHub.

### Étape 3 : Déployer sur Render

1. Va sur [render.com](https://render.com) et inscris-toi (gratuit).
2. Connecte ton compte **GitHub** (Settings → Connect account).
3. Clique sur **New** → **Web Service**.
4. Choisis le dépôt **spam-detector**.
5. Render détecte automatiquement :
   - **Environment** : Python
   - **Build Command** : `pip install -r requirements.txt`
   - **Start Command** : `python app.py`
6. Vérifie que le **Plan** est **Free**.
7. Clique sur **Create Web Service**.

Le premier déploiement peut prendre 5–10 minutes (installation des dépendances + modèles).

### Étape 4 : Utiliser ton app en ligne

Une fois le déploiement terminé, Render te donne une URL du type :

**https://spam-detector-api.onrender.com**

- **Page d’accueil (interface web)** : ouvre cette URL dans le navigateur.
- **API** :
  - `GET https://ton-app.onrender.com/health`
  - `POST https://ton-app.onrender.com/predict` avec un JSON `{"message": "ton texte"}`.

Le frontend (HTML/JS dans `static/`) utilise déjà `window.location.origin`, donc il appellera automatiquement la même URL en production. Aucune modification de code n’est nécessaire.

---

## Limites du plan gratuit Render

- Le service s’**endort après ~15 minutes** sans requête.
- Le **premier appel** après une période d’inactivité peut prendre **30–50 secondes** (réveil du serveur).
- C’est normal ; les appels suivants sont rapides.

---

## Option 2 : Héberger l’app Flutter (Web) séparément

Si tu veux aussi mettre en ligne l’application **Flutter** (mon_premier_projet) en web :

### 1. Déployer d’abord l’API sur Render (Option 1)

Tu obtiens une URL du type : `https://spam-detector-api.onrender.com`.

### 2. Configurer l’URL de l’API dans Flutter

Dans `mon_premier_projet/lib/main.dart`, remplace l’URL par celle de Render :

```dart
static const String _baseUrl = "https://spam-detector-api.onrender.com";
```

(Remplace par ta vraie URL Render.)

### 3. Build Flutter pour le web

```bash
cd "C:\Users\USER\Desktop\Projet ML M2\mon_premier_projet"
flutter build web
```

Les fichiers générés sont dans `build/web/`.

### 4. Héberger le build Flutter sur Vercel (gratuit)

1. Va sur [vercel.com](https://vercel.com) et connecte ton compte GitHub.
2. **Add New** → **Project** → importe le dépôt qui contient **mon_premier_projet** (ou seulement le dossier Flutter).
3. **Root Directory** : mets `mon_premier_projet`.
4. **Build Command** : `flutter build web` (ou laisse Vercel le détecter si tu as un script).
5. **Output Directory** : `build/web`.
6. Déploie.

Tu auras une URL du type `https://mon-premier-projet.vercel.app` qui appelle l’API sur Render.

**Alternative :** Tu peux aussi héberger le contenu de `build/web` sur **Netlify** ou **GitHub Pages** en uploadant le dossier `build/web`.

---

## Récapitulatif

| Composant        | Plateforme gratuite | URL typique                    |
|------------------|---------------------|---------------------------------|
| API + site web   | **Render**          | https://spam-detector-api.onrender.com |
| App Flutter (web)| **Vercel** / Netlify| https://ton-projet.vercel.app   |

Pour commencer, l’**Option 1** (tout sur Render) suffit pour avoir ton app web en ligne gratuitement.
