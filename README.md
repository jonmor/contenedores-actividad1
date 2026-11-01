# Actividad1

Para la practica se genero una app basica TODO API en 4 lenguajes, mismo contrato, misma base Postgres.

| Servicio | Imagen runtime                | Puerto host |
|----------|-------------------------------|-------------|
| python   | python:3.13-alpine            | 8081        |
| node     | node:22-alpine                | 8082        |
| java     | eclipse-temurin:21-jre-alpine | 8083        |
| php      | php:8.4-cli-alpine            | 8084        |
| db       | postgres:17-alpine            | 5432        |

## Contrato (igual en los 4)

- `GET /todos` → lista de todos (de **todos** los servicios; la columna `lang` dice quién lo creó)
- `POST /todos` con `{"title": "..."}` → 201 + el todo creado; 400 si falta `title`

## Levantar con docker compose

```bash
docker compose up --build -d
docker compose logs -f
```

## Detener con docker compose

```bash
docker compose down
```

## Probar

```bash
for p in 8081 8082 8083 8084; do
  curl -s -X POST localhost:$p/todos -H 'Content-Type: application/json' -d "{\"title\":\"tarea desde $p\"}"
  echo
done
curl -s localhost:8081/todos | jq
curl -s localhost:8082/todos | jq

```

## Notas

- `init.sql` solo se ejecuta cuando el volumen `pgdata` está vacío. para revisar si existe volumen `docker volume ls`
- Credenciales en claro en el compose: todo se usa con valor de "todo" en socker-compose.yml
- Para la practica se creo un repositorio publico: https://hub.docker.com/r/jonme25/unir-act1 
- **IMPORTANTE (Se debe eliminar despues de entrega y calificación de la practica)**
