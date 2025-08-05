# 🧪 Medplum Local Docker Environment

This project provides a simple **Docker-based local development environment** for running a self-hosted instance of [Medplum](https://www.medplum.com/).

⚠️ **Warning**: This setup is intended **for development and testing purposes only**. It is **not suitable for production environments** as it uses default credentials, stores data on local volumes, and lacks security hardening (e.g., TLS, authentication secrets, backup, monitoring, etc.).

---

## 📦 What's Included

This `docker-compose.yml` starts the following services:

| Service             | Description                                      | Port   |
|---------------------|--------------------------------------------------|--------|
| `postgres`          | PostgreSQL 15 database                           | 5432   |
| `redis`             | Redis 7 cache                                    | 6379   |
| `medplum-server`    | Medplum FHIR API server                          | 8103   |
| `medplum-app` (opt) | Medplum frontend (optional, disabled by default) | 3000   |

---

## 🚀 Getting Started

### 1. Clone this repository

```bash
git clone https://github.com/your-org/medplum-local-docker.git
cd medplum-local-docker
```

### 2. Configure Medplum

Update the `medplum.config.json` file to suit your environment.

Refer to the official [Medplum configuration docs](https://www.medplum.com/docs/self-hosting/config-settings) for full details.

### 3. Start the environment

```bash
docker-compose up --build
```

> The first run may take a few minutes to pull images and build containers.

---

## 🌐 Accessing Medplum

- API Base URL: [http://localhost:8103](http://localhost:8103)
- Default Super Admin: `admin@example.com`
- Default Password: `admin`

If you enable the optional frontend service (`medplum-app`), access the UI at:

- Frontend URL: [http://localhost:3000](http://localhost:3000)

---

## 🛠️ Using Your Own Frontend

You can either:

- Use the optional `medplum-app` image provided (by uncommenting in `docker-compose.yml`), or
- Mount your own custom frontend in a folder such as `./app` and build it via Docker

Tip: Use [git submodules](https://git-scm.com/book/en/v2/Git-Tools-Submodules) or symbolic links to sync with your local frontend project.

---

## 🛑 Not for Production Use

This Docker setup is not suitable for production because:

- Uses default super admin credentials
- Lacks TLS/HTTPS
- No secrets management
- No backup or monitoring
- Not designed for horizontal scaling
- Exposes containers on local ports

For production-ready setup, refer to [Medplum's self-hosting guide](https://www.medplum.com/docs/self-hosting/overview).

---

## 🧼 Stopping & Cleaning Up

To stop services:

```bash
docker-compose down
```

To stop and remove all local volumes (e.g., database files):

```bash
docker-compose down -v
```

---

## 🧪 Tips

- Use tools like `curl` or [Postman](https://www.postman.com/) to test the FHIR API.
- All services share a custom Docker network (`medplum-net`), making it easier to add integrations.
- You can access the backend interface with `docker compose exec -it server /bin/bash`, the medplum cli is included on the image.

---

## 📄 License

This project is provided as-is for local development. Refer to Medplum’s license for production usage.
