FROM centos:latest

ADD https://support.illumina.com/content/dam/illumina-support/documents/downloads/software/bcl2fastq/bcl2fastq2-v2-20-0-linux-x86-64.zip /tmp/bcl2fastq.zip

RUN set -e \
      && yum -y upgrade \
      && yum -y install unzip \
      && unzip -d /tmp /tmp/bcl2fastq.zip \
      && yum -y install /tmp/bcl2fastq2-*.rpm \
      && yum -y autoremove \
      && yum clean all \
      && rm -rf /var/cache/yum /tmp/bcl2fastq*

ENTRYPOINT ["/usr/local/bin/bcl2fastq"]
