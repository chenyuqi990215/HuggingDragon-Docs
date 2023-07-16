#####################
Trajectory Preprocess
#####################

In this tutorial, we show how to generate task specific dataset for training specific task.

Trajectory Recovery task
========================

Trajectory dataset for Trajectory Recovery task has the following format.

.. code-block:: console

    ROOT
      ├── train
      |    ├── train_input.txt
      |    └── train_output.txt
      ├── valid
      |    ├── valid_input.txt
      |    └── valid_output.txt
      └── test
           ├── test_input.txt
           └── test_output.txt

To generate training samples from raw trajectories, run

.. code-block:: console

    python -m scripts.trajrec --map_root <map_root> --zone_range <zone_range> --traj_path <traj_path> --epsilon <sample_interval> --min_time <min_time> --max_time <max_time> --ratio <dowmsample_ratio> --save_root <save_root>

To generate Porto dataset, run

.. code-block:: console

    python -m scripts.trajrec --map_root ./data/road_network/Porto/ --zone_range [41.111975,-8.667057,41.177462,-8.585305] --traj_path ./data/trajectory/Porto.txt --epsilon 15 --min_time 600 --max_time 1200 --ratio 8 --save_root ./data/trajectory/Porto/


.. tip::

    * ``epsilon``: Specifies the sample interval of target trajectory.
    * ``ratio``: Specifies the downsample rate, when ``ratio=8``, only 12.5% of GPS points will be saved.

We provide the `trajectory recovery dataset <https://drive.google.com/drive/folders/1QNADHYKQNSo574S04iyOjh4LYySSpC2N?usp=drive_link>`_ on Porto for easy reproduce the experiment results.
