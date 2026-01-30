# ⚡ Déploiement Rapide - Checklist

## ✅ Étape 1 : Pousser sur GitHub

Les fichiers sont déjà ajoutés et commités. Il ne reste qu'à pousser :

```bash
git push origin main
```

---

## ✅ Étape 2 : Déployer sur Render

### Option A : Déploiement automatique avec render.yaml (Recommandé)

1. **Va sur [render.com](https://render.com)** et connecte-toi avec GitHub

2. **Clique sur "New +" → "Web Service"**

3. **Connecte ton repository** : `SPAM_HAM_DETECTOR`

4. **Render détectera automatiquement `render.yaml`** ✅
   - Plan : Free
   - Build Command : `pip install -r requirements.txt && python train_model.py`
   - Start Command : `python app.py`

5. **Clique sur "Create Web Service"**

6. **Attends 5-10 minutes** pour le déploiement

7. **Ton API sera disponible sur** : `https://spam-detector-api.onrender.com`

---

### Option B : Configuration manuelle (si render.yaml ne fonctionne pas)

Si l'option automatique ne fonctionne pas :

1. **Plan** : Free
2. **Build Command** : 
   ```
   pip install -r requirements.txt && python train_model.py
   ```
3. **Start Command** : 
   ```
   python app.py
   ```
4. **Environment Variables** :
   - `FLASK_DEBUG` = `0`
   - `PORT` = `10000` (Render le définit automatiquement, mais on peut le mettre)

---

## 🎯 Après le déploiement

### Tester l'API

1. **Health check** :
   ```
   https://TON-URL.onrender.com/health
   ```

2. **Interface web** :
   ```
   https://TON-URL.onrender.com
   ```

3. **API predict** :
   ```bash
   curl -X POST https://TON-URL.onrender.com/predict \
     -H "Content-Type: application/json" \
     -d '{"message": "URGENT! Gagnez 1000€!"}'
   ```

---

## 📝 Notes

- ⏱️ **Premier démarrage** : 30-60 secondes (plan gratuit)
- 💤 **Veille automatique** : Après 15 min d'inactivité
- 🔄 **Mises à jour** : `git push` → Déploiement automatique

---

**🚀 C'est tout ! Ton API est en ligne !**
