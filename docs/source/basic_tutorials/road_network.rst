=======================
Creating a Road Network
=======================

In this tutorial, we show how to train with your own road network. We suggest to put road networks under ``data/road_network/``.

File Structure of Road Network
==============================

.. code-block:: console

    data/
    └── road_network/
        └── <City Name>/
            ├── nodeOSM.txt
            ├── edgeOSM.txt
            ├── wayTypeOSM.txt
            └── poiOSM.txt (optional)

* ``nodeOSM.txt``: This file contains data related to the nodes in the road network, where each line contains the ID, latitude and longitude of an intersection in the road network.

* ``edgeOSM.txt``: This file contains data related to the edges (road segments) in the road network, where each line contains the ID, the node ID that the road segment starts/ends with and the coordinates that make up the road segment.

* ``wayTypeOSM.txt``: This file contains data specifying the type of each road in the network, where each line contains the ID, way type name and way type ID of each road segment.

* ``poiOSM.txt`` (optional): This file contains data related to points of interest (POIs) in the road network, where each line contains the ID, latitude, longitude and type of each POI in the road network.


Create From Open Street Map
===========================

OpenStreetMap (OSM) is a collaborative mapping project that aims to create a free and editable map of the world. It provides an open and accessible platform for individuals and organizations to contribute geographic data, including roads, buildings, landmarks, and points of interest. OSM data is widely used by various applications, researchers, and developers for mapping, navigation, and spatial analysis purposes.

To create a new road network from OSM website, please follow the following steps.

.. tabs::

    .. tab:: Step 1

        * Download OSM Data

        Download the OSM data for your desired area from `Geofabrik <https://download.geofabrik.de/>`_ in the ``.osm.pbf`` format.

        Geofabrik provides pre-processed extracts of OSM data for different regions and countries, making it easier to obtain the data you need.

    .. tab:: Step 2

        * Download ``osm2rn`` tool.

        The osm2rn tool is a powerful software utility designed to extract data from OpenStreetMap (OSM) data. To install the tool, run the following commands.

        .. code-block:: console

            git clone https://github.com/sjruan/osm2rn.git
            cd osm2rn

        .. tip:: Please follow `osm2rn <https://github.com/sjruan/osm2rn>`_ to install the requirements.

        Note that to successfully install ``GDAL``, please use the following command instead of the command recommended in ``osm2rn``.

        Remove conda-forge and use the default channel as suggested in the `issue <https://github.com/ContinuumIO/anaconda-issues/issues/10351>`_:

        .. code-block:: console

            conda install --channel defaults gdal

    .. tab:: Step3

        * Clip the data according to your region of interest (following ``osm2rn``).

        To clip the OSM data using ``osm2rn``, run the following command.

        .. code-block:: console

            python osm_clip.py --input_path asia-latest.osm.pbf --output_path interest_region.osm.pbf --min_lat <min_lat> --min_lng <min_lng> --max_lat <max_lat> --max_lng <max_lng>

        .. tip::

            * ``input_path``: Specifies the path to the input OSM data file.
            * ``output_path``: Specifies the path for the output file that will contain the clipped data.
            * ``min_lat``: Specifies the minimum latitude value of the region of interest.
            * ``min_lng``: Specifies the minimum longitude value of the region of interest.
            * ``max_lat``: Specifies the maximum latitude value of the region of interest.
            * ``max_lng``: Specifies the maximum longitude value of the region of interest.

            Make sure to replace ``<min_lat>``, ``<min_lng>``, ``<max_lat>``, and ``<max_lng>`` with the appropriate values for your specific region of interest.

    .. tab:: Step 4

        * Run ``scipts/osm2rn.py`` and store the road network.

        In the final step of the preprocessing phase, you need to run the modified ``osm2rn.py`` script to generate the road network file in our desired format.

        .. code-block:: console

            python -m scripts.osm2rn --input_path interest_region.osm.pbf --output_path interest_region

        .. tip::

            * Replace ``interest_region.osm.pbf`` with the path and filename of the clipped OSM data file obtained in the previous step.
            * Replace ``interest_region`` with the desired output path and filename for the generated road network file.


Extract Extra POI features
==========================

Extracting Extra Points of Interest (POI) features from OpenStreetMap (OSM) data enables the extraction of specific information about various locations such as restaurants, banks, parks, and landmarks. By leveraging the rich geospatial data in OSM, this process provides valuable insights for mapping, analysis, and decision-making purposes. To extract POI features from OSM data, please follow the following steps.

.. tabs::

    .. tab:: Step 1

        * Install ``osmosis`` tool.

        ``Osmosis`` is a powerful command-line tool for manipulating and processing OpenStreetMap (OSM) data, allowing users to perform various operations such as filtering, merging, and transforming OSM data to meet specific requirements. To install the tool, run the following commands:

        .. code-block:: console

            wget https://github.com/openstreetmap/osmosis/releases/download/0.48.3/osmosis-0.48.3.tgz
            mkdir osmosis
            mv osmosis-0.48.3.tgz osmosis
            cd osmosis
            tar xvfz osmosis-0.48.3.tgz
            rm osmosis-0.48.3.tgz
            chmod a+x bin/osmosis

    .. tab:: Step 2

        * Extract POIs from ``.osm.pbf`` format files using ``osmosis`` tool.

        To extract POI features using ``osmosis`` tool, run the following commands:

        .. code-block:: console

            bin/osmosis --rbf interest_region.osm.pbf --nk keyList="amenity" --wx interest_region.osm

        .. tip:: Please ensure that ``Java`` is installed.

    .. tab:: Step 3

        * Run ``scripts/osm2poi.py`` to extract POIs from xml.

        In the final step, you need to run the following command to generate ``poiOSM.txt``:

        .. code-block:: console

            python -m scripts.osm2poi --input_path interest_region.osm --output_path interest_region

        .. tip:: ``output_path`` is a dictionary instead of the path to the file.

        .. note::

            We follow `website <https://wiki.openstreetmap.org/wiki/Key:amenity>`_ to map each POI type to category label.

Convert from Libcity format to ours
===================================

`LibCity <https://github.com/LibCity/Bigscity-LibCity>`_ is an open-source Python library developed by the Bigscity Research Group. It provides a comprehensive framework for urban computing and transportation research. We provide tools to convert trajectory datasets and road networks to our format.

.. code-block:: console

    python -m scripts.libcity --input_path <input_path> --rn_prefix <rn_prefix> --output_rn_path <output_rn_path> --traj_prefix <traj_prefix> --output_traj_path <output_traj_path>

.. tip::

    * ``input_path``: Specifies the root dictionary of Libcity data.
    * ``rn_prefix``: Specifies the prefix name of the road network.
    * ``output_rn_path``: Specifies the path to store the road network.
    * ``traj_prefix``: Specifies the prefix name of the trajectory.
    * ``output_traj_path``: Specifies the path to store the trajectories.

    Make sure to download required data from Libcity and replace ``<input_path>``, ``<rn_prefix>``, ``<output_rn_path>``, ``<traj_prefix>``, and ``<output_traj_path>`` with the appropriate values.

For instance, to convert Beijing dataset in `link <https://github.com/aptx1231/START/blob/master/bj-data-introduction.md>`_, run

.. code-block:: console

    python -m scripts.libcity --input_path <input_path> --rn_prefix bj_roadmap_edge --output_rn_path ./data/road_network/Beijing --traj_prefix traj_bj_11 --output_traj_path <output_traj_path>

The above command will convert road network and trajectory data simultaneously, if you only want to convert the road network, please use the following command:

.. code-block:: console

    python -m scripts.libcity --input_path <input_path> --rn_prefix <rn_prefix> --output_rn_path <output_rn_path> --task rn