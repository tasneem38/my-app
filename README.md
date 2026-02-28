# 📘 PROJECT DOCUMENTATION: Automated Docker Build & Push Workflow using GitHub Actions

## 1️⃣ Abstract
In modern software development, containerization has become essential for ensuring application portability and consistency across environments. However, manual Docker image builds and deployments often lead to inconsistencies, version mismatches, and human errors.

This project implements an automated CI/CD pipeline using GitHub Actions that automatically builds and pushes Docker images to Docker Hub whenever code is committed to the repository. The system eliminates manual intervention, improves reliability, and ensures consistent image generation.

## 2️⃣ Problem Statement
Manual Docker image builds and pushes create several issues:
- Inconsistent image versions
- Human errors during tagging
- Delayed deployment cycles
- Lack of automation
- Environment mismatch issues

There is a need for an automated workflow that ensures every code update results in a consistent and reproducible Docker image build and deployment.

## 3️⃣ Objective
The main objectives of this project are:
- To automate Docker image building
- To automate Docker image pushing to Docker Hub
- To implement CI/CD using GitHub Actions
- To eliminate manual Docker build inconsistencies
- To demonstrate real-world DevOps practices

## 4️⃣ Tools & Technologies Used
| Tool | Purpose |
| :--- | :--- |
| Docker | Containerization |
| Docker Hub | Image Registry |
| GitHub | Version Control |
| GitHub Actions | CI/CD Automation |
| Python (Flask) | Sample Application |

## 5️⃣ System Architecture
**Workflow:**
Developer → GitHub → GitHub Actions → Docker Build → Docker Hub

**Explanation:**
1. Developer pushes code to GitHub.
2. GitHub Actions detects the push.
3. Workflow logs into Docker Hub securely.
4. Docker image is built automatically.
5. Image is pushed to Docker Hub.
6. Image is available for deployment anywhere.

## 6️⃣ Project Structure
```text
my-app/
│
├── app.py
├── requirements.txt
├── Dockerfile
└── .github/
    └── workflows/
        └── docker.yaml
```

## 7️⃣ Application Code (Python Flask)
`app.py`
```python
from flask import Flask

app = Flask(__name__)

@app.get("/")
def home():
    return "Docker CI/CD with Python Flask 🚀"

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000)
```

## 8️⃣ Requirements File
`requirements.txt`
```text
Flask==3.0.3
```

## 9️⃣ Dockerfile
```dockerfile
FROM python:3.11-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

EXPOSE 5000

CMD ["python", "app.py"]
```

## 🔟 GitHub Actions Workflow
**Location:** `.github/workflows/docker.yaml`

```yaml
name: Docker Build and Push

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Code
        uses: actions/checkout@v3

      - name: Login to Docker Hub
        uses: docker/login-action@v2
        with:
          username: ${{ secrets.DOCKER_USERNAME }}
          password: ${{ secrets.DOCKER_PASSWORD }}

      - name: Build and Push Docker Image
        uses: docker/build-push-action@v4
        with:
          context: .
          push: true
          tags: tasneembanu29/my-app:latest
```

## 1️⃣1️⃣ Implementation Steps
- **Step 1: Create Python Flask Application** - Developed a simple Flask application.
- **Step 2: Create Dockerfile** - Defined container instructions for building the application image.
- **Step 3: Test Locally** - Used:
  ```bash
  docker build -t tasneembanu29/my-app:latest .
  docker run -p 5000:5000 tasneembanu29/my-app
  ```
- **Step 4: Create Docker Hub Repository** - Created repository on Docker Hub.
- **Step 5: Add GitHub Secrets** - Added `DOCKER_USERNAME` and `DOCKER_PASSWORD` (Access Token).
- **Step 6: Create GitHub Actions Workflow** - Defined automated build and push pipeline.
- **Step 7: Push Code** - GitHub automatically triggered workflow.

## 1️⃣2️⃣ Expected Outcome
- Automated Docker image build on every push
- Automated push to Docker Hub
- Elimination of manual Docker operations
- Consistent and reproducible builds

## 1️⃣3️⃣ Results
After successful execution:
- GitHub Actions workflow executed successfully
- Docker image built automatically
- Image pushed to Docker Hub
- CI/CD pipeline fully functional

## 1️⃣4️⃣ Advantages
- Reduces human errors
- Improves consistency
- Faster deployment cycles
- Real-world DevOps implementation
- Scalable solution

## 1️⃣5️⃣ Limitations
- Requires internet connectivity
- Depends on GitHub availability
- Basic pipeline (can be extended with testing & security scanning)

## 1️⃣6️⃣ Future Enhancements
- Add version tagging (v1.0, v1.1)
- Add Docker image vulnerability scanning (Trivy)
- Add Kubernetes auto deployment
- Add multi-environment support
- Add Slack notifications

## 1️⃣7️⃣ Conclusion
This project successfully demonstrates how manual Docker builds can be replaced with an automated CI/CD workflow using GitHub Actions. The system ensures consistent image builds, improves deployment efficiency, and aligns with modern DevOps practices used in the industry.
