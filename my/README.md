
## Environment
- vscode
- python3 (version >= 3.9)

```bat
python -m venv ./venv
.\venv\Scripts\activate
rem or: source ./venv/bin/activate
```

In VS Code, select Python interpreter to the "venv".

Run in git bash:
```
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
- run nvidia-smi to check driver and cuda versions. Reinstall driver if needed
- pip uninstall torch torchvision torchaudio
- reinstall: https://pytorch.org/

## 1st stage：Representation Learning

1）Relational state inference module training: 

```bat
cd code\Transformer\script
train_mae.bat
```

2）Long-term state inference module training:

```bat
cd code\Transformer\script
train_pred_long.bat
```

3）Short-term state inference  module training:

```bat
cd code\Transformer\script
train_pred_short.bat
```

4）Select the best model of three state inference modules from '*code\Transformer\checkpoints\*' according to their performance on validation set and add them to '*code\Transformer\pretrained\*'

**OR** directly use the model which have been pretrained in advance by us (dir:'*code\Transformer\pretrained\csi\* ')
