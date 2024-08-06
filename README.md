# forecastle

Repository with instructions to install Forecastle on Kubernetes

> [!WARNING]
> This is a personal repository to help me to install Forecastle in my clusters.
> To get official information, visit the [Forecastle repository](https://github.com/stakater/Forecastle).

## Table of Contents

- [Install](#install)
  - [Kustomize](#kustomize)
  - [Helm](#helm)
- [My Personal Install with Flux](#my-personal-install-with-flux)

## Install

### Kustomize

Since kustomize is removed from kubectl binary in version 1.31, It is necessary
to use kustomize binary itself to send the YAML files to kubectl:

> [!NOTE]
> There is a route object in the kustomization file, and It is commented.

```bash
kustomize build github.com/mmmarceleza/forecastle//manifests | kubectl apply -f-
```

### Helm

> [!NOTE]
> Some configs were set to simplify the installation of forecastleapps custom
> resource objects. Check the [official repository](https://github.com/stakater/Forecastle) for more information.

```bash
helm upgrade --install forecastle forecastle \
-n forecastle --create-namespace \
--repo "https://stakater.github.io/stakater-charts" \
--version "v1.0.143" \
--set "forecastle.config.crdEnabled=true" \
--set "forecastle.config.namespaceSelector.any=true" \
--set "forecastle.config.namespaceSelector.matchNames=[]"
```

## My Personal Install with Flux

> [!NOTE]
> This is for my environmental using my local cluster with [Kind](https://github.com/mmmarceleza/kind).

```bash
kustomize build github.com/mmmarceleza/forecastle//flux | kubectl apply -f-
```
