#############################
Creating a Trajectory Dataset
#############################

Data Format
===========

The data format of raw trajectory is simple. Each trajectory is represented as following.

.. code-block:: console

    timestamp-1 lat-1 lon-1 rid-1
    timestamp-2 lat-2 lon-2 rid-2
    ...
    timestamp-n lat-n lon-n rid-n
    -cnt <--optionals>

For raw trajectory without map matching ``rid`` can be ``-1``.

.. tip::

    * ``-cnt``: Specifies the ID of the trajectory.
    * ``<--optionals>``: Specifies the extra information of the trajectory, like ``--uid <uid>``.


Perform Map Matching
====================

To perform map matching, please run the following scripts.

.. code-block:: console

    python -m scripts.hmm --map_root <map_root> --zone_range <zone_range> --traj_path <traj_path> --tmp_path <tmp_path> --output_path <output_path>


.. tip::

    Before running the above script, you should first build the C++ file using the following commands.

    .. code-block:: console

        cd scripts/
        g++ hmm.cpp -o hmm

For instance, run the following script for Porto dataset:

.. code-block:: console

    python -m scripts.porto --input_path ./data/trajectory/Porto/train.csv --output_path ./data/trajectory/Porto/process.txt
    python -m scripts.hmm --map_root ./data/road_network/Porto/ --zone_range [41.08,-8.69,41.27,-8.40] --traj_path ./data/trajectory/Porto/process.txt --tmp_path ./data/trajectory/Porto/tmp.txt --output_path ./data/trajectory/Porto/raw.txt

