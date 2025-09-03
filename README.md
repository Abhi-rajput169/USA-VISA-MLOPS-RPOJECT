# MLOPs – Production-Ready Machine Learning Project (Visa Approval Prediction)

This repository demonstrates how to build an **end-to-end ML system** that loads and cleans data, trains models, monitors performance, and deploys to production using **Docker + AWS (ECR + EC2) + GitHub Actions**.  

---

## 🔗 Quick Links
- **Anaconda:** [Download](https://www.anaconda.com/)  
- **VS Code:** [Download](https://code.visualstudio.com/download)  
- **Git:** [Download](https://git-scm.com/)  
- **Flowchart Design Tool:** [Whimsical](https://whimsical.com/)  
- **Monitoring Tool:** [EvidentlyAI](https://www.evidentlyai.com/)  
- **MongoDB Atlas:** [Login](https://account.mongodb.com/account/login)  
- **Dataset (EasyVisa):** [Kaggle Link](https://www.kaggle.com/datasets/moro23/easyvisa-dataset)  

> **Dataset:** We are using the **EasyVisa dataset** from Kaggle. Download it and place it inside `data/raw/`.

---

## 🧭 Table of Contents
1. Project Goals  
2. Tech Stack  
3. Project Structure  
4. Workflow (Code Flow)  
5. Local Setup  
6. Get the Data  
7. Environment Variables  
8. Train & Run Locally  
9. Monitoring with EvidentlyAI  
10. Dockerization  
11. AWS CICD (GitHub Actions → ECR → EC2)  
12. Git Commands  
13. License  

---

## 🎯 Project Goals
- Build a machine learning pipeline for **Visa Approval Prediction**.  
- Follow **production-ready best practices**: modular code, configs, logging, exception handling.  
- Implement **data & model monitoring** using EvidentlyAI.  
- Automate **deployment with AWS (ECR + EC2) & GitHub Actions**.  

---

## 🛠 Tech Stack
- **Language:** Python 3.8  
- **ML/DS:** pandas, numpy, scikit-learn  
- **Monitoring:** EvidentlyAI  
- **Database:** MongoDB Atlas  
- **Packaging/Environment:** Conda, pip  
- **Containerization:** Docker  
- **Cloud:** AWS ECR (image registry), AWS EC2 (compute)  
- **CI/CD:** GitHub Actions  

---

## 📂 Project Structure
```
.
├── src/
│   ├── constants/           # Global constants
│   ├── entity/              # Config & artifact schemas
│   ├── components/          # Data ingestion, transformation, training, evaluation
│   ├── pipeline/            # Orchestration pipelines
│   ├── utils/               # Helpers: logging, IO, exceptions
│   └── app.py               # API/UI for predictions
├── configs/
│   └── config.yaml
├── data/
│   ├── raw/                 # Raw Kaggle data
│   ├── processed/           # Cleaned data
│   └── artifacts/           # Models, metrics
├── reports/                 # Evidently reports
├── Dockerfile
├── requirements.txt
├── .env.example
├── .github/workflows/deploy.yml
└── README.md
```

---

## 🔄 Workflow (Code Flow)
1. **constants/** → fixed values (paths, file names, seeds).  
2. **entity/** → configs and artifact schemas.  
3. **components/** →  
   - Data Ingestion  
   - Data Transformation  
   - Model Training  
   - Model Evaluation  
4. **pipeline/** → orchestrates the steps end-to-end.  
5. **app.py** → API or UI for inference.  

---

## 💻 Local Setup
```bash
# Create and activate Conda environment
conda create -n visa python=3.8 -y
conda activate visa

# Install dependencies
pip install -r requirements.txt
```

---

## 📊 Get the Data
**Option A (Manual):**  
1. Download dataset from [Kaggle EasyVisa](https://www.kaggle.com/datasets/moro23/easyvisa-dataset).  
2. Place it in `data/raw/`.  

**Option B (CLI):**
```bash
kaggle datasets download -d moro23/easyvisa-dataset -p data/raw --unzip
```

---

## ⚙️ Environment Variables
Set these before running:
```bash
export MONGODB_URL="mongodb+srv://<username>:<password>@<cluster-url>/<db>"
export AWS_ACCESS_KEY_ID=<your-key>
export AWS_SECRET_ACCESS_KEY=<your-secret>
export AWS_DEFAULT_REGION=us-east-1
```

---

## ▶️ Train & Run Locally
```bash
# Run pipeline
python main.py

# Run API
python src/app.py
```

---

## 📈 Monitoring with EvidentlyAI
- Use **EvidentlyAI** to track data drift and model quality.  
- Reports will be saved in `reports/`.  

---

## 🐳 Dockerization
```bash
# Build image
docker build -t visa-app .

# Run container
docker run -p 8080:8080 visa-app
```

---

## ☁️ AWS CICD (GitHub Actions → ECR → EC2)
1. Create an **IAM User** with:  
   - `AmazonEC2ContainerRegistryFullAccess`  
   - `AmazonEC2FullAccess`  
2. Create **ECR Repository** → save URI (e.g., `315865595366.dkr.ecr.us-east-1.amazonaws.com/visarepo`).  
3. Launch an **EC2 Instance (Ubuntu)**.  
4. Install Docker:  
   ```bash
   sudo apt-get update -y
   sudo apt-get upgrade -y
   curl -fsSL https://get.docker.com -o get-docker.sh
   sudo sh get-docker.sh
   sudo usermod -aG docker ubuntu
   newgrp docker
   ```
5. Configure EC2 as **GitHub self-hosted runner**.  
6. Add GitHub secrets:  
   - `AWS_ACCESS_KEY_ID`  
   - `AWS_SECRET_ACCESS_KEY`  
   - `AWS_DEFAULT_REGION`  
   - `ECR_REPO`  

---

## 🔑 Git Commands
```bash
git add .
git commit -m "Updated"
git push origin main
```

--