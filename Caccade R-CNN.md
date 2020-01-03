# Train  
首先将coco或自定义数据集放在{detectron2根目录}/datasets下  
注：1.需要载入自定义数据集的代码（train/test)都要先注册自定义数据集。  
    2.数据读取地址被硬编码在了框架中，所以需要载入数据集的代码（train/test)都必须在根目录中运行。
```
conda activate detectron2 # 激活虚拟环境
# pyd是在环境变量中指向的虚拟环境中的python3.6
pyd tools/train_net.py \
	--config-file configs/Misc/cascade_mask_rcnn_R_50_FPN_3x.yaml \
	SOLVER.IMS_PER_BATCH 2 SOLVER.BASE_LR 0.0025
```
说明：  
1. train_net.py 是detectron2提供的可以训练所有模型结构的代码，可以根据需要将其简化。  
默认参数值放在{detectron2根目录}/detectron2/config/defaults.py中。  
训练时，可以将需要修改的参数值直接写在python命令中，见上面代码块的第三行;也可以在train.py中修改训练参数：
```
from detectron2.engine import DefaultTrainer
from detectron2.config import get_cfg

cfg = get_cfg()
cfg.merge_from_file("./detectron2_repo/configs/COCO-InstanceSegmentation/mask_rcnn_R_50_FPN_3x.yaml")
cfg.DATASETS.TRAIN = ("balloon_train",)
cfg.DATASETS.TEST = ()
cfg.DATALOADER.NUM_WORKERS = 2
cfg.MODEL.WEIGHTS = "detectron2://COCO-InstanceSegmentation/mask_rcnn_R_50_FPN_3x/137849600/model_final_f10217.pkl"  # initialize from model zoo
cfg.SOLVER.IMS_PER_BATCH = 2
cfg.SOLVER.BASE_LR = 0.00025
cfg.SOLVER.MAX_ITER = 300    # 300 iterations seems good enough, but you can certainly train longer
cfg.MODEL.ROI_HEADS.BATCH_SIZE_PER_IMAGE = 128   # faster, and good enough for this toy dataset
cfg.MODEL.ROI_HEADS.NUM_CLASSES = 1  # only has one class (ballon)

os.makedirs(cfg.OUTPUT_DIR, exist_ok=True)
trainer = DefaultTrainer(cfg)
trainer.resume_or_load(resume=False)
trainer.train()
```
2. --config-file后接算法模型的配置文件。  
3. 在python命令前使用环境变量CUDA_VISIBLE_DEVICES=， 可以指定运行的GPU号，命令中用--num-gpus 规定使用的的GPU数量，如：  
```
CUDA_VISIBLE_DEVICES=1,3 pyd projects/TridentNet/train_net.py \
--config-file projects/TridentNet/configs/tridentnet_fast_R_101_C4_3x.yaml \
--num-gpus 2 --resume SOLVER.IMS_PER_BATCH 2 SOLVER.BASE_LR 0.0025
```  
4. 当用--resume时，检查断点，自动训练。
