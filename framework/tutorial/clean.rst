.. _framework-tutorial-clean:

Stop Galaxy and clean environment
=================================

Galaxy runs as a background process and have to be stopped manually:

.. code-block:: bash

    $ ./src/stop_galaxy.sh

Once stopped, the environment must be cleared with:

.. code-block:: bash

    $ ./src/clean_galaxy.sh

.. bibliography:: /assets/references.bib
   :cited:
   :style: plain
   :filter: docname in docnames
