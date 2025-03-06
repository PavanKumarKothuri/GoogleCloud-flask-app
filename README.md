# **🚀 Deploy a Flask App on Google Cloud Run**  
 
---

🎯 **Goal:** Deploy a simple **Flask web app** on **Google Cloud Platform (GCP)** using **Cloud Run & Docker**.  

![GCP Cloud Run](https://upload.wikimedia.org/wikipedia/commons/thumb/a/a5/Google_Cloud_logo.svg/1200px-Google_Cloud_logo.svg.png)  

### **📌 What You’ll Learn**  
✅ How to deploy a **Flask app** on **Google Cloud Run**  
✅ How to use **Docker** to containerize applications  
✅ How to automate deployment using **Cloud Build**  
✅ How to work with **Google Cloud CLI**  

---

## **🛠 Tech Stack**  
🔹 **Python** (Flask)  
🔹 **Google Cloud Platform (GCP)**  
🔹 **Docker** (for containerization)  
🔹 **Cloud Run & Cloud Build**  
🔹 **gcloud CLI** (Terminal-based deployment)  

---

## **🚀 Step 1: Setup Google Cloud Project**  

Before deploying, **enable necessary services** on GCP:  

```sh
gcloud config set project your-project-id
gcloud services enable run.googleapis.com cloudbuild.googleapis.com
```

---

## **💻 Step 2: Setup Flask App**  

📁 Create a project folder:  

```sh
mkdir gcp-flask-app && cd gcp-flask-app
python3 -m venv venv
source venv/bin/activate  # (Mac/Linux)
```

🔹 Install Flask:  
```sh
pip install flask gunicorn
```

🔹 Create `app.py`:  

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def home():
    return "🚀 Flask App Deployed on Google Cloud Run!"

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=8080)
```

---

## **🐳 Step 3: Create a Dockerfile**  

🔹 Inside your project folder, create a `Dockerfile`:  

```dockerfile
# Use an official lightweight Python image
FROM python:3.9-slim

# Set working directory
WORKDIR /app

# Copy project files
COPY . /app

# Install dependencies
RUN pip install --no-cache-dir flask gunicorn

# Expose port
EXPOSE 8080

# Run the application
CMD ["gunicorn", "-b", "0.0.0.0:8080", "app:app"]
```

---

## **🛠 Step 4: Build & Push Docker Image**  

🔹 Authenticate with **Google Artifact Registry**:  

```sh
gcloud auth configure-docker
```

🔹 Build & Push Image to **Google Container Registry (GCR)**:  

```sh
docker build -t gcr.io/your-project-id/flask-app .
docker push gcr.io/your-project-id/flask-app
```

---

## **🚀 Step 5: Deploy on Google Cloud Run**  

🔹 Deploy the app on **Cloud Run**:  

```sh
gcloud run deploy flask-app \
  --image gcr.io/your-project-id/flask-app \
  --platform managed \
  --region us-central1 \
  --allow-unauthenticated
```

🔹 **Get the URL** and test in a browser:  

```sh
gcloud run services list
```

---

## **🧹 Step 6: Cleanup (Avoid Charges 💰)**  

After testing, **delete running services** to avoid charges:  

```sh
gcloud run services delete flask-app
gcloud container images delete gcr.io/your-project-id/flask-app
```

---

## **🎯 Key Takeaways**  
✔️ **Docker** helps package the app into a portable container  
✔️ **Cloud Run** deploys & manages the app without worrying about servers  
✔️ **gcloud CLI** automates the deployment  

---


## **💡 Want to Learn More?**  
📖 **Official Docs:**  
🔗 [Flask](https://flask.palletsprojects.com/)  
🔗 [Google Cloud Run](https://cloud.google.com/run/docs)  
🔗 [Docker](https://docs.docker.com/)  

---

## **🏆📫 Author**

- Built with ❤️ by PavanKumar Kothuri - Cloud Computing and Machine learning are fun!
- 🌐 [LinkedIn | https://www.linkedin.com/in/iamkpk/](https://www.linkedin.com/in/iamkpk/)
- 💻 [GitHub | https://github.com/PavanKumarKothuri](https://github.com/PavanKumarKothuri)  
- ✉️ [Email | pavankumarkothuri9@gmail.com](mailto:pavankumarkothuri9@gmail.com)

Feel free to connect with me for further discussions or contributions. 🌟 **Happy Coding!** 🚀

---
