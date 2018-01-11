Docker Images for Running Tests with TensorFlow on Travis CI
============================================================

This is a Ubuntu 16.04 Docker image for running tests with various versions of TensorFlow on `Travis CI <travis-ci.org>`_.

Major Packages
--------------

* Ubuntu 16.04
* Ubuntu Packages: build-essential, wget, git
* Python: 2.7, 3.5, 3.6
* Python Packages: numpy, six, coverage, mock, pytest, sphinx, matplotlib, ipython[all]
* TensorFlow: 1.2.1, 1.3.0, 1.4.1, 1.5.0rc0

Development
-----------

To populate the Dockerfiles, execute the following command::

    pip install jinja2
    python Dockerfile.py

Installation
------------

::

    # to build a certain variant, for example, py35tf141
    docker build \
        --build-arg UBUNTU_MIRROR=archive.ubuntu.com \
        --build-arg CACHEBUST="$(date +%s)" \
        -t ipwx/travis-tensorflow-docker:py35tf141 \
        py35tf141
