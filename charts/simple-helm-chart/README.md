# Simple Helm chart

Installs:

- Deployment
- Service
- PersistentVolume (optional)
- PersistentVolumeClaim (optional)
- HTTPRoute (optional)

Note that for HTTPRoute, a `traefik-gateway` Gateway needs to be present and listening to the selected namespace.  Check with the following:
```bash
k get gateway traefik-gateway -n traefik -o yaml | yq '.spec'
```

Example output:
```yaml
gatewayClassName: traefik
listeners:
  - allowedRoutes:
      namespaces:
        from: All
    name: web
    port: 8000
    protocol: HTTP
```

Currently, only the `web` listener is supported, meaning all services installed with this chart will use HTTP instead of HTTPS.
