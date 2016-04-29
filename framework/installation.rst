.. _framework-installation:

Installation
============

ASaiM framework is based on a custom Galaxy instance (Figure 1). This customization is done using several bash and Ansible scripts. 

Download code sources
#####################

Source code of ASaiM framework are available on a `GitHub repository <https://github.com/ASaiM/framework/>`_.

Git
***

To get ASaiM framework, ``git`` clone the project:

.. code-block:: bash

    $ git clone http://github.com/ASaiM/framework.git

Releases
********

All releases of ASaiM framework can be found at `https://github.com/ASaiM/framework/releases <https://github.com/ASaiM/framework/releases>`_.

.. _framework-installation-requirements:

Requirements
############

Some tools must be installed:

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
- ``proftpd``
- ``postgresql``

It can be automatically done by running:

.. code-block:: bash

    $ ./src/install_dependencies.sh

.. note::

    ``apt-get`` is required for Debian, ``yum`` for RHEL and ``homebrew`` for MacOSX.


