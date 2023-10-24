# Helm Chart for Traefik Ingress Controller

- Terraform Eks Blue prints https://github.com/quickbooks2018/aws-eks-blueprints.git

```bash
helm repo ls
helm repo add traefik https://helm.traefik.io/traefik
helm repo update
helm search repo traefik
helm show values traefik/traefik
helm search repo traefik/traefik --versions
helm show chart traefik/traefik --version 24.0.0
helm show readme traefik/traefik --version 24.0.0
helm show values traefik/traefik --version 24.0.0
helm show all traefik/traefik --version 24.0.0
```

- Install Traefik Ingress Controller

```bash
helm -n traefik upgrade --install traefik --create-namespace traefik/traefik --version 24.0.0 --values=values.yaml --wait
```

- GKE Cloudflare Traefik Ingress
```bash
helm -n traefik upgrade --install traefik --create-namespace traefik/traefik --version 24.0.0 --values=gke-values.yaml --wait
```

- Access Traefik Dashboard url http://localhost:8080/dashboard/ (read only web gui) http://localhost:46443/dashboard/#/

- Kind MetalLb Installation
- https://github.com/metallb/metallb
```bash
kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/v0.13.12/config/manifests/metallb-native.yaml
```
- kubernetes api-resources
```bash
kubectl api-resources | grep metal
```
- Create IPPool.yaml
```bash
apiVersion: metallb.io/v1beta1
kind: IPAddressPool
metadata:
  name: first-pool
  namespace: metallb-system
spec:
  addresses:
  - 172.31.20.205/20
```
```bash
kubectl -n metallb-system apply -f pool-1.yml
```
- Create L2Advertisement.yaml
```bash
apiVersion: metallb.io/v1beta1
kind: L2Advertisement
metadata:
  name: homelab-l2
  namespace: metallb-system
spec:
  ipAddressPools:
  - first-pool
```
```bash
kubectl apply -f L2Advertisement.yaml
```
- Sample Deployment
```bash
apiVersion: v1
kind: Pod
metadata:
  name: nginx
  labels:
    app: nginx
spec:
  containers:
  - name: nginx
    image: nginx:1.14.2
    ports:
    - containerPort: 80
---
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  selector:
    app: nginx
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
  type: LoadBalancer
```
