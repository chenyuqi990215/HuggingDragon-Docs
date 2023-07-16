===================================
Download Datasets from Google Drive
===================================

We provide processed data for research purpose.

Processed Road Network
======================

We provide processed road networks on Porto and Beijing in `road network <https://drive.google.com/drive/folders/1dJ4kosqtbidUCDxVb4sPXjaMew_R-OWk?usp=drive_link>`_, please download it and put them under ``data`` folder.

.. tip::

    Note that the road networks mentioned above may not be the most up-to-date version, as this information is provided solely for the purpose of reproducing the results shown in this repository.

    For more information, please see :doc:`new road network <../basic_tutorials/road_network>`.

Raw Trajectory Dataset
======================

We provide three trajectory datasets.

.. tabs::

    .. tab:: Porto

        The `Porto <https://www.kaggle.com/datasets/crailtap/taxi-trajectory>`_ taxi dataset is an open dataset available on Kaggle. We provide map-matched trajectories in `Porto.txt <https://drive.google.com/file/d/1O0hozbJtYxmK4gAIGj9fM6cm-moXtzVz/view?usp=drive_link>`_.

        We also provide code for processing raw trajectory data downloaded from kaggle website.

        .. code-block:: console

            python -m scripts.porto --input_path <input_path> --output_path <output_path>

    .. tab:: T-drive

        The `T-drive <https://www.microsoft.com/en-us/research/publication/t-drive-trajectory-data-sample/>`_ taxi dataset is an open dataset provided by Microsoft. It contains trajectory data from taxi rides. We provide map-matched trajectory in `T-drive.txt <https://drive.google.com/file/d/146C0NR8w86eG9Q4WJB2RoHdIIlGVSjnj/view?usp=drive_link>`_.

        We also provide code for processing raw trajectory data downloaded from Microsoft website:

        .. code-block:: console

            python -m scripts.tdrive --input_path <input_path> --output_path <output_path>

    .. tab:: Beijing

        The `Beijing <https://github.com/aptx1231/START/blob/master/bj-data-introduction.md>`_ taxi dataset is provided in Libcity. We provide map-matched trajectories in `Beijing.txt <https://drive.google.com/file/d/17eQHZbxTK-hjbR_Na7n_7EMI_i2f9AuV/view?usp=drive_link>`_.

        .. note::

            For more information about processing Beijing dataset, please see :doc:`new road network <../basic_tutorials/road_network>`.

.. note::

    To use the map matching result, please make sure to use the road network we provided.


.. tip::

    To generate task specific trajectory datasets, please see :doc:`preprocess <../basic_tutorials/preprocess>`.

    We provide a processed Porto dataset for trajectory recovery task shown in :doc:`quick start <quick_start>` in `here <https://drive.google.com/drive/folders/1QNADHYKQNSo574S04iyOjh4LYySSpC2N?usp=drive_link>`_.