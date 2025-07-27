```markdown
# 🌸 Iris API Deployment with Docker, Kubernetes & CML

This project demonstrates how to **package an ML model** (Iris classifier) using **FastAPI**, containerize it with **Docker**, deploy it to a **Kubernetes** cluster using **Minikube**, and automate deployment with **Continuous Machine Learning (CML)** via **GitHub Actions**.

---

## 📁 Project Structure

```

iris-api/
├── app/
│   ├── main.py              # FastAPI app for serving the model
│   ├── model.pkl            # Trained Iris model
│   └── requirements.txt     # Python dependencies
├── Dockerfile               # Docker image definition
├── k8s/
│   ├── deployment.yaml      # Kubernetes deployment manifest
│   └── service.yaml         # Kubernetes service manifest
├── .github/
│   └── workflows/
│       └── cml-deploy.yml   # CML GitHub Actions definition
└── README.md

````

---

## 🚀 Getting Started

### ✅ Prerequisites

Make sure the following tools are installed on your system:

- [Docker](https://docs.docker.com/get-docker/)
- [Minikube](https://minikube.sigs.k8s.io/docs/)
- [kubectl](https://kubernetes.io/docs/tasks/tools/)
- [Git](https://git-scm.com/)
- [DVC (Optional)](https://dvc.org/doc/install)

---

## 🐳 Run the API Locally with Docker

1. **Navigate to the project root:**
   ```bash
   cd iris-api
````

2. **Build the Docker image:**

   ```bash
   sudo docker build -t iris-api .
   ```

3. **Run the container:**

   ```bash
   sudo docker run -p 8080:8080 iris-api
   ```

4. **Access the API:**

   * Open in browser: [http://localhost:8080/docs](http://localhost:8080/docs)

---

## ☸️ Deploy on Kubernetes (via Minikube)

1. **Start Minikube:**

   ```bash
   minikube start
   ```

2. **Apply Kubernetes manifests:**

   ```bash
   kubectl apply -f k8s/
   ```

3. **Access the API service:**

   ```bash
   minikube service iris-api-service
   ```

> This opens the service in your default browser using Minikube's tunnel.

---

## 🔄 Continuous Deployment with CML

The GitHub Actions workflow under `.github/workflows/cml-deploy.yml` automates deployment steps such as:

* Model testing and reporting
* Deployment pipeline execution
* Posting metrics or status to pull requests (using CML)

### GitHub Actions Example (CML):

```yaml
name: CML Deploy

on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: iterative/setup-cml@v1
      - name: Docker Build
        run: docker build -t iris-api .
      - name: Deploy to Kubernetes
        run: kubectl apply -f k8s/
```

> You can customize this workflow based on your cluster and security requirements.

---

## 🧪 API Example

* **GET /ping**

  ```bash
  curl http://localhost:8080/ping
  ```

* **POST /predict**

  ```bash
  curl -X POST http://localhost:8080/predict \
       -H "Content-Type: application/json" \
       -d '{"sepal_length": 5.1, "sepal_width": 3.5, "petal_length": 1.4, "petal_width": 0.2}'
  ```

---

## 📦 Dependencies

Install Python dependencies using:

```bash
pip install -r app/requirements.txt
```

---

## 📌 Notes

* Make sure your user has access to Docker (`sudo usermod -aG docker $USER && newgrp docker`)
* Ensure Kubernetes context is active before running `kubectl apply`

---

## 📄 License

This project is licensed under the [MIT License](LICENSE).

---

## 🙌 Acknowledgments

* [FastAPI](https://fastapi.tiangolo.com/)
* [Docker](https://www.docker.com/)
* [Kubernetes](https://kubernetes.io/)
* [CML by Iterative](https://cml.dev/)
* [Minikube](https://minikube.sigs.k8s.io/docs/)

---

```

---

Let me know if you’d like to:
- Add a badge for GitHub Actions CI/CD.
- Include screenshots of the Swagger UI or Minikube deployment.
- Explain the model training or DVC pipeline.

I can help tailor the README even further depending on your goals (e.g., for a portfolio, assignment, or production use).
```
