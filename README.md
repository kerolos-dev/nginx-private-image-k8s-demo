# NGINX Private Image with Kubernetes Deployment

🎯 Simple project showing how to:
- Build a custom Docker image
- Push it to a **private Docker Hub repository**
- Deploy it to Kubernetes using a **Deployment**
- Mount imagePullSecrets to access private images
- Expose via a **NodePort Service**

---

## 📁 Folder Structure

- `Dockerfile` – Custom image with static HTML
- `deployment.yaml` – Kubernetes Deployment using private image
- `service.yaml` – NodePort service to access from outside
- `secret.yaml` – Docker Hub credentials as a K8s Secret

---

## 🚀 How to Run

```bash
# 1. Build the image
docker build -t youruser/my-nginx:v1 .

# 2. Push it to Docker Hub (make it private!)
docker push youruser/my-nginx:v1

# 3. Create secret to pull from private registry
kubectl create secret docker-registry regcred \
  --docker-username=youruser \
  --docker-password=yourpass \
  --docker-email=youremail@example.com

# 4. Deploy app
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml

# 5. Access
minikube service nginx-service
