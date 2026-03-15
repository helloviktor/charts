# Helm Charts

This repository hosts [Helm](https://helm.sh) charts for a homelab Kubernetes cluster.

- **Packaged charts** (`.tgz` archives and the `index.yaml` repository index) are stored in the [`docs/`](./docs) directory, which is served via GitHub Pages as the Helm repository.
- **Chart sources** live in the [`charts/`](./charts) directory, one sub-directory per chart.

The charts currently available are:

| Chart | Description |
|-------|-------------|
| [cloudflared](./charts/cloudflared) | Helm chart for a cloudflared tunnel |
| [linkding](./charts/linkding) | Helm chart for Linkding |
| [miniflux](./charts/miniflux) | Helm chart for Miniflux |
| [postgres](./charts/postgres) | Helm chart for PostgreSQL |
| [whoami](./charts/whoami) | Helm chart for traefik/whoami |

## Using the charts

Add this repository to Helm and install a chart:

```bash
# Add the repo (only needed once)
helm repo add helloviktor https://helloviktor.github.io/charts

# Update the local index cache
helm repo update

# Search the available charts
helm search repo helloviktor

# Install a chart (example: whoami)
helm install whoami helloviktor/whoami --namespace default
```

To customize a chart, download its default values first and pass your overrides:

```bash
helm show values helloviktor/whoami > my-values.yaml
# Edit my-values.yaml as needed, then:
helm install whoami helloviktor/whoami -f my-values.yaml --namespace default
```

## Building charts

The following tools are required:

- [Helm](https://helm.sh/docs/intro/install/) v3+

### Package a chart

```bash
# From the repository root, package a specific chart into docs/
helm package charts/<chart-name> --destination docs/
```

### Update the repository index

After packaging one or more charts, regenerate the `index.yaml` so Helm clients can discover the new versions:

```bash
helm repo index docs/ --url https://helloviktor.github.io/charts
```

### All-in-one example

```bash
# Package every chart and refresh the index
for chart in charts/*/; do
  helm package "$chart" --destination docs/
done
helm repo index docs/ --url https://helloviktor.github.io/charts
```

Commit and push the updated `docs/` directory to publish the new chart versions.
