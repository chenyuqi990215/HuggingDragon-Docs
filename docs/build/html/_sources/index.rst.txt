.. HuggingDragon documentation master file, created by
   sphinx-quickstart on Sun Jul  9 21:07:11 2023.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

########################
HuggingDragon's Document
########################


HuggingDragon is an advanced and unified framework designed to revolutionize trajectory-based applications within the realm of intelligent transportation systems (ITS). Our objective is to offer researchers a robust experimental tool and a convenient development framework, facilitating the exploration and implementation of trajectory-based applications.

----

.. tip:: Please make sure that all the datasets and checkpoints are used for **research purpose only**.


Fast Installation
=================

Currently, HuggingDragon can only be installed from source code.

To proceed with the installation, please create an environment with Python version ``3.8`` and execute the following commands:

.. code-block:: console

   git clone https://github.com/chenyuqi990215/HuggingDragon.git
   cd HuggingDragon
   python setup.py install

Features
========

* **Unified Framework**: HuggingDragon provides a unified framework that integrates multiple trajectory-based tasks and applications within intelligent transportation systems, offering a centralized solution for various trajectory analysis needs.

* **Extensibility**: HuggingDragon is designed to be extensible, allowing researchers and developers to easily incorporate new tasks, algorithms, and models into the framework, fostering flexibility and adaptability to evolving research needs.

* **Comprehensive Task Support**: HuggingDragon currently supports essential tasks such as trajectory recovery and trajectory similarity, facilitating effective comparison and analysis for trajectory-based applications.

* **Systematic Pipeline**: HuggingDragon provides a systematic pipeline that encompasses all necessary steps and components related to trajectory-based tasks, ensuring a structured and efficient workflow for researchers and developers.

* **Reproducibility and Standardization**: HuggingDragon emphasizes reproducibility and standardization in the field of trajectory-based applications. By providing a comprehensive and consistent framework, it enables researchers to compare results, validate findings, and contribute to the advancement of the field.


.. toctree::
   :hidden:
   :maxdepth: 1
   :caption: Getting Started

   Download Datasets<get_started/download.rst>
   Installation<get_started/install.rst>
   Quick Start<get_started/quick_start.rst>
   Project Structure<get_started/structure.rst>

.. toctree::
   :hidden:
   :maxdepth: 1
   :caption: Basic Tutorials

   Create a Road Network<basic_tutorials/road_network.rst>
   Create a Trajectory Dataset<basic_tutorials/trajectory.rst>
   Trajectory Preprocess<basic_tutorials/preprocess.rst>
   Config Settings<basic_tutorials/config.rst>

.. toctree::
   :hidden:
   :maxdepth: 1
   :caption: Advanced Usage

   Tips for Coding<advanced/tips.rst>
   Write Config File<advanced/config.rst>
   Customize Network<advanced/network.rst>
   Customize Task<advanced/task.rst>

.. toctree::
   :hidden:
   :maxdepth: 1
   :caption: Supported Tasks

   Overview<task/task.rst>
   Trajectory Recovery<task/trajrec.rst>

.. toctree::
   :hidden:
   :maxdepth: 1
   :caption: Visualization

   Trajectory Recovery<visualization/trajectory_recovery.ipynb>