# Flask CI/CD Pipeline with GitHub Actions

## 📌 Project Overview
This project sets up a **CI/CD pipeline** for a simple Flask web application using **GitHub Actions**.  
The pipeline automates the following:
1. **Build** – Install dependencies and package the Flask app.
2. **Test** – Run unit tests with `pytest`.
3. **Deploy to Staging** – On pushes to the `staging` branch.
4. **Deploy to Production** – On publishing a GitHub Release.

---

## ⚙️ Prerequisites
Before running the workflow, ensure the following are ready:

- **GitHub Repository**
  - Contains your Flask application (`flask_app.py`).
  - Has a `requirements.txt` file.
  - Has a `test_flask_app.py` file for unit tests.
  - Two branches:  
    - `staging` → for testing deployments.  
    - `main` → stable production-ready code.

- **Two AWS EC2 instances**
  - **Staging EC2** (smaller instance, e.g., t2.micro).  
  - **Production EC2** (larger, e.g., t2.small or higher).  
  - Both must have:
    - Python 3 and `venv` installed.
    - Security group allowing SSH (port 22) and Flask app port (default: 5000).

- **GitHub Secrets (Repo → Settings → Secrets and variables → Actions)**
  - `STAGING_HOST` → Public IP/DNS of Staging EC2.
  - `PROD_HOST` → Public IP/DNS of Production EC2.
  - `EC2_USER` → Username for EC2 (`ubuntu` for Ubuntu AMI).
  - `SSH_KEY` → Private SSH key (corresponding to public key in EC2 `~/.ssh/authorized_keys`).

---

## 🏗️ Workflow File

The GitHub Actions workflow is located at:
.github/workflows/main.yml

markdown
Copy code

### Key Workflow Steps
1. **Checkout code**  
   Uses the official `actions/checkout@v3`.

2. **Set up Python**  
   Uses `actions/setup-python@v4`.

3. **Install dependencies & Run Tests**  
   Installs packages via pip and runs tests with `pytest`.

4. **Build**  
   Packages the app into a tarball for deployment.

5. **Deploy to Staging**  
   - Trigger: push to `staging` branch.  
   - Deploys app to **Staging EC2** using SSH.

6. **Deploy to Production**  
   - Trigger: publish a GitHub Release.  
   - Deploys app to **Production EC2** using SSH.

---

## 📬 Deployment Flow

- **Staging Deployment**
  - Trigger: `git push origin staging`
  - Workflow builds, tests, and deploys app to **Staging EC2**.

- **Production Deployment**
  - Trigger: Publish a **Release** in GitHub (`Releases → Draft new release → Publish`).
  - Workflow builds, tests, and deploys app to **Production EC2**.

---

## 📂 Repository Structure

├── flask_app.py # Main Flask application
├── requirements.txt # Python dependencies
├── test_flask_app.py # Unit tests (pytest)
├── .github/
│ └── workflows/
│ └── main.yml # GitHub Actions workflow
└── README.md # Project documentation

---

## 🚀 Running Locally (Optional)

You can test the app locally before pushing:
```bash
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
pytest
python flask_app.py
Visit: http://127.0.0.1:5000
```
## 📸 Screenshots

1.**Github Actions file**
 ![Image Alt](https://github.com/aviral31/Flask-App-with-Github-Actions/blob/0175f5b6b920384dc50d3089a26d5377a1660ae5/ss8.png)
 ![Image Alt](https://github.com/aviral31/Flask-App-with-Github-Actions/blob/0175f5b6b920384dc50d3089a26d5377a1660ae5/ss9.png)
 ![Image Alt](https://github.com/aviral31/Flask-App-with-Github-Actions/blob/0175f5b6b920384dc50d3089a26d5377a1660ae5/ss10.png)
 ![Image Alt](https://github.com/aviral31/Flask-App-with-Github-Actions/blob/0175f5b6b920384dc50d3089a26d5377a1660ae5/ss11.png)
 ![Image Alt](https://github.com/aviral31/Flask-App-with-Github-Actions/blob/0175f5b6b920384dc50d3089a26d5377a1660ae5/ss12.png)
 ![Image Alt](https://github.com/aviral31/Flask-App-with-Github-Actions/blob/0175f5b6b920384dc50d3089a26d5377a1660ae5/ss13.png)
2.**Workflow Overview (CI/CD pipeline)**
 ![Image Alt](https://github.com/aviral31/Flask-App-with-Github-Actions/blob/0175f5b6b920384dc50d3089a26d5377a1660ae5/ss1.png)
3.** Build & Test stage success **
 ![Image Alt](https://github.com/aviral31/Flask-App-with-Github-Actions/blob/0175f5b6b920384dc50d3089a26d5377a1660ae5/ss2.png)
4.**Deploy to Staging success**
 ![Image Alt](https://github.com/aviral31/Flask-App-with-Github-Actions/blob/0175f5b6b920384dc50d3089a26d5377a1660ae5/ss3.png)
 ![Image Alt](https://github.com/aviral31/Flask-App-with-Github-Actions/blob/0175f5b6b920384dc50d3089a26d5377a1660ae5/ss4.png)
5.**Deploy to Production success (on Release)**
![Image Alt](https://github.com/aviral31/Flask-App-with-Github-Actions/blob/0175f5b6b920384dc50d3089a26d5377a1660ae5/ss5.png)
![Image Alt](https://github.com/aviral31/Flask-App-with-Github-Actions/blob/0175f5b6b920384dc50d3089a26d5377a1660ae5/ss6.png)
![Image Alt](https://github.com/aviral31/Flask-App-with-Github-Actions/blob/0175f5b6b920384dc50d3089a26d5377a1660ae5/ss7.png)
6.**Flask App**
![Image Alt](https://github.com/aviral31/Flask-App-with-Github-Actions/blob/0175f5b6b920384dc50d3089a26d5377a1660ae5/ss14.png)
---
🎯 Conclusion
This project demonstrates how to implement a GitHub Actions CI/CD pipeline for a Flask application with:

Automated builds and tests.

Branch-based deployments (Staging vs Production).

Secure deployments to EC2 using GitHub Secrets.

The setup ensures reliable, automated deployments with minimal manual intervention.
---
