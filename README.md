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

- Access Traefik Dashboard url http://localhost:8080/dashboard/ (read only web gui) http://localhost:46443/dashboard/#/
