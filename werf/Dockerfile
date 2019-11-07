FROM gcr.io/cloud-builders/gcloud

ARG HELM_VERSION=v2.14.0
ARG WERF_VERSION=v1.0.4-beta.9

COPY entrypoint.bash /builder/entrypoint.bash

RUN chmod +x /builder/entrypoint.bash && \
  apt-get update && \
  apt-get install -y curl && \
  mkdir -p /builder/helm && \
  curl -SL "https://storage.googleapis.com/kubernetes-helm/helm-${HELM_VERSION}-linux-amd64.tar.gz" -o helm.tar.gz && \
  tar zxvf helm.tar.gz --strip-components=1 -C /builder/helm linux-amd64/helm linux-amd64/tiller && \
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
