# Traefik v3

- k get ingressroute (Note: use below command)

- https://github.com/traefik/traefik-helm-chart

- Install CRDS (Note: install below crds, if not worked navigate to this https://github.com/traefik/traefik-helm-chart see the section Install CRDS)
```bash
kubectl apply --server-side --force-conflicts -k https://github.com/traefik/traefik-helm-chart/traefik/crds/?ref=v27
```

- Traefik 3 helm Installation
```bash
helm -n traefik upgrade --install traefik --create-namespace traefik/traefik --version 28.0.0 --values=values.yaml --wait
```

```bash
k get ingressroute.traefik.io
```
