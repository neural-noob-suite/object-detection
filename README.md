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

## convert to tflite

```
cd tensorflow
bazel run --config=opt tensorflow/lite/toco:toco -- \
  --input_file=interface_graphs/graph_name_version/frozen_inference_graph.pb \
  --output_file=output.tflite \
  --inference_type=FLOAT \
  --input_shape=1,300,300,3 \
  --input_array=Preprocessor/sub \
  --output_arrays=concat,concat_1
```

```
// not sure this is needed, its just here for prosperity
https://www.tensorflow.org/lite/models/object_detection/overview
cd models/research/object_detection
python export_tflite_ssd_graph.py \
  --pipeline_config_path=samples/configs/ssd_mobilenet_v2_coco.config \
  --trained_checkpoint_prefix=train_v4_15k/model.ckpt-15835 \
  --output_directory=tflite \
  --add_postporcessing_op=true
```

## model zoo

https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/detection_model_zoo.md
