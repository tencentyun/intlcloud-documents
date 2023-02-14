
<dx-alert infotype="explain" title="">
This document is written by a Cloud GPU Service user and is for study and reference only.
</dx-alert>

## Overview
This document describes how to use a GPU instance to train a ViT model offline to complete a simple image classification task.


## ViT Model Overview
The Vision Transformer (ViT) model is proposed by Alexey Dosovitskiy to get the state-of-the-art (SOTA) result from multiple tasks.
![](https://qcloudimg.tencent-cloud.cn/raw/118faac2352673dcd4a207dfb3c79a51.png)


For an input image, ViT splits it into multiple subimage patches. Each patch is spliced with position embedding and combined with class labels to be input to transformer encoder together. After the corresponding output layer results of the class label positions pass through a network, the ViT result will be output. In the pretraining status, the ground truth of the result can replaced by a patch of the mask.


## Instance Environment
- **Instance type**: In this document, you can select a [GN7](https://intl.cloud.tencent.com/document/product/560/19701) or [GN8](https://intl.cloud.tencent.com/document/product/560/19701) model. Based on the GPU performance comparison provided in [Tesla P40 vs Tesla T4](https://technical.city/en/video/Tesla-P40-vs-Tesla-T4), the performance of T4 in Turing architecture is higher than that of P40 in Pascal architecture. Therefore, GN7.5XLARGE80 is selected in this document.
- **Region**: As large datasets may need to be uploaded, we recommend you select the region with the lowest latency. This document uses the [online ping](https://cloud.feitsui.com/tencent) tool for testing. As the latency between the test region and Chongqing region where GN7 resides is the lowest, Chongqing region is selected in this example.
- **System disk**: 100 GB Premium Cloud Storage disk.
- **Operating system**: Ubuntu 18.04.
- **Bandwidth**: 5 Mbps.
- **Local operating system**: macOS


## Directions

### Setting passwordless login for your instance (optional)

1. (Optional) You can configure the server alias in `~/.ssh/config` on your local server. In this document, the alias `tcg` is used.
2. Run the `ssh-copy-id` command to copy the SSH public key of the local server to the GPU instance.
3. Run the following command in the GPU instance to disable password login to enhance security:
```shellsession
echo 'PasswordAuthentication no' | sudo tee -a /etc/ssh/ssh\_config
```
4. Run the following command to restart the SSH service.
```shellsession
sudo systemctl restart sshd
```


### Configuring the PyTorch-GPU development environment
To use pytorch-gpu for development, you need to further configure the environment as follows:

1. Install the NVIDIA graphics card driver.
Run the following command to install the NVIDIA graphics card driver:
```shellsession
sudo apt install nvidia-driver-418
```
After the installation is completed, run the following command to check whether the installation is successful:
```shellsession
nvidia-smi
```
If the following result is returned, the installation is successful.
![](https://qcloudimg.tencent-cloud.cn/raw/b8faab7af92e4a7c58930a970aa69325.png)
2. Configure the conda environment.
Run the following commands to configure the conda environment:
```shellsession
wget https://repo.anaconda.com/miniconda/Miniconda3-py39\_4.11.0-Linux-x86\_64.sh
```
```shellsession
chmod +x Miniconda3-py39\_4.11.0-Linux-x86\_64.sh
```
```shellsession
./Miniconda3-py39\_4.11.0-Linux-x86\_64.sh
```
```shellsession
rm Miniconda3-py39\_4.11.0-Linux-x86\_64.sh
```
3. Compile the `~/.condarc` file to add the following software source information and replace the conda software source with the Qinghua source.
```shellsession
channels:

   - defaults

show\_channel\_urls: true

default\_channels:

   - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main

   - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/r

   - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/msys2

custom\_channels:

  conda-forge: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud

  msys2: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud

  bioconda: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud

  menpo: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud

  pytorch: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud

  pytorch-lts: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud

  simpleitk: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
```
4. Run the following command to set the `pip` source to the Tencent Cloud image source.
```shellsession
pip config set global.index-url https://mirrors.cloud.tencent.com/pypi/simple
```
5. Install PyTorch.
Run the following command to install PyTorch:
```shellsession
conda install pytorch torchvision cudatoolkit=11.4 -c pytorch --yes
```
Run the following commands to view whether PyTorch is installed successfully:
```shellsession
python
```
```shellsession
import torch
```
```shellsession
print(torch.cuda.is_avaliable())
```
If the following result is returned, PyTorch is installed successfully:
![](https://qcloudimg.tencent-cloud.cn/raw/12b5f76946fd80ff46a4e4dfa9aed2cd.png)



### Preparing the experiment data
The test task in this training is an image classification task and uses the flower image classification dataset in the Tencent Cloud online document. The dataset contains five classes of flowers and is 218 MB in size. Below are the sampled dataset results (examples of images of flowers in each class):
![](https://main.qcloudimg.com/raw/cb16186fcf4cf98a6764face437a59ca.png)

The data of each class in the raw dataset is stored in the folder of the corresponding class. You need to convert it to the standard format of ImageNet and divide the training and verification datasets at the ratio of 4:1. Use the following code to convert the format:
```python
# split data into train set and validation set, train:val=scale

import shutil

import os

import math

scale = 4

data\_path = '../raw'

data\_dst = '../train\_val'

#create imagenet directory structure

os.mkdir(data\_dst)

os.mkdir(os.path.join(data\_dst, 'train'))

os.mkdir(os.path.join(data\_dst, 'validation'))

for item in os.listdir(data\_path):

    item\_path = os.path.join(data\_path, item)

 if os.path.isdir(item\_path):

        train\_dst = os.path.join(data\_dst, 'train', item)

        val\_dst = os.path.join(data\_dst, 'validation', item)

        os.mkdir(train\_dst)

        os.mkdir(val\_dst)

        files = os.listdir(item\_path)

 print(f'Class {item}:\n\t Total sample count is {len(files)}')

        split\_idx = math.floor(len(files) \* scale / ( 1 + scale ))

 print(f'\t Train sample count is {split\_idx}')

 print(f'\t Val sample count is {len(files) - split\_idx}\n')

 for idx, file in enumerate(files):

            file\_path = os.path.join(item\_path, file)

 if idx <= split\_idx:

                shutil.copy(file\_path, train\_dst)

 else:

                shutil.copy(file\_path, val\_dst)

print(f'Split Complete. File path: {data\_dst}')
```
Below is the dataset overview:
```shellsession
Class roses:

     Total sample count is 641

     Train sample count is 512

     Validation sample count is 129

Class sunflowers:

     Total sample count is 699

     Train sample count is 559

     Validation sample count is 140

Class tulips:

     Total sample count is 799

     Train sample count is 639

     Validation sample count is 160

Class daisy:

     Total sample count is 633

     Train sample count is 506

     Validation sample count is 127

Class dandelion:

     Total sample count is 898

     Train sample count is 718

     Validation sample count is 180
```

To accelerate the training process, you need to further convert the dataset to a GPU-friendly format such as NVIDIA Data Loading Library (DALI). The DALI library can use GPU to replace CPU to accelerate data preprocessing. When data in the ImageNet format already exists, you can simply run the following command to use DALI:
```shellsession
git clone https://github.com/ver217/imagenet-tools.git

cd imagenet-tools && python3 make\_tfrecords.py \

  --raw\_data\_dir="../train\_val" \

  --local\_scratch\_dir="../train\_val\_tfrecord" && \

python3 make\_idx.py --tfrecord\_root="../train\_val\_tfrecord"  
```


### Model training result
To facilitate subsequent training of large distributed models, this document describes how to train and develop a model based on the distributed training framework [Colossal-AI](https://colossalai.org/). Colossal-AI provides a set of easy-to-use APIs, which enables you to easily perform data, model, pipeline, and mixed parallel training.
Based on the demo provided by Colossal-AI, this document uses ViT integrated in the [pytorch-image-models](https://github.com/rwightman/pytorch-image-models) repository for implementation. The minimum `vit\_tiny\_patch16\_224` model at a resolution of 224\*224 is used, where each sample is divided into 16 `patches`.
1. Run the following command to install Colossal-AI and pytorch-image-models as instructed in Start Locally:
```shellsession
pip install colossalai==0.1.5+torch1.11cu11.3 -f https://release.colossalai.org
```
```shellsession
pip install timm
```
2. Write the following model training code based on the [demo](https://github.com/hpcaitech/ColossalAI-Examples) provided by Colossal-AI:
```python
from pathlib import Path

from colossalai.logging import get\_dist\_logger

import colossalai

import torch

import os

from colossalai.core import global\_context as gpc

from colossalai.utils import get\_dataloader, MultiTimer

from colossalai.trainer import Trainer, hooks

from colossalai.nn.metric import Accuracy

from torchvision import transforms

from colossalai.nn.lr\_scheduler import CosineAnnealingLR

from tqdm import tqdm

from titans.utils import barrier\_context

from colossalai.nn.lr\_scheduler import LinearWarmupLR

from timm.models import vit\_tiny\_patch16\_224

from titans.dataloader.imagenet import build\_dali\_imagenet

from mixup import MixupAccuracy, MixupLoss

def main():

    parser = colossalai.get\_default\_parser()

    args = parser.parse\_args()

    colossalai.launch\_from\_torch(config='./config.py')

    logger = get\_dist\_logger()

 # build model

    model = vit\_tiny\_patch16\_224(num\_classes=5, drop\_rate=0.1)

 # build dataloader

    root = os.environ.get('DATA', '../train\_val\_tfrecord')

    train\_dataloader, test\_dataloader = build\_dali\_imagenet(

        root, rand\_augment=True)

 # build criterion

    criterion = MixupLoss(loss\_fn\_cls=torch.nn.CrossEntropyLoss)

 # optimizer

    optimizer = torch.optim.SGD(

        model.parameters(), lr=0.1, momentum=0.9, weight\_decay=5e-4)

 # lr\_scheduler

    lr\_scheduler = CosineAnnealingLR(

       optimizer, total\_steps=gpc.config.NUM\_EPOCHS)

    engine, train\_dataloader, test\_dataloader, \_ = colossalai.initialize(

        model,

        optimizer,

        criterion,

        train\_dataloader,

        test\_dataloader,

    )

 # build a timer to measure time

    timer = MultiTimer()

 # create a trainer object

    trainer = Trainer(engine=engine, timer=timer, logger=logger)

 # define the hooks to attach to the trainer

    hook\_list = [

        hooks.LossHook(),

        hooks.LRSchedulerHook(lr\_scheduler=lr\_scheduler, by\_epoch=True),

        hooks.AccuracyHook(accuracy\_func=MixupAccuracy()),

        hooks.LogMetricByEpochHook(logger),

        hooks.LogMemoryByEpochHook(logger),

        hooks.LogTimingByEpochHook(timer, logger),

        hooks.TensorboardHook(log\_dir='./tb\_logs', ranks=[0]),

        hooks.SaveCheckpointHook(checkpoint\_dir='./ckpt')

    ]

 # start training

    trainer.fit(train\_dataloader=train\_dataloader,

                epochs=gpc.config.NUM\_EPOCHS,

                test\_dataloader=test\_dataloader,

                test\_interval=1,

                hooks=hook\_list,

                display\_progress=True)

if \_\_name\_\_ == '\_\_main\_\_':

    main()
```
Below is the specific model configuration:
```shellsession
from colossalai.amp import AMP\_TYPE

BATCH\_SIZE = 128

DROP\_RATE = 0.1

NUM\_EPOCHS = 200 

CONFIG = dict(fp16=dict(mode=AMP\_TYPE.TORCH))

gradient\_accumulation = 16

clip\_grad\_norm = 1.0

dali = dict(

    gpu\_aug=True,

    mixup\_alpha=0.2

)
```
Below is the model execution process. Each epoch time is within 20s:
![](https://qcloudimg.tencent-cloud.cn/raw/0b9d0c91d5a05acd5808b8e71211e4a8.png)
The result shows that the highest accuracy of the model with the verification dataset is 66.62%. You can also increase the number of model parameters; for example, you can change the model to `v![](https://qcloudimg.tencent-cloud.cn/raw/34f6f93aa9479375e23ccee3dd31dd68.png).


## Summary
The biggest problem encountered in this example was that cloning from GitHub was very slow. To solve this, a tunnel and ProxyChains were used for acceleration. However, such operations violated the CVM use rules and caused a period of unavailability. Eventually, this problem was solved by deleting the proxy and submitting a ticket.
Using a public network proxy doesn't comply with the CVM use regulations. To guarantee the stable operations of your business, do not violate the regulations.


## References
[1] Dosovitskiy, Alexey, et al. "An image is worth 16x16 words: Transformers for image recognition at scale." arXiv preprint arXiv:2010.11929 (2020).
[2] [NVIDIA/DALI](https://github.com/NVIDIA/DALI)
[3] Bian, Zhengda, et al. "Colossal-AI: A Unified Deep Learning System For Large-Scale Parallel Training." arXiv preprint arXiv:2110.14883 (2021).
