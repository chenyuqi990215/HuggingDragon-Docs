###############
Config Settings
###############

The experiment parameter configuration is determined by three aspects: the parameters passed by the command line, the user-defined configuration file (``yaml`` style file), and parameters passed through training entry file.

Parameter Priority
==================

command line parameters > user-defined configuration file > parameters passed through training entry file > default parameters of the model module > default parameters of other modules.

.. tip::

    The parameters with higher priority will override the parameters with the same name of lower priority.

User-defined Configuration File
===============================

Command Line Parameters
=======================

Default Configuration
=====================