# 📝 redt974's Write-Ups

Bienvenue dans mon dépôt GitHub regroupant mes write-ups de CTFs, Root-Me, TryHackMe et notes de pentest. Ce projet utilise **MkDocs** avec le thème **Material for MkDocs** pour générer une documentation propre, claire et facilement navigable.

## 📂 Structure du dépôt

| Branche       | Description                                         |
|---------------|-----------------------------------------------------|
| `main`        | Contient les fichiers sources Markdown (`docs/`).   |
| `gh-pages`    | Contient le site statique généré (`site/`) utilisé par **GitHub Pages** pour l’hébergement. ⚠️ Ne pas modifier manuellement.

---

## 🚀 Déploiement

### 🔧 Pour mettre à jour le site GitHub Pages :

```bash
mkdocs gh-deploy
```

Cette commande :
- Génère le site statique dans le dossier `site/`.
- Publie automatiquement le contenu sur la branche `gh-pages`.

### 💾 Pour mettre à jour la branche `main` avec tes fichiers Markdown :

```bash
git add .
git commit -m "<même commit que gh-deploy>"
git push
```

---

## 📚 Génération locale

Pour travailler localement et prévisualiser ton site :

```bash
mkdocs serve
```

Accède ensuite à : [http://localhost:8000](http://localhost:8000)

---

## 📦 Technologies

- [MkDocs](https://www.mkdocs.org/)
- [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/)

---

## 🔗 Liens utiles

- 🔥 Site en ligne : [https://redt974.github.io/write-ups/](https://redt974.github.io/write-ups/)
- 🧑‍💻 Mon Portfolio : [https://tv-portfolio.vercel.app/](https://tv-portfolio.vercel.app/)
- ⚔️ Mon profil TryHackMe : [https://tryhackme.com/p/redt974](https://tryhackme.com/p/redt974)
- 💀 Mon profil Root-Me : [https://www.root-me.org/redt974](https://www.root-me.org/redt974)

---

## ©️ Auteur

**Thibaut Vandier**  
Passionné de cybersécurité, CTF et reverse engineering.

```

---