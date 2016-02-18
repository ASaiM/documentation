.. _framework-tutorial-installation:

Install and configure the framework
===================================

To :ref:`install the framework <framework-installation>`, clone the `GitHub repository <http://github.com:ASaiM/framework>`_:

.. code-block:: bash

    $ git clone http://github.com/ASaiM/framework.git

Move to the corresponding directory:

.. code-block:: bash

    $ cd framework

:ref:`Install the required dependencies <framework-installation-requirements>`:

.. code-block:: bash

    $ ./src/install_dependencies.sh

:ref:`Configure Galaxy environment <framework-use-configure>`:

.. code-block:: bash

    $ ./src/configure.sh
    
:ref:`Launch ASaiM Galaxy instance <framework-use-launch>`:

.. code-block:: bash

    $ ./src/launch_galaxy.sh


Once you are done with ASaiM Galaxy instance, you have to :ref:`stop it <framework-tutorial-clean>` and :ref:`clean Galaxy environment <framework-tutorial-clean>`.

:ref:`Usage of ASaiM framework <framework-use>` can be sum up by the following scheme:

.. _framework_tutorial_virtual_circle:

.. figure:: /assets/images/framework/usage/virtual_circle.png
    :align: center

    Virtual circle to get ASaiM framework correctly running



