###########
Quick Start
###########

In this tutorial, we will walk you through an example of using HuggingDragon for the Trajectory Recovery task using the Porto dataset.

Prerequisites
=============

Before starting, make sure you have the following:

- HuggingDragon installed and set up on your machine.
- Python version 3.8 is installed.

Trajectory Recovery
===================

.. tabs::

    .. tab:: Step 1

        * Download the trajectory dataset

        We provide the Porto dataset in `link <https://drive.google.com/file/d/1O0hozbJtYxmK4gAIGj9fM6cm-moXtzVz/view?usp=drive_link>`_.

        Please download the dataset and put it under ``data/trajectory/Porto/``.

    .. tab:: Step 2

        * Run the Porto dataset with MTrajRec model

        .. code-block:: console

            # Create the output directory
            mkdir -p outputs/MTrajRec_Porto

            # Run Training
            python -m huggingdragon.entry.train_trajectory_recovery config/trajectory_recovery/MTrajRec_Porto.yml


        The results will be saved in the `outputs/MTrajRec_Porto` directory.

    .. tab:: Step 3

        * Modifying default parameters in the config file

        If you want to modify the default parameters in the YAML config file, such as changing the `online_features_flag` from `false` to `true`, you can do the following:

        .. code-block:: console

            mkdir -p outputs/MTrajRec_Porto_online_features_flag

            python -m huggingdragon.entry.train_trajectory_recovery config/trajectory_recovery/MTrajRec_Porto.yml \
                --flag.online_features_flag true \
                --runtime.output_dir outputs/MTrajRec_Porto_online_features_flag

        The results will be saved in the `outputs/MTrajRec_Porto_online_features_flag` directory.
