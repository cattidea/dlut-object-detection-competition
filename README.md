# DLUT Object Detection Competition

[2021 DLUT 目标识别挑战赛](https://teach.dlut.edu.cn/info/1016/10777.htm)

## Installation

### Installing from source

```bash
git clone https://github.com/cattidea/dlut-object-detection-competition.git
cd dlut-object-detection-competition/
pip3 install poetry --user
poetry install
```

## Inference

```bash
poetry run yolo-detect --images data/samples/
```

还有很多参数，比如下面这样：

```bash
poetry run yolo-detect \
             --images data/val \
             --model config/cattidea-yolov4.cfg \
             --weights checkpoints/yolo_ckpt_127.pth \
             --classes data/object_detection_dataset_train/classes.names \
             --conf_thres 0.35 \
             --nms_thres 0.7 \
             --soft_nms \
             --multiscale_testing \
             --text_only
```

使用 Colab 训练好的推理模型：

   - [GitHub Releases](https://github.com/cattidea/dlut-object-detection-competition/releases/tag/v1.0.0)
   - [Google Drive](https://drive.google.com/file/d/12GIcunQ7jmeXF1Fot7AWsHm1VggOgaJZ/view?usp=sharing)
   - [Baidu Netdisk](https://pan.baidu.com/s/1FcYdJIcvYiw51ApiQTtaQg) Extract code: dh9u

## Train

建议直接使用 Colab，这里有已经写好的 [Colab Notebook: dlut-object-detection-competition](https://colab.research.google.com/drive/1lW3jsdbdBSZyDF40gcvTFttUSSNQjnrx?usp=sharing)


### Download pretrained weights

```bash
cd /weights/
sh ./download_weights.sh
```

### Generate custom model config

```bash
cd config/
sh <model_generation_script> <num_classes> <image_size> <config_name>
```

比如像下面这样：

```bash
cd config/
sh ./create_custom_yolov4_model.sh 49 416 cattidea-yolov4.cfg
```

### Configure custom data config

对照 `config/custom.data` 配置即可

## References

- 整体基于：<https://github.com/eriklindernoren/PyTorch-YOLOv3>
- 多尺度测试：<https://zhuanlan.zhihu.com/p/266887169>
- Soft NMS: <https://github.com/DongPoLI/NMS_SoftNMS/blob/main/soft_nms.py>
- YOLOv4 模型结构及预训练参数：<https://github.com/AlexeyAB/darknet#how-to-train-to-detect-your-custom-objects>
