# Apache Kafka: ReadyStack build kit

The offline build kit for the Docker image `readystack/kafka:4.4.0-CE-ubuntu24.04-r7`. It holds what the image is built from (upstream source, base images, toolchain, pinned dependencies) and the documents, so the image can be rebuilt with no network access (`docker build --network=none`).

- Release: [4.4.0-CE-ubuntu24.04-r7](https://github.com/readystack-dev/kafka/releases/tag/4.4.0-CE-ubuntu24.04-r7)
- Image: [`docker.io/readystack/kafka:4.4.0-CE-ubuntu24.04-r7`](https://hub.docker.com/r/readystack/kafka/tags), manifest digest `sha256:2a692a681e03e0f6455475ec53c4acd7aae08aebe7e4725cb2fc3c6af734764f`
- Product page: https://readystack.dev/products/kafka
- Source and build recipe: https://readystack.dev/products/kafka/recipe
- Build trail: https://readystack.dev/products/kafka/trail/4.4.0-CE-ubuntu24.04-r7
- Defects: this repository's Issues (defects recorded from 25 November 2026 on) and https://readystack.dev/defects.html?product=kafka

## The image

A single container running one Kafka node in KRaft combined mode (it is both broker and controller; Kafka 4 has no ZooKeeper) as the non-root kafka user, on the Eclipse Temurin 25 JRE. Topic data is log segments under /var/lib/kafka/data. There is no web UI, no REST API and no SQL database; clients use the Kafka protocol on port 9092, and the Kafka command-line tools are in the image under /opt/kafka/bin (on PATH).

## Who uses Apache Kafka and why

Engineering teams who move streams of events between systems in real time, for data pipelines, analytics and event-driven applications.

Kafka is a distributed event streaming platform. Applications publish streams of events, Kafka stores them durably, and other applications read and process them in real time or later.

A typical use: An online retailer records every order, payment and shipment as an event. Kafka stores those streams, and the warehouse system, the fraud checks and the analytics database each read them at their own pace, instead of every system calling every other system directly.

From the upstream project's own description: https://github.com/apache/kafka, https://kafka.apache.org/intro.

## This release

- Docker Scout policy grade at release: **A** (94%), graded 2026-11-20 with `docker scout policy` (CLI 1.26.0, docker-default configuration).
  - Docker Scout counts 91 packages with copyleft licences (GPL, LGPL, MPL), all of them operating-system packages (it counts only packages whose licence it can read; the SBOM lists every component).
- Signed with ReadyStack's release key (fingerprint `04daa92344a52dbc`): https://readystack.dev/keys/cosign.pub.
- Runs as a non-root user (`kafka`).
- Attestations on the image: an SPDX SBOM and SLSA provenance v1.
- Rebuilt from this kit with network egress blocked on 2026-11-20; the rebuilt image digest is the published one.
- Base: Ubuntu 24.04.

The current grade, measured again every day, is on https://readystack.dev/products/kafka.

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

— ReadyStack · https://readystack.dev
