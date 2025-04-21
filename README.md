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

```yaml
# docker-compose.prod.yml
services:
  backend:
    image: esscraye/reiletai-api:latest
    container_name: reiletai-backend
    volumes:
      - app_data:/app/data
    ports:
      - "8123:8123"
    networks:
      - networkReilet
    restart: unless-stopped

  frontend:
    image: esscraye/reiletai-web:latest
    container_name: reiletai-frontend
    ports:
      - "3000:3000"
    depends_on:
      - backend
    networks:
      - networkReilet
    restart: unless-stopped

volumes:
  app_data:

networks:
  networkReilet:
    driver: bridge
```

Lancez :
```bash
docker compose -f docker-compose.prod.yml up -d
```