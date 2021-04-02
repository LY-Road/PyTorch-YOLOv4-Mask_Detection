# PyTorch-YOLOv4-Mask_Detection
● 使用YOLOv4实现口罩佩戴检测
训练100个epochs，在验证集上效果
Class|Precision|Recall|mAP@.5
--|--|--|--
all|0.79|0.906|0.918
### 配置环境
> $ pip3 install -r requirements.txt
### 下载数据集 
images：https://pan.baidu.com/s/1m-4Z80T4IBtJXrlJrRW9pg 提取码：zpbw  
labels：https://pan.baidu.com/s/1L-fYqoylbEKMyiKXCXz-7g 提取码：szqg  

### 口罩数据集预训练模型
链接：https://pan.baidu.com/s/1jQVOnqoy0HAswB67R8BQ0w 提取码：gypi  
将下载好的模型放在weights文件夹下。

### 数据处理
将下载好的images和labels放在data/mydata文件夹下，train.txt和valid.txt我已经生成好放在mydata文件夹下了。
### 修改数据读取配置文件
找到data/coco.yaml，需要修改的内容如下：
> train: data/mydata/train.txt/   &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  # 训练数据路径  
> val: data/mydata/valid.txt/     &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  # 验证数据路径  
> test: data/mydata/valid.txt/     &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  # 测试数据路径，这里用的是验证集数据，也可以选择其他数据   
> nc: 2                            &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; # num_classes=2  
> names: ['face_not_mask','face_mask'] &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; # claes_name
### 修改模型配置文件
找到cfg/yolov4-pacsp.cfg，搜索[yolo]，将[yolo]上面的filters=255修改为filters=21，下面的classes=80修改为classes=2，总共有三个位置需要修改。

### 训练
执行如下代码：
>$ python train.py --device 0 --batch-size 16 --img 640 640 --data coco.yaml --cfg cfg/yolov4-pacsp.cfg --name yolov4-pacsp

加载预训练权重执行如下代码：
>$ python train.py --device 0 --batch-size 16 --img 640 640 --data coco.yaml --cfg cfg/yolov4-pacsp.cfg --weights weights/best.pth --name yolov4-pacsp

### 测试
>$ python test.py --img 640 --conf 0.001 --batch 8 --device 0 --data coco.yaml --cfg cfg/yolov4-pacsp.cfg --weights weights/best.pth
 
### 参考代码
https://github.com/WongKinYiu/PyTorch_YOLOv4
