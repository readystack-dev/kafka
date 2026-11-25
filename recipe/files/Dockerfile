# GENERATED L-009 hermetic Java build (--network=none, SBOM+SLSA-attestation-producing).
# Pinned bases; vendored source + gradle cache(s) + toolchain/runtime debs from Dockerfile.vendor.
FROM eclipse-temurin:25-jdk-noble@sha256:589ff4cc3f71aab462e7048a47a0d10edf57fbccde3fceea2281e610bf5880b4 AS jbuild
# dpkg-install the vendored build toolchain (git/unzip) — no apt, fully offline.
RUN --mount=type=bind,source=vendored/build-debs,target=/tmp/bdebs \
    set --; for f in /tmp/bdebs/*.deb; do [ -e "$f" ] && set -- "$@" "$f"; done; \
    for pass in 1 2 3 4 5; do [ $# -eq 0 ] || dpkg -i --skip-same-version "$@" >/dev/null 2>&1 && break; done; \
    dpkg --configure -a && bad= && for d in "$@"; do p=$(dpkg-deb -f "$d" Package) v=$(dpkg-deb -f "$d" Version); \
      case "$(dpkg-query -W -f='${Version} ${db:Status-Abbrev}' "$p" 2>/dev/null)" in "$v ii"*) ;; *) bad="$bad $p=$v" ;; esac; done && \
    { [ -z "$bad" ] || { echo "vendored debs not installed at their vendored version:$bad" >&2; false; }; }
WORKDIR /src
COPY vendored/kafka-src/ .
COPY vendored/caches/gradle-home/ /gradle-home/
ENV GRADLE_USER_HOME="/gradle-home"
ENV GRADLE_OPTS="-Dorg.gradle.daemon=false"
RUN GH="${GRADLE_USER_HOME:-/gradle-home}"; rm -rf "$GH"/caches/*/transforms "$GH"/caches/*/transforms-* "$GH"/caches/*/groovy-dsl "$GH"/caches/*/kotlin-dsl "$GH"/caches/*/generated-gradle-jars "$GH"/caches/*/dependencies-accessors "$GH"/caches/jars-* "$GH"/caches/build-cache-* 2>/dev/null; true
RUN mkdir -p "${GRADLE_USER_HOME:-/root/.gradle}/init.d" && printf '%s\n' 'allprojects { configurations.all { resolutionStrategy { force("at.yawk.lz4:lz4-java:1.11.4"); force("org.xerial.snappy:snappy-java:1.1.10.9") } } }' > "${GRADLE_USER_HOME:-/root/.gradle}/init.d/kitforge-cve-forces.gradle" && cat "${GRADLE_USER_HOME:-/root/.gradle}/init.d/kitforge-cve-forces.gradle"
RUN cd /src && ./gradlew --no-daemon --offline --console=plain -PcommitId=1156b2752aaa28eafc0b4c4d387e63356793268d releaseTarGz
RUN mkdir -p /opt/kafka && tar -xzf /src/core/build/distributions/kafka_2.13-4.4.0.tgz -C /opt/kafka --strip-components=1 && rm -rf /opt/kafka/site-docs
RUN mkdir -p /opt/kafka/readystack-docker && cp /src/docker/resources/common-scripts/bash-config /src/docker/resources/common-scripts/configure /src/docker/resources/common-scripts/configureDefaults /src/docker/resources/common-scripts/run /src/docker/jvm/launch /opt/kafka/readystack-docker/ && sed -i '/SharedArchiveFile/d' /opt/kafka/readystack-docker/launch && ! grep -q SharedArchiveFile /opt/kafka/readystack-docker/launch
FROM eclipse-temurin:25-jre-noble@sha256:f3dd0838e69b881cc382237d5901e74ae3705b1056ad964b2e0e523b174fef99
ENV DEBIAN_FRONTEND=noninteractive PATH=/opt/kafka/bin:/opt/java/openjdk/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
RUN --mount=type=bind,source=vendored/debs,target=/tmp/debs \
    set --; for f in /tmp/debs/*.deb; do [ -e "$f" ] && set -- "$@" "$f"; done; \
    for pass in 1 2 3 4 5; do [ $# -eq 0 ] || dpkg -i --skip-same-version "$@" >/dev/null 2>&1 && break; done; \
    dpkg --configure -a && bad= && for d in "$@"; do p=$(dpkg-deb -f "$d" Package) v=$(dpkg-deb -f "$d" Version); \
      case "$(dpkg-query -W -f='${Version} ${db:Status-Abbrev}' "$p" 2>/dev/null)" in "$v ii"*) ;; *) bad="$bad $p=$v" ;; esac; done && \
    { [ -z "$bad" ] || { echo "vendored debs not installed at their vendored version:$bad" >&2; false; }; } && \
    rm -rf /var/lib/apt/lists/* \
           /var/log/dpkg.log /var/log/alternatives.log /var/log/apt /var/cache/ldconfig/aux-cache /var/cache/fontconfig
ARG SOURCE_DATE_EPOCH=1795200585
RUN (! getent passwd ubuntu >/dev/null || userdel --remove ubuntu) && groupadd -r -g 1000 kafka && useradd -r -u 1000 -g kafka -d /var/lib/kafka -m kafka && \
    : "${SOURCE_DATE_EPOCH:?SOURCE_DATE_EPOCH must be set for a reproducible build}" && \
    sed -ri "s/^([^:]*:[^:]*):[0-9]*:/\1:$((SOURCE_DATE_EPOCH/86400)):/" /etc/shadow && \
    rm -f /etc/passwd- /etc/shadow- /etc/group- /etc/gshadow-
COPY --from=jbuild /opt/kafka /opt/kafka
RUN mkdir -p /var/lib/kafka/data /etc/kafka/docker /etc/kafka/secrets /mnt/shared/config /opt/kafka/config /opt/kafka/logs && chown -R kafka:kafka /var/lib/kafka/data /etc/kafka/docker /etc/kafka/secrets /mnt/shared/config /opt/kafka/config /opt/kafka/logs
COPY server.properties /etc/kafka/docker/server.properties
RUN chmod 0644 /etc/kafka/docker/server.properties
RUN cp /opt/kafka/readystack-docker/* /etc/kafka/docker/ && rm -rf /opt/kafka/readystack-docker && cp /opt/kafka/config/log4j2.yaml /opt/kafka/config/tools-log4j2.yaml /etc/kafka/docker/ && chmod 0755 /etc/kafka/docker/run /etc/kafka/docker/launch /etc/kafka/docker/configure /etc/kafka/docker/configureDefaults /etc/kafka/docker/bash-config && chown -R kafka:kafka /etc/kafka /var/lib/kafka /mnt/shared/config /opt/kafka/config /opt/kafka/logs
LABEL org.opencontainers.image.licenses="Apache-2.0"
LABEL org.opencontainers.image.title="Apache Kafka"
LABEL org.opencontainers.image.description="Apache Kafka is the open-source event streaming platform: durable, partitioned topics that producers write and consumer groups read at their own pace. This image runs one Kafka 4.4 node in KRaft mode (no ZooKeeper), built from source, with upstream's own Docker configuration interface."
LABEL org.opencontainers.image.source="https://github.com/apache/kafka"
LABEL org.opencontainers.image.version="4.4.0-CE-ubuntu24.04-r7"
LABEL org.opencontainers.image.revision="1156b2752aaa28eafc0b4c4d387e63356793268d"
HEALTHCHECK --interval=30s --timeout=60s --start-period=60s \
  CMD /opt/kafka/bin/kafka-cluster.sh cluster-id --bootstrap-server localhost:9092 >/dev/null 2>&1 || exit 1
WORKDIR /var/lib/kafka
USER kafka
EXPOSE 9092
ENTRYPOINT ["/etc/kafka/docker/run"]
