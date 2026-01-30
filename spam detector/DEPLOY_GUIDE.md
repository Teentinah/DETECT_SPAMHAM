# 🚀 Guide de Déploiement sur Render

## 📋 Prérequis

1. **Compte GitHub** (gratuit) : [github.com](https://github.com)
2. **Compte Render** (gratuit) : [render.com](https://render.com)

---

## 📦 Étape 1 : Préparer Git et GitHub

### 1.1 Ajouter tous les fichiers à Git

```bash
git add .
```

### 1.2 Créer un commit

```bash
git commit -m "Initial commit: Spam Detector avec front-end web"
```

### 1.3 Créer un repository sur GitHub

1. Va sur [github.com](https://github.com) et connecte-toi
2. Clique sur **"New repository"** (bouton vert)
3. Nomme-le : `spam-detector` (ou un autre nom)
4. **Ne coche PAS** "Initialize with README" (on a déjà les fichiers)
5. Clique sur **"Create repository"**

### 1.4 Connecter ton repo local à GitHub

GitHub te donnera des commandes. Utilise celles-ci (remplace `TON_USERNAME` par ton nom d'utilisateur GitHub) :

```bash
git remote add origin https://github.com/TON_USERNAME/spam-detector.git
git branch -M main
git push -u origin main
```

**Si tu as déjà un remote**, vérifie-le :
```bash
git remote -v
```

---

## 🌐 Étape 2 : Déployer sur Render

### 2.1 Créer un compte Render

1. Va sur [render.com](https://render.com)
2. Clique sur **"Get Started for Free"**
3. Connecte-toi avec **GitHub** (recommandé)

### 2.2 Créer un nouveau Web Service

1. Dans le dashboard Render, clique sur **"New +"**
2. Sélectionne **"Web Service"**
3. Connecte ton repository GitHub `spam-detector`
4. Render détectera automatiquement le fichier `render.yaml` ✅

### 2.3 Configuration automatique

Le fichier `render.yaml` configure tout automatiquement :
- ✅ Plan gratuit
- ✅ Installation des dépendances
- ✅ Entraînement du modèle
- ✅ Démarrage de l'API

**Tu n'as rien à modifier !** Clique simplement sur **"Create Web Service"**

### 2.4 Attendre le déploiement

- Render va :
  1. Cloner ton code
  2. Installer les dépendances (`pip install -r requirements.txt`)
  3. Entraîner le modèle (`python train_model.py`)
  4. Lancer l'API (`python app.py`)

⏱️ **Temps estimé : 5-10 minutes**

### 2.5 Obtenir l'URL de ton API

Une fois déployé, Render te donnera une URL comme :
```
https://spam-detector-api.onrender.com
```

**⚠️ Important :** La première fois, ça peut prendre 30-60 secondes à démarrer (plan gratuit).

---

## 🔧 Étape 3 : Tester ton API déployée

### 3.1 Tester l'endpoint health

Ouvre dans ton navigateur :
```
https://TON-URL.onrender.com/health
```

Tu devrais voir : `{"status":"ok"}`

### 3.2 Tester l'interface web

Ouvre :
```
https://TON-URL.onrender.com
```

Tu verras ton interface de détection de spam ! 🎉

### 3.3 Tester l'API avec curl (optionnel)

```bash
curl -X POST https://TON-URL.onrender.com/predict \
  -H "Content-Type: application/json" \
  -d '{"message": "URGENT! Gagnez 1000€ maintenant!"}'
```

---

## 🔄 Mises à jour futures

Quand tu modifies ton code :

```bash
git add .
git commit -m "Description de tes changements"
git push
```

Render redéploiera automatiquement ! ✨

---

## ⚠️ Notes importantes

1. **Plan gratuit Render** :
   - Le service se met en veille après 15 min d'inactivité
   - Le premier démarrage après veille prend 30-60 secondes
   - C'est normal et gratuit !

2. **Modèles** :
   - Les modèles (`.pkl`) sont inclus dans Git
   - Ils seront entraînés automatiquement lors du déploiement

3. **Variables d'environnement** :
   - `PORT` est automatiquement défini par Render
   - `FLASK_DEBUG=0` en production (défini dans `render.yaml`)

---

## 🆘 Dépannage

### Le déploiement échoue ?

1. Vérifie les **logs** dans le dashboard Render
2. Assure-toi que `requirements.txt` contient toutes les dépendances
3. Vérifie que les modèles sont bien dans le repo Git

### L'API ne répond pas ?

1. Attends 30-60 secondes (premier démarrage)
2. Vérifie l'URL (doit finir par `/health` ou `/`)
3. Consulte les logs dans Render

---

**🎉 Félicitations ! Ton API est maintenant en ligne !**
