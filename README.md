[![ReadyStack](https://readystack.dev/logo.svg)](https://readystack.dev)

**Stable, Open-source Releases, Automated** · [readystack.dev](https://readystack.dev)

[![Docker Hub](https://img.shields.io/badge/Docker%20Hub-readystack%2Fkafka-2496ED?logo=docker&logoColor=white)](https://hub.docker.com/r/readystack/kafka) [![Docker pulls](https://img.shields.io/docker/pulls/readystack/kafka)](https://hub.docker.com/r/readystack/kafka) [![Grade at release](https://img.shields.io/badge/grade%20at%20release-A%20%2894%25%29-2ea44f)](https://readystack.dev/products/kafka) [![Signed: cosign](https://img.shields.io/badge/signed-cosign-2ea44f)](https://readystack.dev/keys/cosign.pub) ![SBOM: SPDX](https://img.shields.io/badge/SBOM-SPDX-2ea44f) ![Provenance: SLSA v1](https://img.shields.io/badge/provenance-SLSA%20v1-2ea44f) ![Offline rebuild: verified](https://img.shields.io/badge/offline%20rebuild-verified-2ea44f)

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

`recipe/` holds the kit's recipe files (Dockerfiles, build scripts, pins) as published at https://readystack.dev/products/kafka/recipe. The complete kit is the release download. Each release is a tag here. How to report a vulnerability: [SECURITY.md](SECURITY.md).

## About ReadyStack

**Stable, Open-source Releases, Automated.** ReadyStack releases popular open-source apps every week with every available critical and high security fix applied, plus full documentation, reference data, tests and a build recipe that recreates each release bit-for-bit. Each release is rebuilt from its pinned inputs with the network off, checked against its published digest, signed, and scanned and graded again every day. The images and build kits are free, and ReadyStack is soon to be a nonprofit.

[readystack.dev](https://readystack.dev) · [All products](https://readystack.dev/products.html) · [Build kits on GitHub](https://github.com/readystack-dev) · [Defect log](https://readystack.dev/defects.html) · contact@readystack.dev

— ReadyStack · https://readystack.dev
