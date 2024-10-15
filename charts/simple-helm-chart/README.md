# Simple Helm chart

This chart packages a Docker container into a Kubernetes deployment, with the following resources:

- `Deployment`
- `Service`
- `PersistentVolume` (optional)
- `PersistentVolumeClaim` (optional)
- `HTTPRoute` (optional)

## Prerequisite: Traefik

> [!NOTE]
> Creation of an `HTTPRoute` can be skipped by omitting the `traefik` section in `values.yaml`.

Note that to create an `HTTPRoute`, a `traefik-gateway` Gateway needs to be present and listening to the selected namespace. See [here](https://github.com/yinchi-k8s-test/microk8s/tree/main/traefik) for installation instructions (for a Microk8s cluster).

## Adding the repo to Helm

```bash
helm repo add simple-helm-chart https://yinchi-k8s-test.github.io/simple-helm-chart/
helm repo update
```

## Installing the chart

Create a `values.yaml` file to override the chart's default values. Then:
```bash
helm install test simple-helm-chart/simple-helm-chart -f values.yaml
```

> [!NOTE]
> You can see the chart's default values using `helm show values simple-helm-chart/simple-helm-chart`.

## Install the chart as a subchart

You can invoke this chart as a subchart in another Helm chart by adding it to the `dependencies` section in your `Chart.yaml`. This can be useful for adding additional Kubernetes resources to your chart, such as ConfigMaps and Secrets.  Use `helm dependencies update` to keep your chart dependencies synced.

See the official documentation for Helm dependencies [here](https://helm.sh/docs/topics/charts/#chart-dependencies).
