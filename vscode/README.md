# docker

Docker

---

## Podman

```bash

# build

podman build --target="cpu" -t gabr1elt/gabr1elt.github.io/vscode:cpu -f "${HOME}/Development/gabr1elt.github.io/vscode/Dockerfile" "${HOME}/Development/gabr1elt.github.io/"

# run

podman run -it --rm -v "${HOME}/Development/gabr1elt.github.io:/root/Development:cached" -h "vscode" gabr1elt/gabr1elt.github.io/vscode:cpu
# podman run -it --rm -v "${HOME}/Development/gabr1elt.github.io:/root/Development:cached" -p 127.0.0.1:3000:3000 -h "vscode" gabr1elt/gabr1elt.github.io/vscode:cpu

# pod

podman run -it --rm --pod gabr1elt.github.io -v "${HOME}/Development/gabr1elt.github.io:/root/Development:cached" gabr1elt/gabr1elt.github.io/vscode

```
