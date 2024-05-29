# Traefik v3

- k get ingressroute (Note: use below command)

- Traefik 3 helm Installation
```bash
helm -n traefik upgrade --install traefik --create-namespace traefik/traefik --version 28.0.0 --values=values.yaml --wait
```

```bash
k get ingressroute.traefik.io
```