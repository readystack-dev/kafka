# Apache Kafka: ReadyStack build kit

The offline build kit for the Docker image `readystack/kafka:4.4.0-CE-ubuntu24.04-r7`. It holds what the image is built from (upstream source, base images, toolchain, pinned dependencies) and the documents, so the image can be rebuilt with no network access (`docker build --network=none`).

- Release: [4.4.0-CE-ubuntu24.04-r7](https://github.com/readystack-dev/kafka/releases/tag/4.4.0-CE-ubuntu24.04-r7)
- Image: [`docker.io/readystack/kafka:4.4.0-CE-ubuntu24.04-r7`](https://hub.docker.com/r/readystack/kafka/tags), manifest digest `sha256:2a692a681e03e0f6455475ec53c4acd7aae08aebe7e4725cb2fc3c6af734764f`
- Product page: https://readystack.dev/products/kafka
- Defects: this repository's Issues (defects recorded from 25 November 2026 on) and https://readystack.dev/defects.html?product=kafka

Apache Kafka is distributed under its upstream licence (Apache-2.0); the kit contains upstream's source under that licence, and each vendored component under its own.

## Download

From the [4.4.0-CE-ubuntu24.04-r7 release](https://github.com/readystack-dev/kafka/releases/tag/4.4.0-CE-ubuntu24.04-r7): `ReadyStack-kafka-4.4.0-CE-ubuntu24.04-r7.tar.gz` (939.0 MB), SHA-256 `4de45096836eed541d8adbe2f7b1257583262aa88cebce1d5773eb02f06a661a`.

```sh
sha256sum --check --ignore-missing SHA256SUMS
```

## Verify and rebuild

The rebuild statement is signed with the ReadyStack release key. Check the signature before you rely on it:

```sh
cosign verify-blob --key https://readystack.dev/keys/cosign.pub \
  --bundle ReadyStack-kafka-4.4.0-CE-ubuntu24.04-r7.rebuild.json.sigstore ReadyStack-kafka-4.4.0-CE-ubuntu24.04-r7.rebuild.json
```

Unpack with `-p` so file modes are kept, then follow the kit's own README.md and docs/REBUILD.md:

```sh
tar -xpzf ReadyStack-kafka-4.4.0-CE-ubuntu24.04-r7.tar.gz
cd 4.4.0-CE-ubuntu24.04-r7
less README.md docs/REBUILD.md
```

The build trail (`ReadyStack-kafka-4.4.0-CE-ubuntu24.04-r7.trail.json`, signed the same way, and its Markdown copy) records how this release was built and checked.

## This repository

`recipe/` holds the kit's recipe files (Dockerfiles, build scripts, pins) as published at https://readystack.dev/products/kafka/recipe. The complete kit is the release download. Each release is a tag here.
