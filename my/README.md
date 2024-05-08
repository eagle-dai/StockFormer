
## Environment
- python3 (version >= 3.9)

```bash
python3 -m venv ./venv
source ./venv/bin/activate
# To activate venv on Windows, command: .\venv\Scripts\activate

python -m pip install --upgrade pip
pip install -r requirements.txt
```

### Verify GPU
```
> python
import torch
print(torch.__version__)
2.3.0+cu121
print(torch.cuda.is_available())
True
```

If cuda is not avaialble, refert to:
- run nvidia-smi to check driver and cuda versions. Reinstall proper vsersion of nvidia GPU driver if needed.
- pip uninstall torch torchvision torchaudio
- reinstall: https://pytorch.org/, e.g.,
  pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu121


## 1st stage：Representation Learning

1）Relational state inference module training: 

```bash
cd code/Transformer/script
sh train_mae.sh
```

2）Long-term state inference module training:

```bash
cd code/Transformer/script
sh train_pred_long.sh
```

3）Short-term state inference  module training:

```bash
cd code/Transformer/script
sh train_pred_short.sh
```

4）Select the best model of three state inference modules from '*code/Transformer/checkpoints/*' according to their performance on validation set and add them to '*code/Transformer/pretrained/*'

**OR** directly use the model which have been pretrained in advance by us (dir:'*code/Transformer/pretrained/csi/* ')

## 2nd stage：Policy Learning

1) train SAC model (three state inference module's path can be changed in *train_rl.py* file)

```bash
python train_rl.py
```

2) get prediction result on test set from '*code/results/df_print/*'
