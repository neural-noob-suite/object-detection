# tensorflow

tensorflow-gpu is highly recommended.

https://www.tensorflow.org/install/source

```
git clone git@github.com:tensorflow/tensorflow.git
pip install /tmp/tensorflow_pkg/tensorflow-version-tags.whl
```

# protobuf

This is needed to compile models protocol buffers

```
git clone git@github.com:protocolbuffers/protobuf.git
cd protobuf
./autogen.sh
./configure
make
```

# models

```
git clone git@github.com:tensorflow/models.git
cd models/research
protobuf/src/protoc object_detection/protos/*.proto --python_out=.
export PYTHONPATH=$PYTHONPATH:`pwd`:`pwd`/slim
python setup.py install # or build/install
```

* use config from models/research/object_detection/samples/config/\*.config
