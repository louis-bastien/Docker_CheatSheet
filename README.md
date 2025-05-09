# 🐳 Docker CLI Cheatsheet

## 🧠 BASIC DOCKER COMMANDS

| Command                         | Purpose                                      |
|--------------------------------|----------------------------------------------|
| `docker build -t myapp .`      | Build image from Dockerfile                  |
| `docker run -it ubuntu bash`   | Start Ubuntu container interactively         |
| `docker run -it myapp`         | Run container from custom image              |
| `docker run -d myapp`          | Run container in background (detached)       |
| `docker ps` / `docker ps -a`   | List running / all containers                |
| `docker images`                | List Docker images                           |
| `docker logs <id>`             | View logs of container                       |
| `docker exec -it <id> bash`    | Open a shell inside container                |
| `docker stop <id>`             | Stop a running container                     |
| `docker rm <id>`               | Remove container                             |
| `docker rmi <id>`              | Remove image                                 |
| `docker system prune`          | Clean up unused containers/images/volumes    |

---

## 🧱 KEEP CONTAINER RUNNING

| Command                                              | What It Does                  |
|------------------------------------------------------|-------------------------------|
| `docker run -it ubuntu bash`                         | Stays alive while shell is open |
| `docker run -it ubuntu tail -f /dev/null`            | Keep alive forever (common)   |
| `docker run -it ubuntu sleep infinity`               | Sleep forever (if supported)  |
| `docker run -it ubuntu bash -c "while true; do sleep 1000; done"` | Manual infinite loop |

---

## 📦 VOLUMES

| Command                              | Purpose                              |
|--------------------------------------|--------------------------------------|
| `docker volume create myvol`         | Create a named volume                |
| `docker run -v myvol:/data myapp`    | Mount volume inside container        |
| `docker volume ls` / `inspect`       | List or inspect volumes              |
| `docker volume rm myvol`             | Remove a volume                      |
| `docker run -v $(pwd):/app myapp`    | Bind-mount current folder            |

---

## 🌐 NETWORKS

| Command                                 | Purpose                              |
|-----------------------------------------|--------------------------------------|
| `docker network create mynet`           | Create a custom network              |
| `docker run --network mynet ...`        | Attach container to network          |
| `docker network ls` / `inspect`         | List or inspect networks             |
| `docker network rm mynet`               | Remove unused network                |

🧠 Use container names to communicate inside a custom network (e.g., `ping db`).

---

## 🧪 DEBUGGING QUICK TIPS

| Problem               | What to Check                                      |
|-----------------------|----------------------------------------------------|
| Service unreachable   | `docker ps`, port mapping, try `curl localhost:<port>` |
| Container exits early | `docker logs <id>`                                 |
| Services can't connect| Check `--network`, use container names             |
| Volume not syncing    | Check paths, permissions                           |
| Image build fails     | Check `Dockerfile`, build context (`.`)            |
---

# 📦 Docker Compose Cheatsheet

## 🔧 COMMON COMMANDS

| Command                            | Purpose                                               |
|------------------------------------|-------------------------------------------------------|
| `docker-compose up`               | Start all services defined in the compose file        |
| `docker-compose up -d`            | Start services in detached mode (background)          |
| `docker-compose down`             | Stop and remove containers, networks, and volumes     |
| `docker-compose build`            | Build/rebuild services                                |
| `docker-compose stop`             | Stop running services                                 |
| `docker-compose start`            | Start previously stopped services                     |
| `docker-compose restart`          | Restart services                                      |

---

## 🐚 EXECUTION & LOGS

| Command                              | Purpose                                |
|--------------------------------------|----------------------------------------|
| `docker-compose ps`                 | List status of services                |
| `docker-compose logs`              | View combined logs from all services   |
| `docker-compose logs -f`           | Follow logs (live stream)              |
| `docker-compose exec <svc> bash`   | Open a shell in a running service      |
| `docker-compose run <svc> <cmd>`   | Run a one-off command in a service     |

---

## 🛠️ TIPS

- Compose automatically sets up a **network** so services can talk to each other by **service name** (e.g., `db`, `web`).
- Volumes and ports can be managed directly from the `docker-compose.yml` file.
- You can use `.env` files for configuration.

---

## 📁 FILES

| File Name              | Purpose                                 |
|------------------------|-----------------------------------------|
| `docker-compose.yml`   | Main configuration file for services    |
| `.env`                 | Optional environment variable override  |

---
