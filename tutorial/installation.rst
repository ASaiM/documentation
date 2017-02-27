.. _framework-tutorial-installation:

Launch the ASaiM framework
==========================

To :ref:`install and launch the framework <framework-installation>`, you will need `Docker <https://www.docker.com/products/overview#h_installation>`_. 

For Linux users and people familiar with the command line, please follow the `very good instructions <https://docs.docker.com/installation/>`_ from the Docker project. Non-Linux users are encouraged to use `Kitematic <https://kitematic.com>`_, a graphical User-Interface for managing Docker containers.

Once Docker is installed, the launch of the ASaiM framework is easy

.. code-block:: bash

    $ docker run -d -p 8080:80 quay.io/bebatut/asaim-framework

The ASaiM framework will be accessible at `http://localhost:8080 <http://localhost:8080>`_.

For more details and more custom installation, please read :ref:`"Installation and usage"<framework-installation>`


