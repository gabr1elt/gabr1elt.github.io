# docker

Docker

---

## Podman

```bash

# tests

podman run -it --rm alpine

## pod

podman pod create -h "gabr1elt.github.io" gabr1elt.github.io
# podman pod create -p 127.0.0.1:3000:3000 -h "gabr1elt.github.io" gabr1elt.github.io
podman pod rm gabr1elt.github.io

# generate

podman kube generate > "${HOME}/Development/gabr1elt.github.io/docker/kube.yml"

# build

podman kube play --build --context-dir "${HOME}/Development/gabr1elt.github.io" --replace "${HOME}/Development/gabr1elt.github.io/docker/kube.yml"

# run

podman kube play --replace "${HOME}/Development/gabr1elt.github.io/docker/kube.yml"
# podman kube play --replace --network=slirp4netns:--dns-forward "${HOME}/Development/gabr1elt.github.io/docker/kube.yml"

podman kube down "${HOME}/Development/gabr1elt.github.io/docker/kube.yml"

# attach

podman attach gabr1elt.github.io-vscode

```
