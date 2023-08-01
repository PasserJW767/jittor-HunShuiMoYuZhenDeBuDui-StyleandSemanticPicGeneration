# Jittor-浑水摸鱼真的不队-风格及语义引导的风景图像生成赛题(赛题一)

## 简介

本目录基于第三届计图挑战赛baseline进行训练，单卡训练时间约为45epoch/24h。原仓库地址：https://github.com/Jittor/JGAN/tree/master/models/gaugan

测试时，SPADE网络可以完成一张参考的ref图+一张label Mask图通过网络输出一张生成图。

## 安装

#### 运行环境

- ubuntu 21.04 LTS
- python >= 3.7
- jittor >= 1.3.0

#### 安装依赖

```bash
pip install -r requirements.txt # 本目录下的requirements.txt
```

#### 数据集

赛事训练数据集[由此下载](https://cloud.tsinghua.edu.cn/f/063e7fcfe6a04184904d/?dl=1)。

预训练模型采用的是 `Jittor` 框架自带的 `vgg19` 模型，无需额外下载，在代码运行的过程中会载入到内存里。

## 训练

在单卡上训练：

```bash
sh train.sh
```
此前需要修改train.sh，其内容为：
```bash
# train.sh
CUDA_VISIBLE_DEVICES="0" python train.py --input_path {训练数据集路径（即train_resized文件夹所在路径）}
```
## 测试

在单卡上进行测试：

```bash 
sh test.sh
```

此前需要：
1. 将label与img的映射关系（label_to_img.json）放置在gaugan目录下
2. 修改test.sh，其内容为：
```bash
CUDA_VISIBLE_DEVICES="0" python test.py  \
--input_path {测试数据集路径（即labels文件夹所在路径），它提供label mask图} \
--img_path {训练数据集的图片路径（即train_resized/imgs文件夹所在路径，它提供ref图）}
--which_epoch 150
```

在此，我们训练的最优模型150_net_D.pkl、150_net_E.pkl、150_net_G.pkl均已放在./checkpoints/bs4vae文件夹下。

## 致谢

本文完全参考了官方开源代码：[https://github.com/Jittor/JGAN/tree/master/models/gaugan](https://github.com/Jittor/JGAN/tree/master/models/gaugan)。