# gabr1elt.github.io

Gabriel Torcat (Web Site) development

--------

## Podman

``` bash

podman build -f docker/Dockerfile -t gabr1elt/gabr1elt.github.io-dev

podman run --rm -v "${HOME}/Development/gabr1elt.github.io:/root/Development:cached" -p 127.0.0.1:3000:3000 -it -h "gabr1elt.github.io-dev" gabr1elt/gabr1elt.github.io-dev
podman run --rm -v "${HOME}/Development/gabr1elt.github.io:/root/Development:cached" -p 127.0.0.1:3000:3000 -it -h "drmbth-training-dev" gabr1elt/gabr1elt.github.io-dev /bin/bash

```
