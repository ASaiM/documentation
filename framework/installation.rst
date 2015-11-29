.. _framework-installation:

Installation
############

Download code sources
=====================

Git
---

To get ASaiM framework, `git` clone the project:

.. code-block:: bash

    $ git clone git@github.com:ASaiM/framework.git

Releases
--------

All releases of ASaiM framework can be found at `https://github.com/ASaiM/framework/releases <https://github.com/ASaiM/framework/releases>`_.

Requirements
============

Some tools must be installed before launching any scripts:

- `git`
- `python`
- `pip`
- `perl`
- `scons`
- `mercurial`
- `openssl`
- `java` 
- `wget`
- `openssl`
- `proftpd` (installed in `/usr/local`)
- `postgresql`

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

**Note:** `apt-get` is required for Debian, `yum` for RHEL and `homebrew` for MacOSX.

Configuration
=============

PostgreSQL is used to manage databases in Galaxy. It must be launched as a background 
tasks. PostgreSQL database must be then setup for Galaxy (new database and user creation).
Launch and setup of PostgreSQL is done by running:

.. code-block:: bash

    $ ./src/postgresql/configure_postgres.sh


The FTP server with `proftpd` has to be configured and launched, by running:

.. code-block:: bash

    $ ./src/proftpd/configure_proftpd.sh


All the configuration (postgresql and proftpd) can be done by running:

.. code-block:: bash

    $ ./src/configure.sh



