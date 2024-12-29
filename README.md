# fly-compose
example compose.yaml
```yaml
version: '3.8'
fly_preffix_app: sun-oms
fly_organization: personal
fly_region: sin
services:
  web:
    build: .
    command: python manage.py runserver 0.0.0.0:8000
    resources:
      instance: 1
      kind: 'shared'
      limits:
        cpus: '1'
        memory: 512M
    volumes:
      - .:/app
    ports:
      - "8000:8000"
    depends_on:
      - db
  redis:
    image: redis:alpine
    ports:
      - "6379:6379"
  db:
    image: postgres:14
    volumes:
      - postgres_data:/var/lib/postgresql/data/pgdata
    environment:
      POSTGRES_USER: admin
      POSTGRES_PASSWORD: password
      POSTGRES_DB: django_db
      PGDATA: /var/lib/postgresql/data/pgdata
    ports:
      - "5432:5432"

```
1. create file compose.yaml or docker-compose.yaml
2. python fly-compose.py to deploy
