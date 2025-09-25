# Flask App CI/CD with GitHub Actions

## 📌 Overview
This repository demonstrates a **CI/CD pipeline** for a Python Flask application using **GitHub Actions**.  

The workflow runs on:
- **main branch** → CI checks (build, test).
- **staging branch** → Deploy to staging environment.
- **release tags** → Deploy to production environment.

---

## ⚙️ Workflow Stages
1. **Build & Test**
   - Runs on all pushes to `main` or `staging`.
   - Installs dependencies.
   - Runs `pytest` test suite.
   - Prepares app for deployment.

2. **Deploy to Staging**
   - Runs only on pushes to `staging`.
   - Deploys app to staging environment using secrets for authentication.

3. **Deploy to Production**
   - Runs only when a GitHub release/tag is created.
   - Deploys app to production environment.

---

## 🔑 GitHub Secrets
The workflow uses **GitHub Secrets** for sensitive data:
- `STAGING_SSH_KEY` → SSH key for staging server.
- `PROD_SSH_KEY` → SSH key for production server.
- Add secrets under: `Repo → Settings → Secrets and variables → Actions`.

---

## 🚀 Running Locally
To test app locally:
```bash
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
pytest
python flask_app.py
App runs at: http://127.0.0.1:5000

📸 Screenshots

Build & Test job success

Deploy to Staging job

Deploy to Production job
---