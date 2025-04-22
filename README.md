# 📦 Reiletai
> 🌐 Site en ligne : https://reiletai.baleras.fr

Ce projet regroupe deux applications Dockerisées :

- **API** : service FastAPI (`/api`)
- **Frontend** : application Next.js en mode standalone (`/web`)

Vous pouvez démarrer le projet de deux manières :

1. **Développement local** (depuis les sources)
2. **Production** (avec les images Docker Hub)

---

## 🚀 1. Développement local

### Prérequis

- Git
- Docker ≥ 20.10
- Docker Compose ≥ 1.29

### Étapes

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
   remplissez les champs nécessaires

3. **Lancer les services** :  
   ```bash
   docker-compose up --build -d
   ```
   (> Le fichier `docker-compose.yml` doit définir les services `backend` et `frontend` pointant vers `./api` et `./web`.)

4. **Accès** :  
   - API : http://localhost:8123  
   - Frontend : http://localhost:3000


## ⚡️ 2. Production (Docker Hub images)

Vous pouvez déployer rapidement en utilisant les images publiées :

Lancez :
```bash
docker compose -f docker-compose.prod.yml up -d
```

## 🛠️ 3. Mode Sans GPU

Si vous n'avez pas de GPU, vous pouvez utiliser le mode sans GPU, grâce à l'image `esscraye/reiletai-api:dev`.

Lancez le docker-compose.dev pour ça :
```bash
docker compose -f docker-compose.dev.yml up -d
```
