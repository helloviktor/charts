# Homelab Helm Charts

[![Lint and Test Charts](https://github.com/helloviktor/charts/actions/workflows/lint-test.yml/badge.svg)](https://github.com/helloviktor/charts/actions/workflows/lint-test.yml)
[![Release Charts](https://github.com/helloviktor/charts/actions/workflows/release.yml/badge.svg)](https://github.com/helloviktor/charts/actions/workflows/release.yml)

A collection of Helm charts for homelab deployments, hosted on GitHub Pages.

## Usage

```bash
helm repo add helloviktor https://helloviktor.github.io/charts
helm repo update
```

Install a chart:

```bash
helm install my-release helloviktor/my-app
```

## Charts

| Chart | Description | Version |
|-------|-------------|---------|
| [my-app](charts/my-app) | A generic application chart for homelab deployments | 0.1.0 |

## Development

### Prerequisites

- [Helm](https://helm.sh/docs/intro/install/) v3.x
- [helm/chart-testing](https://github.com/helm/chart-testing) (for linting)
- [kind](https://kind.sigs.k8s.io/) (for local testing)

### Lint and test charts locally

```bash
ct lint --config ct/ct.yaml
ct install --config ct/ct.yaml
```

## Publishing

Charts are automatically packaged and published to GitHub Pages when changes are merged to the `main` branch, using [helm/chart-releaser-action](https://github.com/helm/chart-releaser-action).

> **Note:** Before the first release, enable GitHub Pages on this repository:
> Go to **Settings → Pages**, set the source to **Deploy from a branch**, and select the `gh-pages` branch.

