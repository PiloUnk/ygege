# Patches Directory

Ce dossier contient les patches personnalisés appliqués au code upstream de YGGé.

## custom.patch

Ce fichier contient les modifications personnalisées appliquées à la branche upstream/develop.

### Contenu des modifications

- **docker/Dockerfile** : Changement de l'URL source de l'image
- **src/rest/mod.rs** : Ajout du endpoint `download_magnet`
- **src/rest/search.rs** : Renommage du paramètre `connarr` en `sortcat`
- **src/rest/torrent.rs** : Ajout du endpoint pour télécharger des fichiers magnet
- **website/** : Mise à jour de la documentation API
- **ygege.yml & ygege-en.yml** : Ajustements de configuration

### Mise à jour du patch

Après avoir intégré les changements de l'upstream et appliqué vos propres modifications :

```bash
# 1. Récupérer les dernières modifications upstream
git fetch upstream

# 2. Merger upstream dans votre branche develop
git merge upstream/develop

# 3. Régénérer le patch
git diff upstream/develop develop > patches/custom.patch

# 4. Commiter le patch mis à jour
git add patches/custom.patch
git commit -m "Update custom.patch"
```

### Workflow GitHub

Le workflow `.github/workflows/build-develop.yml` utilise ce patch pour :
1. Cloner la branche upstream/develop
2. Appliquer `custom.patch`
3. Builder l'image Docker multi-architecture (amd64, arm64)
4. Pusher vers `ghcr.io/pilounk/ygege:develop`

Le workflow se déclenche :
- Sur push vers la branche develop
- Manuellement via workflow_dispatch
