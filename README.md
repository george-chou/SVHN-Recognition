# svhn_recognition
[![license](https://img.shields.io/github/license/Genius-Society/svhn_recognition.svg)](https://github.com/Genius-Society/svhn_recognition/blob/master/LICENSE)
[![hf](https://img.shields.io/badge/huggingface-svhn_dataset-ffd21e.svg)](https://huggingface.co/datasets/Genius-Society/svhn)
[![hf](https://img.shields.io/badge/huggingface-svhn_model-ffd21e.svg)](https://huggingface.co/Genius-Society/svhn)
[![hf](https://img.shields.io/badge/huggingface-svhn_space-ffd21e.svg)](https://huggingface.co/spaces/Genius-Society/svhn)
[![ms](https://img.shields.io/badge/modelscope-svhn_dataset-624aff.svg)](https://www.modelscope.cn/datasets/Genius-Society/svhn)
[![ms](https://img.shields.io/badge/modelscope-svhn_model-624aff.svg)](https://www.modelscope.cn/models/Genius-Society/svhn)
[![ms](https://img.shields.io/badge/modelscope-svhn_studio-624aff.svg)](https://www.modelscope.cn/studios/Genius-Society/svhn)

This project is a PyTorch implementation that uses deep CNN to recognize multi-digit numbers using the SVHN dataset derived from Google Street View house numbers, each picture contains a set of numbers from 0 to 9, the model is tested to have 89% accuracy.

## Environment
```bash
conda create -n py311 python=3.11 -y
conda activate py311
pip install -r requirements.txt
```

## Usage
1. Clone the source code:
```bash
git clone git@github.com:Genius-Society/svhn_recognition.git
cd svhn_recognition
```
2. Run `convert_to_lmdb.py`
3. Run `train.py`

## Dataset
[Street View House Number](http://ufldl.stanford.edu/housenumbers/SVHN) Dateset 来源于谷歌街景门牌号码

本次任务的目标数据集是其中的 Format 1 (Full Numbers: train.tar.gz, test.tar.gz , extra.tar.gz)

其中, train.tar.gz 为训练数据集, test.tar.gz为测试数据集。注: extra.tar.gz是附加数据集, 建议不使用。

在 train.tar.gz 与 test.tar.gz 中，分别包含：<br>
1) 一些 .png 格式的图片，每张图片包含一个门牌号；<br>
2) 一个 digitStruct.mat 文件，包含每张图片所对应的门牌号，以及每个门牌号数字的位置信息；<br>
3) 一个 see_bboxes.m 文件，用于辅助 Matlab 环境下的处理，请忽略之。

## Tasks
1. 设计一个网络，用 train.tar.gz 中的数据进行训练，并用 test.tar.gz 中的数据进行测试；
2. 在测试的过程中，不允许使用 test.tar.gz/digitStruct.mat 文件中的位置信息作为输入，即必须在“忽略测试数据集中给出的位置信息”的前提下，识别出 test.tar.gz 中每张图片中的门牌号；
3. 撰写一份报告，包含如下信息：<br>
    (1) 所设计的网络的结构和超参数信息；<br>
    (2) 网络的训练方法和优化方法；<br>
    (3) 体现训练过程的“训练曲线”；<br>
    (4) 识别准确率；

## Params
<table>
    <tr>
        <th>Steps</th>
        <th>GPU</th>
        <th>Batch Size</th>
        <th>Learning Rate</th>
        <th>Patience</th>
        <th>Decay Step</th>
        <th>Decay Rate</th>
        <th>Accuracy</th>
    </tr>
    <tr>
        <td>122000</td>
        <td>GTX 1080 Ti</td>
        <td>512</td>
        <td>0.01</td>
        <td>100</td>
        <td>625</td>
        <td>0.9</td>
        <td>89.21%</td>
    </tr>
</table>

## Training curve
![](./docs/loss.png)

## Reference
[1] [Multi-digit Number Recognition from Street View Imagery using Deep Convolutional Neural Networks](http://arxiv.org/pdf/1312.6082.pdf)