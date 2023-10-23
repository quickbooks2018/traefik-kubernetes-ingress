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

- Kind MetalLb Installation
- https://github.com/metallb/metallb
```bash
kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/v0.13.12/config/manifests/metallb-native.yaml
```
  
- GKE Cloudflare Traefik Ingress
```bash
helm -n traefik upgrade --install traefik --create-namespace traefik/traefik --version 24.0.0 --values=gke-values.yaml --wait
```

- metallb-config.yaml
```bash
apiVersion: v1
kind: ConfigMap
metadata:
  namespace: metallb-system
  name: config
data:
  config: |
    address-pools:
    - name: default
      protocol: layer2
      addresses:
      - 172.18.0.200-172.18.0.250
```
```bash
kubectl apply -f metallb-config.yaml
```

- Access Traefik Dashboard url http://localhost:8080/dashboard/ (read only web gui) http://localhost:46443/dashboard/#/
