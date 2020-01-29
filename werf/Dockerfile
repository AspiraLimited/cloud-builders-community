FROM gcr.io/cloud-builders/gcloud

ARG HELM_VERSION=v3.3.1
ARG WERF_VERSION=v1.1.22+fix20

COPY entrypoint.bash /builder/entrypoint.bash

RUN chmod +x /builder/entrypoint.bash && \
  mkdir -p /builder/helm && \
  apt-get update && \
  apt-get install -y curl && \
  curl -SL https://get.helm.sh/helm-${HELM_VERSION}-linux-amd64.tar.gz -o helm.tar.gz && \
  tar zxvf helm.tar.gz --strip-components=1 -C /builder/helm linux-amd64 && \
  rm helm.tar.gz && \
  mkdir -p /builder/werf && \
  curl -SL "https://dl.bintray.com/flant/werf/${WERF_VERSION}/werf-linux-amd64-${WERF_VERSION}" -o /builder/werf/werf && \
  chmod +x /builder/werf/werf && \
  apt-get --purge -y autoremove && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/*

ENV PATH=/builder/helm/:$PATH
ENV PATH=/builder/werf/:$PATH

ENTRYPOINT ["/builder/entrypoint.bash"]
