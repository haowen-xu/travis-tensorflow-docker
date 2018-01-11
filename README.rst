Docker Images for Running Tests with TensorFlow on Travis CI
============================================================

.. image:: https://travis-ci.org/korepwx/travis-tensorflow-docker.svg?branch=master
    :target: https://travis-ci.org/korepwx/travis-tensorflow-docker

This is a Ubuntu 16.04 Docker image for running tests with various versions of Python and TensorFlow on `Travis CI <travis-ci.org>`_.

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

Development
-----------

To populate the Dockerfiles, execute the following command::

    pip install jinja2
    python Dockerfile.py

Installation
------------

::

    # to build a certain variant, for example, py3tf1.4
    docker build \
        --build-arg UBUNTU_MIRROR=archive.ubuntu.com \
        --build-arg CACHEBUST="$(date +%s)" \
        -t ipwx/travis-tensorflow-docker:py3tf1.4 \
        py3tf1.4
