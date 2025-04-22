# 📦 Reiletai
> 🌐 Site en ligne : https://reiletai.baleras.fr

Ce projet regroupe deux applications Dockerisées :

- **API** : service FastAPI (`/api`)
- **Frontend** : application Next.js en mode standalone (`/web`)

Vous pouvez démarrer le projet de deux manières :

1. **Développement local** (depuis les sources)
2. **Production** (avec les images Docker Hub)

<b><span style="color:red;">Attention : le réseau de l'UQAC bloque notre application. Il est conseillé de télécharger toutes les images dont la taille finale sur le disque est d'environ 11Go et de tester sur un réseau sans réstrictions.</span></b>

---

## 🚀 1. Développement local

### Prérequis

- Git
- Docker ≥ 20.10
- Docker Compose ≥ 1.29
- NVidia CUDA Toolkit ≥ 18.8 : https://developer.nvidia.com/cuda-downloads
- (Linux uniquement) NVidia Container Toolkit : https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html

### Étapes

0. Installer les prérequis obligatoires au bon fonctionnement

1. **Cloner les dépôts** :  
   ```bash
   git clone https://github.com/ReiletaI/api.git api
   git clone https://github.com/ReiletaI/web.git web
   ```
2. **Configuration des variables d'environnement** :  
   ```bash
   cd api
   cp .env.example .env
   cd ../web
   cp .env.local.example .env.local
   ```
   Remplissez les champs nécessaires

3. **Lancer les services** :  
   ```bash
   docker-compose up --build -d
   ```
   Sur windows avec support CUDA :
   ```bash
   docker-compose --profile gpu up --build
   ```
   (> Le fichier `docker-compose.yml` doit définir les services `backend` et `frontend` pointant vers `./api` et `./web`.)

5. **Accès** :  
   - API : http://localhost:8123  
   - Frontend : http://localhost:3000


## ⚡️ 2. Production (Docker Hub images)

Vous pouvez déployer rapidement en utilisant les images publiées sur Dockerhub :

Lancez :
```bash
docker compose -f docker-compose.prod.yml up -d
```

## 🛠️ 3. Mode Sans GPU

Si vous n'avez pas de GPU, vous pouvez utiliser le mode sans GPU, grâce à l'image `esscraye/reiletai-api:dev`.

NB : Un fonctionnement avec GPU est privilégié pour les performances.

Lancez le docker-compose.dev pour ça :
```bash
docker compose -f docker-compose.dev.yml up -d
```
