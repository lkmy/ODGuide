# 1 数据集  
## &nbsp;&nbsp;COCO  
&emsp;{detectron2根目录}/coco/  
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;val2017  
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;train2017  
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;annotations   

detectron2硬编码了数据集读取位置，所以运行train/test等需要载入数据集的操作，必须运行在detectron2根目录下  
## &nbsp;&nbsp;自定义数据集  
detectron2采用注册机制 train/test前都要进行数据集的注册操作。
