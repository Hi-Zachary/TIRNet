# Text as Illumination: Spatial Contrastive Retinex Learning for Language-guided Medical Image Segmentation

## Environment Setup

```bash
# Option 1: Create from environment.yml
conda env create -f environment.yml
conda activate tirnet

# Option 2: Manual setup
conda create -n tirnet python=3.10 -y
conda activate tirnet
pip install -r requirements.txt
```

## Pre-trained Weights

Download [ViT-B/32.pt](https://openaipublic.azureedge.net/clip/models/40d365715913c9da98579312b702a82c18be219cc2a73407c4526f58eba950af/ViT-B-32.pt) and place it under `pretrained/`.

## Datasets

Refer to [LViT](https://github.com/HUANGLIZI/LViT) to download the datasets. Place or symlink data under `datasets/`:

```
datasets/QaTa-COV19-v2/{Train_Folder,Val_Folder,Test_Folder}
datasets/MosMedData+Dataset/{Train_Folder,Val_Folder,Test_Folder}
```

Each folder requires `img/`, `labelcol/`, and the corresponding `*_text.xlsx`.

## Training

```bash
python train_model.py --cfg_path config_qata --gpu 0
python train_model.py --cfg_path config_mosmed --gpu 0
```

Outputs are saved under `outputs/<dataset>/TIRNet/session_*/`.

## Testing

```bash
# Test a specific training session
python test_model.py --cfg_path config_qata --test_session <session_name> --gpu 0

# Test with a specific model checkpoint
python test_model.py --cfg_path config_qata --model_path outputs/QaTa/TIRNet/<session>/models/best_model-TIRNet.pth.tar --gpu 0
```
