
---

````markdown
# Blue-Green Deployment with Docker

This project demonstrates how to set up a **Blue-Green Deployment strategy** for a simple web application.  
It builds on top of the [Multi-Service Docker project](https://github.com/Harsha-nani75/Blue-green-deployment) and shows how to deploy applications **with zero downtime and zero data loss**.

---

## 📖 Project Overview

The **Blue-Green Deployment** strategy ensures that a new version of the application can be deployed **safely and seamlessly**:

- **Blue Environment** → Current running version of the application.  
- **Green Environment** → New version of the application running in parallel.  
- **Traffic Switch** → Users continue using the Blue version until Green is verified and healthy.  
  Once ready, traffic is switched to Green instantly.  
- If issues occur, you can **rollback** to Blue immediately.

---

## 🛠 Requirements

1. Use an existing application (e.g. from the [Multi-Container Service Project](https://roadmap.sh/projects/multiservice-docker)).
2. Run two versions of the app (`blue` and `green`) in **separate containers**.
3. Use a **reverse proxy (Nginx/Traefik)** to route traffic to either Blue or Green.
4. Deploy a new version without downtime by updating the proxy’s routing.

---

## ⚙️ Setup & Usage

### 1. Clone this repository
```bash
git clone https://github.com/your-username/blue-green-deployment.git
cd blue-green-deployment
````

### 2. Start both versions

```bash
docker compose up --build -d
```

* `web-blue` → serves the old version
* `web-green` → serves the new version (not live yet)

### 3. Configure the proxy

The **reverse proxy** (Nginx in this example) decides which version serves live traffic.
You can switch between **blue** and **green** by updating the proxy config and reloading it:

```bash
docker exec -it nginx-proxy nginx -s reload
```

### 4. Verify Deployment

* Access `http://localhost` → you’ll see the active version.
* Once Green is healthy, update the proxy to point traffic to Green.
* Roll back by switching back to Blue if issues occur.

---

## 🎯 Bonus Features

### ✅ CI/CD Pipeline

* Use **GitHub Actions / GitLab CI / Jenkins** to:

  * Build Docker images on `git push`.
  * Push to Docker Hub or your private registry.
  * Deploy automatically to the server with SSH or remote Docker.

### ✅ Monitoring & Health Checks

* Use **Prometheus + Grafana** or **cAdvisor** to monitor:

  * Container health and performance.
  * Deployment process and resource usage.
* Add Docker health checks in `docker-compose.yml` to ensure only healthy services receive traffic.

---

## 📚 References

* [Blue-Green Deployment Strategy](https://martinfowler.com/bliki/BlueGreenDeployment.html)
* [Docker Multi-Service Project](https://roadmap.sh/projects/multiservice-docker)
* [Nginx Reverse Proxy Guide](https://docs.nginx.com/nginx/admin-guide/web-server/reverse-proxy/)
* [GitHub Actions for Docker](https://docs.github.com/en/actions/publishing-packages/publishing-docker-images)

---

## 🏆 Outcome

By completing this project you will learn how to:

* Deploy containerized applications with **zero downtime**.
* Use a **reverse proxy** to control live traffic.
* Roll out and roll back changes **safely**.
* Automate deployments with **CI/CD**.
* Monitor applications in production.

```

---

