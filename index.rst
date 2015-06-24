ASaiM: a pipeline generator for analysis of intestinal microbiota
#################################################################

ASaiM is a program which can be used to generate pipeline to process and analyze high throughput intestinal microbiota data. `Read more <http://asaim.github.io/about/>`_

ASaiM can be driven via a command-line interface and configuration file generated via a web interface (link)

To install it and its features check out the :ref:`tutorial`, or read the rest of this page for a quick introduction.


Running ASaiM
=============

To run ASaiM, a configuration file in JSON have to be generated, either manually (check out :ref:`configuration-file`) or using the web interface (link).

With this configuration file, ASaiM can be invoked with **make** command from data repository

.. code-block::
	make -f path/to/src/makefile target


What now ?
==========

If you are a user and you want to use ASaiM to process and analyze high throughput data, check out the :ref:`tutorial` and go to :ref:'for-users'.

If you are an curious user or a potential developper and you want to have more information about ASaiM, go to :ref:'for-devs'.

Contributions and Feedback
==========================

Useful links:

- There's a mailing-list for any feedback or question: https://groups.google.com/forum/?hl=fr#!forum/asaim-users
- The repository and issue tracker are on GitHub : https://github.com/asaim

Documentation index
===================

.. toctree::
   :maxdepth: 4

   installation
   tutorial
   for-users/index
   for-devs/index
   faq
   glossary

