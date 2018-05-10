Docker Images for Running Tests with TensorFlow on Travis CI
============================================================

.. image:: https://travis-ci.org/korepwx/travis-tensorflow-docker.svg?branch=master
    :target: https://travis-ci.org/korepwx/travis-tensorflow-docker

This is a Ubuntu 16.04 Docker image for running tests with various versions of Python and TensorFlow on `Travis CI <https://travis-ci.org>`_.

+----------+--------+------------+--------------------------------------------------------------------------------------------------+
| Tag      | Python | TensorFlow | Status                                                                                           |
+==========+========+============+==================================================================================================+
| py2tf1.2 | 2.7    | 1.2.1      | .. image:: https://travis-matrix-badges.herokuapp.com/repos/korepwx/tfsnippet/branches/master/1  |
+----------+--------+------------+--------------------------------------------------------------------------------------------------+
| py3tf1.2 | 3.5    | 1.2.1      | .. image:: https://travis-matrix-badges.herokuapp.com/repos/korepwx/tfsnippet/branches/master/2  |
+----------+--------+------------+--------------------------------------------------------------------------------------------------+
| py2tf1.3 | 2.7    | 1.3.0      | .. image:: https://travis-matrix-badges.herokuapp.com/repos/korepwx/tfsnippet/branches/master/3  |
+----------+--------+------------+--------------------------------------------------------------------------------------------------+
| py3tf1.3 | 3.5    | 1.3.0      | .. image:: https://travis-matrix-badges.herokuapp.com/repos/korepwx/tfsnippet/branches/master/4  |
+----------+--------+------------+--------------------------------------------------------------------------------------------------+
| py2tf1.4 | 2.7    | 1.4.1      | .. image:: https://travis-matrix-badges.herokuapp.com/repos/korepwx/tfsnippet/branches/master/5  |
+----------+--------+------------+--------------------------------------------------------------------------------------------------+
| py3tf1.4 | 3.5    | 1.4.1      | .. image:: https://travis-matrix-badges.herokuapp.com/repos/korepwx/tfsnippet/branches/master/6  |
+----------+--------+------------+--------------------------------------------------------------------------------------------------+
| py2tf1.5 | 2.7    | 1.5.0      | .. image:: https://travis-matrix-badges.herokuapp.com/repos/korepwx/tfsnippet/branches/master/7  |
+----------+--------+------------+--------------------------------------------------------------------------------------------------+
| py3tf1.5 | 3.5    | 1.5.0      | .. image:: https://travis-matrix-badges.herokuapp.com/repos/korepwx/tfsnippet/branches/master/8  |
+----------+--------+------------+--------------------------------------------------------------------------------------------------+
| py2tf1.6 | 2.7    | 1.6.0      | .. image:: https://travis-matrix-badges.herokuapp.com/repos/korepwx/tfsnippet/branches/master/9  |
+----------+--------+------------+--------------------------------------------------------------------------------------------------+
| py3tf1.6 | 3.5    | 1.6.0      | .. image:: https://travis-matrix-badges.herokuapp.com/repos/korepwx/tfsnippet/branches/master/10 |
+----------+--------+------------+--------------------------------------------------------------------------------------------------+
| py2tf1.7 | 2.7    | 1.7.1      | .. image:: https://travis-matrix-badges.herokuapp.com/repos/korepwx/tfsnippet/branches/master/10  |
+----------+--------+------------+--------------------------------------------------------------------------------------------------+
| py3tf1.7 | 3.5    | 1.7.1      | .. image:: https://travis-matrix-badges.herokuapp.com/repos/korepwx/tfsnippet/branches/master/11 |
+----------+--------+------------+--------------------------------------------------------------------------------------------------+
| py2tf1.8 | 2.7    | 1.8.0      | .. image:: https://travis-matrix-badges.herokuapp.com/repos/korepwx/tfsnippet/branches/master/12  |
+----------+--------+------------+--------------------------------------------------------------------------------------------------+
| py3tf1.8 | 3.5    | 1.8.0      | .. image:: https://travis-matrix-badges.herokuapp.com/repos/korepwx/tfsnippet/branches/master/13 |
+----------+--------+------------+--------------------------------------------------------------------------------------------------+

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
      - PYTHON_VERSION=2 TENSORFLOW_VERSION=1.2
      - PYTHON_VERSION=3 TENSORFLOW_VERSION=1.2
      - PYTHON_VERSION=2 TENSORFLOW_VERSION=1.3
      - PYTHON_VERSION=3 TENSORFLOW_VERSION=1.3
      - PYTHON_VERSION=2 TENSORFLOW_VERSION=1.4
      - PYTHON_VERSION=3 TENSORFLOW_VERSION=1.4
      - PYTHON_VERSION=2 TENSORFLOW_VERSION=1.5
      - PYTHON_VERSION=3 TENSORFLOW_VERSION=1.5
    install:
      - docker pull "ipwx/travis-tensorflow-docker:py${PYTHON_VERSION}tf${TENSORFLOW_VERSION}"
    script:
      - docker run
          -v "$(pwd)":"$(pwd)"
          -w "$(pwd)"
          -e TRAVIS="${TRAVIS}"
          -e TRAVIS_JOB_ID="${TRAVIS_JOB_ID}"
          -e TRAVIS_BRANCH="${TRAVIS_BRANCH}"
          "ipwx/travis-tensorflow-docker:py${PYTHON_VERSION}tf${TENSORFLOW_VERSION}"
          bash -c "pip install -r requirements.txt && coverage run -m py.test && coveralls"

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
