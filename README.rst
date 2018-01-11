Docker Images for Running Tests with TensorFlow on Travis CI
============================================================

.. image:: https://travis-ci.org/korepwx/travis-tensorflow-docker.svg?branch=master
    :target: https://travis-ci.org/korepwx/travis-tensorflow-docker

This is a Ubuntu 16.04 Docker image for running tests with various versions of Python and TensorFlow on `Travis CI <https://travis-ci.org>`_.

+----------+--------+------------+
| Tag      | Python | TensorFlow |
+==========+========+============+
| py2tf1.2 | 2.7    | 1.2.1      |
+----------+--------+------------+
| py2tf1.3 | 2.7    | 1.3.0      |
+----------+--------+------------+
| py2tf1.4 | 2.7    | 1.4.1      |
+----------+--------+------------+
| py2tf1.5 | 2.7    | 1.5.0rc0   |
+----------+--------+------------+
| py3tf1.2 | 3.6    | 1.2.1      |
+----------+--------+------------+
| py3tf1.3 | 3.6    | 1.3.0      |
+----------+--------+------------+
| py3tf1.4 | 3.6    | 1.4.1      |
+----------+--------+------------+
| py3tf1.5 | 3.6    | 1.5.0rc0   |
+----------+--------+------------+

Packages
--------

* Ubuntu 16.04
* Apt: build-essential, wget, git
* Python: numpy, six, coverage, mock, pytest, sphinx, matplotlib, pillow, ipython[all]

Usage
-----

An example `.travis.yml`::

    sudo: required
    services:
      - docker
    env:
      matrix:
      - PYTHON_VERSION=2.7 TENSORFLOW_VERSION=1.2.1
      - PYTHON_VERSION=2.7 TENSORFLOW_VERSION=1.3.0
      - PYTHON_VERSION=2.7 TENSORFLOW_VERSION=1.4.1
      - PYTHON_VERSION=2.7 TENSORFLOW_VERSION=1.5.0-rc0
      - PYTHON_VERSION=3.6 TENSORFLOW_VERSION=1.2.1
      - PYTHON_VERSION=3.6 TENSORFLOW_VERSION=1.3.0
      - PYTHON_VERSION=3.6 TENSORFLOW_VERSION=1.4.1
      - PYTHON_VERSION=3.6 TENSORFLOW_VERSION=1.5.0-rc0
    install:
      - docker pull "ipwx/travis-tensorflow-docker:py${PYTHON_VERSION:0:1}tf${TENSORFLOW_VERSION:0:3}"
    script:
      - docker run
          -v "$(pwd)":"$(pwd)"
          -w "$(pwd)"
          -e PYTHON_VERSION="${PYTHON_VERSION}"
          -e TENSORFLOW_VERSION="${TENSORFLOW_VERSION}"
          "ipwx/travis-tensorflow-docker:py${PYTHON_VERSION:0:1}tf${TENSORFLOW_VERSION:0:3}"
          bash -c "pip install -r requirements.txt && python -m unittest"

Development
-----------

To populate the Dockerfiles, execute the following command::

    pip install jinja2
    python Dockerfile.py

Local Build
-----------

::

    # to build a certain variant, for example, py3tf1.4
    docker build \
        --build-arg UBUNTU_MIRROR=archive.ubuntu.com \
        --build-arg CACHEBUST="$(date +%s)" \
        -t ipwx/travis-tensorflow-docker:py3tf1.4 \
        py3tf1.4
