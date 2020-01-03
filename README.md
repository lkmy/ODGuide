# [Detectron2](https://github.com/facebookresearch/detectron2) 
介绍：Detectron2包含了众多的目标检测算法的实现，例如DensePose, panoptic feature pyramid networks,和Mask RCNN的各种变种等等。目前已经应用于Facebook内部的多个工程应用中，例如搭建先进的姿态估计模型然后部署在Facebook的Smart Camera中。通过全新的模块化设计，Detectron2具有更高的灵活性和可扩展性，能够直接在单个或多个GPU服务器进行更快的训练，同时能够帮助研究人员更有效的探索最先进的算法设计。

## 1 特性
+ 基于PyTorch：PyTorch可以提供更直观的命令式编程模型，开发者可以更快的进行迭代模型设计和实验。
+ 模块化、可扩展：从Detectron2开始，Facebook引入了模块化设计，允许用户将自定义模块插入目标检测系统的几乎任何部分。这意味着许多新的研究项目和核心Detectron2库可以完全分开。其可扩展性也使得Detectron2更加灵活。
+ 支持语义分割和全景分割。
+ 速度和可扩展性：速度很快，可以方便地进行GPU服务器的分布式训练。 

## 2 安装 
 ### 2.1 环境需要：  
   + Python ≥ 3.6  
   + PyTorch ≥ 1.3  
   + OpenCV  
   + pycocotools  
   + GCC>=4.9

 ### 2.2 安装教程  
  1. 安装Anaconda3  
  2. 创建虚拟环境[detectron2.yml]()  
  ```  
    conda env create -f detectron2.yml 
  ```  
   3. 环境变量
  ```
    vim ~/.bashrc
    # 在后续的安装detectron2和运行程序的过程中，用到的都是'pyd'指向的虚拟环境中,已安装好pytorch cv等适应版本包的python3.6
    alias pyd=/home/XXX/anaconda3/envs/detectron2/bin/python3
    source ~/.bahrc
    # 初次安装、后续运行detectron2都需要首先激活detectron2虚拟环境
    conda activate detectron2
  ```
  4. 安装detectron2
  注：因为后续要存放数据集，可以放在share下
  ```
    git clone https://github.com/facebookresearch/detectron2.git  
    cd detectron2  
    pyd setup.py build develop  
  ```

## 3 使用测试  
进入detectron2安装根目录
  ```
  pyd demo/demo.py --config-file configs/COCO-Detection/faster_rcnn_R_50_FPN_3x.yaml \
    --input 1.jpg 2.jpg 3.jpg 4.jpg \
    --output /指定的输出路径 \
    --opts MODEL.WEIGHTS detectron2://COCO-Detection/faster_rcnn_R_50_FPN_1x/137257794/model_final_b275ba.pkl
  ```
  注：MODEL.WEIGHTS 可以是存放自己已训练好的， 与config-file对应的模型参数的地址，  
      如 /home/share/xxx/detectron2/output/model_final.pth  
      也可以是[model zool](https://github.com/facebookresearch/detectron2/blob/master/MODEL_ZOO.md)里训练好的模型
## 4 部分检测模型与用法详解
  [Cacade R-CNN]()  
  [TrientNet]()
## 5 框架资料  
[documentation](https://detectron2.readthedocs.io/tutorials/extend.html)
[使用展示](https://colab.research.google.com/drive/16jcaJoc6bCFAQ96jDe2HwtXj7BMD_-m5)
