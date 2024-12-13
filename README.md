# Traffic4cast-Prediction


# Traffic4cast 2021 

## Artifacts
- Visualize Static and Dynamic Dataset
- Study high-resolution 8-channel traffic movies of entire cities
- Cover spatial domain shifts and predict traffic for unseen cities
- Incorporate road network information and detect patterns on graphs


After cloning this [repo](https://github.com/iarai/NeurIPS2021-traffic4cast.git),
download [data](https://www.iarai.ac.at/traffic4cast/forums/forum/competition/competition-2021/) and extract data to `data/raw` subfolder, run

```bash
conda activate t4c

export PYTHONPATH="$PYTHONPATH:$PWD"

DEVICE=cpu
DATA_RAW_PATH="./data/raw"
GROUND_TRUTH=""


# run one of the following:

# a UNet with separate training for temporal cities and fine-tuning for spatiotemporal cities
python baselines/baselines_unet_separate.py --model_str=unet --limit=2 --epochs=10 --batch_size=1 --num_workers=1 --data_raw_path=$DATA_RAW_PATH  --device=$DEVICE $GROUND_TRUTH

# gcn: graph-based model
python baselines/baselines_cli.py --model_str=gcn           --limit=2 --epochs=10 --batch_size=1 --num_workers=1 --train_fraction=0.97 --val_fraction=0.03  --file_filter="**/*BERLIN*8ch.h5" --data_raw_path=$DATA_RAW_PATH --device=$DEVICE $GROUND_TRUTH
```
