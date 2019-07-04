# object-detection

## requirements

virtualenv is recommended.

```
pip install -r requirements.txt
```

And read TENSORFLOW.md

## start training

```
cd models/research/object_detection
mkdir train
python model_main.py \
  --logtostderr \
  --model_dir ./train \
  --pipeline_config_path ./samples/config/\*.config
```

## export interface graph

```
python export_inference_graph.py \
  --input_type image_tensor \
  --pipeline_config_path ./samples/configs/faster_rcnn_inception_v2_coco.config \
  --trained_checkpoint_prefix ./train/model.ckpt-47325
  --output_directory interface_graphs/graph_name_version/
```

## monitor training

```
tensorboard --logdir=models/research/object_detection/train
```

## test graph

```
python detect.py
```

## model zoo

https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/detection_model_zoo.md
