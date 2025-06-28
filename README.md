# Humanitec Score + Backstage Online Boutique Demo

This repository showcases how to run the popular **Online Boutique** microservices app using a full **Internal Developer Platform (IDP)** stack:

- 🧪 [Score](https://score.dev) to define portable workloads  
- 🛠️ [Humanitec Resource Definitions](https://docs.humanitec.com/integrations/resource-definitions/) for dynamic infrastructure  
- 🧑‍🚀 [Backstage](https://backstage.io) for developer self-service  
- 🧳 [PocketIDP](https://github.com/Humanitec-Dev/PocketIDP) for local platform emulation  

Built from a **Platform Engineer’s perspective**, this project enables consistent application delivery using **Golden Path templates**, automated provisioning, and GitOps-powered workflows.

---

## 🧰 Prerequisites

Ensure the following tools are available:

| Tool                         | Description                                                  |
|------------------------------|--------------------------------------------------------------|
| ✅ [PocketIDP]               | Runs Backstage, GitOps, and Humanitec Agent locally          |
| ✅ Humanitec Account         | Required to apply Resource Definitions & deploy workloads     |
| ✅ `score` CLI               | To define and validate app workloads                          |
| ✅ `score-k8s` / `score-compose` | Optional local deployment without Humanitec              |
| ✅ `humctl` CLI              | CLI to interact with the Humanitec Platform                   |

---

## 👷 Platform Engineer Workflow

The platform engineer sets up the system to support developer self-service using Score, Backstage, and Humanitec.

### 🔧 Step-by-Step:

1. **Apply Resource Definitions**

   Define infrastructure mappings (e.g., Pub/Sub, Redis, Ingress) in [`humanitec-resource-definitions/`](./humanitec-resource-definitions/).

   ```bash
   humctl apply -f humanitec-resource-definitions/

2. **Register Backstage Templates**

   Add templates from `backstage-templates/` to your Backstage catalog using either:

   * `catalog-info.yaml`
   * Direct Git registration (e.g., Gitea or GitHub)

3. **Start PocketIDP (Local IDP Environment)**

   Clone and run PocketIDP to spin up:

   * Backstage portal
   * Gitea (Git provider)
   * Humanitec Agent

   ```bash
   git clone https://github.com/Humanitec-Dev/PocketIDP
   cd PocketIDP
   ./run.sh
   ```

4. **Enable Golden Path Templates**

   Developers will now see Online Boutique service templates in the Backstage portal for self-service provisioning.

---

## 👨‍💻 Developer Workflow

After the platform is ready, developers can:

1. **Visit Backstage**

   Launch PocketIDP and access the Backstage portal.

2. **Create a Service from a Template**

   Choose a microservice from the Online Boutique Golden Path.

3. **Customize Configuration**

   Input parameters like name.

4. **Score Workload is Scaffolded and Pushed to Git**

   Generated workload spec (`score.yaml`) and app structure are pushed to Gitea (or GitHub, GitLab, etc.), by the setup humanitec pipleine.

5. **Deployment via Humanitec**

   Humanitec consumes the workload spec and associated resource mappings to:

   * Provision infra dynamically
   * Deploy the workload
   * Bind resources (e.g., DNS, databases, message queues)

---

## ⚙️ Local Deployment with Score Drivers

> 🧱 This demo builds upon the official [**Online Boutique CLI Tutorial**](https://github.com/Humanitec-DemoOrg/score-online-boutique), part of the [Humanitec-DemoOrg](https://github.com/Humanitec-DemoOrg) collection — which showcases how to deploy Score workloads using CLI tools like `score-compose`, `score-k8s`, and `humctl`.

To run services locally using the same Score spec and Humanitec drivers:

```bash
# Validate the Score workload
score validate -f score.yaml

# Run with Docker Compose
score-compose run -f score.yaml

# Run on local Kubernetes (e.g., kind, minikube)
score-k8s run -f score.yaml

# Deploy to Humanitec environment
humctl deploy \
  --app online-boutique \
  --env development \
  -f score.yaml \
  --message "Deploying Online Boutique via CLI"
```

The **official demo focuses on CLI-based deployment and dynamic infra provisioning**.

This repo extends that foundation by:

✅ Turning workloads into reusable **Backstage Golden Paths**
✅ Wiring the experience into a **self-service IDP portal**
✅ Running everything locally using **PocketIDP** for rapid iteration
✅ Giving developers a visual interface to scaffold, deploy, and manage services

> 🔁 You get the best of both worlds: the CLI power of the official tutorial and the seamless self-service UX of Backstage + Humanitec.

---

## 📁 Project Structure

```
.
├── score.yaml                         # Workload definition for Online Boutique
├── humanitec-resource-definitions/   # Infrastructure mappings
├── backstage-templates/              # Golden Path templates for each service
├── .github/workflows/ci.yaml         # CI pipeline for validating Score workloads
└── README.md                         # This file
```

---

## 📘 Related Reference Repos

* ✅ [Humanitec-DemoOrg/score-online-boutique](https://github.com/Humanitec-DemoOrg/score-online-boutique)
  Original CLI-based tutorial using Score, `score-k8s`, `score-compose`, and `humctl`.

---

## 🧠 Key Concepts

* **Workload Portability** with Score across Dev → Staging → Prod
* **Dynamic Provisioning** via Humanitec Resource Definitions
* **Golden Paths** that standardize service scaffolding
* **Self-Service Developer Experience** using Backstage
* **Local-first experimentation** via PocketIDP

---

## 🛡 Maintainers

This project is maintained by Platform Engineers passionate about enabling developer productivity with Humanitec and open standards.

---

## 📚 Resources

* [Score.dev](https://score.dev)
* [Humanitec Docs](https://docs.humanitec.com)
* [PocketIDP](https://github.com/Humanitec-Dev/PocketIDP)
* [Backstage](https://backstage.io)
* [Platform Engineering Slack](https://platformengineering.org/slack)


