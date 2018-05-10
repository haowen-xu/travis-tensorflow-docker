FROM ubuntu:16.04

MAINTAINER Haowen Xu <public@korepwx.com>

ARG UBUNTU_MIRROR=archive.ubuntu.com
ENV LANG=en_US.UTF-8
ENV LC_ALL=en_US.UTF-8
ENV PATH="/miniconda/bin:${PATH}"
ENV SHELL=/bin/bash


RUN sed -i "s/archive.ubuntu.com/${UBUNTU_MIRROR}/g" /etc/apt/sources.list && \
    DEBIAN_FRONTEND=noninteractive apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get -y dist-upgrade && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends apt-utils && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
        build-essential \
        ca-certificates \
        wget \
        git \
        locales \
        language-pack-en \
    && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    wget https://repo.continuum.io/miniconda/Miniconda-latest-Linux-x86_64.sh \
            -O /tmp/miniconda.sh \
            && \
    /bin/bash /tmp/miniconda.sh -b -p /miniconda && \
    rm /tmp/miniconda.sh && \
    conda config --set always_yes yes --set changeps1 no && \
    conda update --yes -q conda && \
    conda info -a && \
    conda install --yes -q python=2.7 && \
    python -m pip install --ignore-installed --upgrade pip setuptools && \
    python -m pip install --ignore-installed --upgrade numpy coverage mock pytest sphinx matplotlib pillow "coveralls>=1.1" && \
    python -m pip install "ipython[all]<6" && \
    python -m pip install tensorflow==1.3.0

CMD ["/bin/bash"]
