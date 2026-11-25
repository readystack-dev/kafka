# Provenance — Apache Kafka (`4.4.0-CE-ubuntu24.04-r7`)

Every item below is copied from a record in this archive; the record is named in brackets.

## Source

- Upstream repository: https://github.com/apache/kafka
- Revision built: `4.4.0-rc4` (commit `1156b2752aaa28eafc0b4c4d387e63356793268d`)
- Source tree: `b5da1e956699ffe902548159723a07726c779eccb63a74c376091efa1d0a83e7` over 7521 files [`docs/provenance/SOURCE_TREE_HASH.json`]
- Community Edition only: enterprise code is removed or refused before the build (CE audit at acquire).

## Build

- Method: `source-rebuild-java`; base image `eclipse-temurin:25-jre-noble`
- Compiled with `--network=none` from vendored source, dependencies and base images; BuildKit pinned to `moby/buildkit:v0.31.2` (shipped in `toolchain/`).
- SOURCE_DATE_EPOCH: `1795200585` [`SOURCE_DATE_EPOCH.txt`]
- Frozen inputs: [`docs/provenance/FREEZE_MANIFEST.json`], build recipe: [`docs/provenance/BUILD_RECIPE.json`].

## Output

- Published image: `readystack/kafka:4.4.0-CE-ubuntu24.04-r7` — index digest `sha256:009f36a681e857fee853d434fbe876152c8ef5fd1448a890e25c7169f375a81b` [`docs/provenance/LOCKED_DIGEST.txt`]
- linux/amd64 image digest `sha256:2a692a681e03e0f6455475ec53c4acd7aae08aebe7e4725cb2fc3c6af734764f` — reproduced from this archive before publishing [`docs/provenance/REPRO_VERIFICATION.json`].

## Attestations and signature

- SBOM + SLSA provenance attached to the image: attached: an SPDX SBOM and SLSA v1 provenance [`docs/provenance/SCOUT_VERDICT.json`]
- cosign signature by the ReadyStack release key: verified before publishing. Check it: `cosign verify --key https://readystack.dev/keys/cosign.pub readystack/kafka:4.4.0-CE-ubuntu24.04-r7`

## Pinned inputs, and why

- 14 pinned inputs, each with where it came from, why this one, how it was checked and when it was decided: `docs/PINS.md` [`docs/provenance/PINS.json`] (upstream source 2, base and build images 3, image digests 2, language runtimes and toolchains 1, dependency versions readystack sets 1, pins in the kit's dockerfiles 3, readystack's build engine 1, dependencies upstream chose 1).

## Build trail

- How this release passed through the ReadyStack harness, record by record (every chain, drive, stage, review round, defect and check, each naming the record it is copied from): `ReadyStack-kafka-4.4.0-CE-ubuntu24.04-r7.trail.json`, published beside this archive and signed with the release key (`ReadyStack-kafka-4.4.0-CE-ubuntu24.04-r7.trail.json.sigstore`), and readable at https://readystack.dev/products/kafka/trail/4.4.0-CE-ubuntu24.04-r7.

