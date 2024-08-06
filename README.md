# forecastle

Repository with instructions to install Forecastle on Kubernetes

## Table of Contents

- [Install](#install)
  - [Kustomize](#kustomize)
  - [Helm](#helm)

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
