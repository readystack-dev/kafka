# Apache Kafka 4.4.0 — ReadyStack release `4.4.0-CE-ubuntu24.04-r7`

Generated 2026-11-20 from this release's build records and strategy. Statements that come from a single record name it in brackets; the others come from this release's strategy and build log.

## Release

- **Image:** `readystack/kafka:4.4.0-CE-ubuntu24.04-r7` (linux/amd64). Index digest `sha256:009f36a681e857fee853d434fbe876152c8ef5fd1448a890e25c7169f375a81b` [`docs/provenance/LOCKED_DIGEST.txt`].
- **Image manifest digest:** `sha256:2a692a681e03e0f6455475ec53c4acd7aae08aebe7e4725cb2fc3c6af734764f` [`TARGET_DIGEST.txt`].
- **Upstream:** Apache Kafka 4.4.0 built from source at `4.4.0-rc4` of https://github.com/apache/kafka — upstream notes: https://github.com/apache/kafka/releases/tag/4.4.0-rc4 [`docs/provenance/BUILD_RECIPE.json`].
- **Base image:** `eclipse-temurin:25-jre-noble`; runtime user `kafka`.
- **Build:** `source-rebuild-java`, compiled offline with `--network=none`.
- **Supersedes:** ReadyStack release `4.4.0-CE-ubuntu24.04-r6`.

## What changed in this release

- Upstream version unchanged (4.4.0); ReadyStack rebuild.
- Apache Kafka 4.4.0 is unchanged from the release this supersedes (4.4.0-CE-ubuntu24.04-r6); this release rebuilds it. Changes: the image is rebuilt on the current eclipse-temurin:25-jre-noble image (sha256:f3dd0838e69b…), which its maintainers updated after 4.4.0-CE-ubuntu24.04-r6 was built on sha256:23481dc33a75…. Settings, ports and data volumes are those of 4.4.0-CE-ubuntu24.04-r6: replace the container with this image on the same volumes.

## Security status at release (measured 2026-11-20)

- **Docker Scout:** 0 fixable critical/high vulnerabilities; runs as `kafka` (non-root); SBOM + provenance attestations present (SPDX SBOM + SLSA v1) [`docs/provenance/SCOUT_VERDICT.json`].
- **OSV cross-check:** no fixable critical/high vulnerability beyond Docker Scout's findings.
- **Signature:** cosign signature verified by ReadyStack's release gate before publishing; check it yourself with `cosign verify --key https://readystack.dev/keys/cosign.pub readystack/kafka:4.4.0-CE-ubuntu24.04-r7` (signatures are recorded in the public Sigstore transparency log).
- **ReadyStack release check at release:** passed (ReadyStack's own test, not a Docker Scout grade). Vulnerabilities are disclosed every day and the image never changes, so it is re-checked daily, beside Docker Scout's own dated grade, at https://readystack.dev/queue.
- **Before exposing this service:** The PLAINTEXT listener on port 9092 has no authentication and no encryption (upstream's default): any client that can reach it can create, read, write and delete topics. Keep it on a private network, or configure SASL/SSL listeners with KAFKA_* variables.

## Reproducibility

Rebuilds offline from this archive to the identical image digest `sha256:2a692a681e03e0f6455475ec53c4acd7aae08aebe7e4725cb2fc3c6af734764f`: run `./BUILD_OFFLINE.sh`, then `./VERIFY_OFFLINE.sh` (add `--online` to confirm the Docker Hub tag holds the same digest). Before publishing, ReadyStack rebuilt the kit with `./BUILD_OFFLINE.sh` and compared the result with the published digest [`docs/provenance/REPRO_VERIFICATION.json`], then ran `./BUILD_OFFLINE.sh` and `./VERIFY_OFFLINE.sh` from this archive (without `--online`).

## Validation

- 12 of 12 use cases passed (12 authored) against the running image [`docs/validation/test-results.json`].

## Known issues

- **high** (upstream): Unauthenticated access by default [`RSD-kafka-62a525c8e6`]

## Defects fixed

- 4 problems found before release and fixed before it shipped (4 by review); each is listed in `docs/defects/defects.json`.

## Verify this archive

```
sha256sum -c CHECKSUMS.sha256
./BUILD_OFFLINE.sh && ./VERIFY_OFFLINE.sh --online
cosign verify --key https://readystack.dev/keys/cosign.pub readystack/kafka:4.4.0-CE-ubuntu24.04-r7
```

ReadyStack records every signature in the public Sigstore transparency log (Rekor), so the command needs no extra flags.

