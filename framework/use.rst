.. _framework-use:

Usage
#####

To use the ASaiM framework, we recommend to use virtual environment

.. code-block:: bash

    virtualenv --no-site-packages venv
    source venv/bin/activate 

Standard usage
==============
.. _framework-use-standard:

To launch the Galaxy instance corresponding to ASaiM framework

.. code-block:: bash

    cd framework
    ./src/launch_galaxy.sh

The Galaxy instance can be then browse on `http://127.0.0.1:8080/ <http://127.0.0.1:8080/>`_.

In ``src/launch_galaxy.sh``, several Shell scripts are called to configure the instance:

1. Get latest revision of Galaxy from Github
2. Prepare databases and local tools
3. Configure with
    - Custom configuration files
    - Wanted tools
    - Wanted databases
4. Launch Galaxy

Galaxy is simple to use. You can check these videos to have more informations:

Some documentation is also available on :ref:`tool usage <framework-tools-usage>` and :ref:`workflow usage <framework-workflow-usage>`.

Data upload, ftp

Testing
=======

Alternatively, the framework can be tested by running `src/run_tests.sh`. This script configure the Galaxy instance, launch Galaxy's `run_tests.sh` and then test the workflow in `data/demo` with the corresponding input files.



