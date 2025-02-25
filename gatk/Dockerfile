FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

ADD https://raw.githubusercontent.com/dceoy/print-github-tags/master/print-github-tags /usr/local/bin/print-github-tags

RUN set -e \
      && apt-get -y update \
      && apt-get -y dist-upgrade \
      && apt-get -y install --no-install-recommends --no-install-suggests \
        ca-certificates curl g++ gcc default-jre libc6-dev make python \
        python3 r-base \
      && apt-get -y autoremove \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

RUN set -e \
      && chmod +x /usr/local/bin/print-github-tags \
      && print-github-tags --release --latest --tar broadinstitute/gatk \
        | xargs -i curl -SL {} -o /tmp/gatk.tar.gz \
      && tar xvf /tmp/gatk.tar.gz -C /usr/local/src --remove-files \
      && mv /usr/local/src/gatk-* /usr/local/src/gatk \
      && Rscript /usr/local/src/gatk/scripts/docker/gatkbase/install_R_packages.R \
      && ln -s /usr/local/src/gatk/gatk /usr/local/bin/gatk

ENTRYPOINT ["/usr/local/bin/gatk"]
