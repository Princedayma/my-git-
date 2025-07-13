# 🚀 DockerHub Push Assignment – Flask App
**Date:** 2025-06-22

## 🐳 Objective
Build a Flask web app image and push it to DockerHub.

---

## ✅ Step 1: Create and Build Flask App

```bash
mkdir flask-docker-app && cd flask-docker-app
```

### Create `app.py`
```python
from flask import Flask
app = Flask(__name__)

@app.route("/")
def hello():
    return "Hello from Docker!"

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000)
```

### Create `requirements.txt`
```txt
flask
```

### Create `Dockerfile`
```Dockerfile
FROM python:3.9-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .
EXPOSE 5000
CMD ["python", "app.py"]
```

### Build Docker Image
```bash
docker build -t flask-app .
```

---

## ✅ Step 2: Push to DockerHub

### Login
```bash
docker login
```

### Tag the Image
```bash
docker tag flask-app <your-dockerhub-username>/flask-app:v1
```

### Push to DockerHub
```bash
docker push <your-dockerhub-username>/flask-app:v1
```

### Pull From DockerHub (Test)
```bash
docker pull <your-dockerhub-username>/flask-app:v1
```

---

## ✅ Step 3: Run the Container

```bash
docker run -d -p 5000:5000 --name flask-container flask-app
```

Visit `http://<your-vm-ip>:5000` to test.
