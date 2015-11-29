.. _framework-installation:

Installation
############

Download code sources
=====================

Git
---

To get ASaiM framework, ``git`` clone the project:

.. code-block:: bash

    $ git clone git@github.com:ASaiM/framework.git

Releases
--------

All releases of ASaiM framework can be found at `https://github.com/ASaiM/framework/releases <https://github.com/ASaiM/framework/releases>`_.

.. _framework-installation-requirements:

Requirements
============

Some tools must be installed before launching any scripts:

- ``git``
- ``python``
- ``pip``
- ``perl``
- ``scons``
- ``mercurial``
- ``openssl``
- ``java``
- ``wget``
- ``openssl``
- ``proftpd`` (installed in ``/usr/local``)
- ``postgresql``

After installation, python dependencies have to be installed in a virtual environment
with pip:

.. code-block:: bash

    $ pip install --upgrade pip
    $ pip install virtualenv
    $ virtualenv --no-site-packages venv
    $ source venv/bin/activate
    $ (venv) pip install -r requirements.txt

For Debian, RHEL and MacOSX, all dependencies can be installed by running:

.. code-block:: bash

    $ ./src/install_dependencies.sh

**Note:** ``apt-get`` is required for Debian, ``yum`` for RHEL and ``homebrew`` for MacOSX.


