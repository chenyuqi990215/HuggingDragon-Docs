## Quick Start: Trajectory Recovery with HuggingDragon

In this tutorial, we will walk you through an example of using HuggingDragon for the Trajectory Recovery task using the Porto dataset.

#### Prerequisites

Before starting, make sure you have the following:

- HuggingDragon installed and set up on your machine.
- Python 3.7 or higher installed.

#### Trajectory Recovery

* 1. Download the trajectory dataset

We provide the Porto dataset, which is identical to the one used in our paper, RNTrajRec.

* 2. Run the Porto dataset with MTrajRec model

```bash
# Create the output directory
mkdir -p outputs/MTrajRec_Porto

# Run the training task
python -m huggingdragon.entry.train_trajectory_recovery config/trajectory_recovery/MTrajRec_Porto.yml
```

The results will be saved in the `outputs/MTrajRec_Porto` directory.

* 3. Modifying default parameters in the config file

If you want to modify the default parameters in the YAML config file, such as changing the `online_features_flag` from `false` to `true`, you can do the following:

```bash
mkdir -p outputs/MTrajRec_Porto_online_features_flag

python -m huggingdragon.entry.train_trajectory_recovery config/trajectory_recovery/MTrajRec_Porto.yml \
    --flag.online_features_flag true \
    --runtime.output_dir outputs/MTrajRec_Porto_online_features_flag
```

The results will be saved in the `outputs/MTrajRec_Porto_online_features_flag` directory.
