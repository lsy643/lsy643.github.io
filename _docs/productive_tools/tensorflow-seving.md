## Using Tensorflow Serving for Model Deployment

Tensorflow Serving is the official way to deploy model trained with Tensorflow.

### Build tensorflow_model_server

The *tensorflow_model_server* is the executable to serve the model with GPU support.

Build the GPU-enabled tensorflow_model_server currently should follow instructions below
(the official instruction seems not to work):

1. Nvidia-docker:
It's highly recommended to build the tensorflow_model_server in nvidia-docker image:
    ```
    nvidia/cuda:8.0-cudnn6-devel-ubuntu16.04
    ```


1. Envrionment Setting:
    ```
    export TF_NEED_CUDA=1
    export TF_NEED_GCP=0
    export TF_NEED_JEMALLOC=1
    export TF_NEED_HDFS=0
    export TF_NEED_OPENCL=0
    export TF_ENABLE_XLA=0
    export TF_CUDA_VERSION=8.0
    export TF_CUDNN_VERSION=6
    export TF_CUDA_COMPUTE_CAPABILITIES="3.7,3.7"
    export CUDA_TOOLKIT_PATH="/usr/local/cuda"
    export CUDNN_INSTALL_PATH="/usr/lib/x86_64-linux-gnu"
    export GCC_HOST_COMPILER_PATH="/usr/bin/gcc"
    export PYTHON_BIN_PATH="/usr/bin/python"
    export CC_OPT_FLAGS="-march=native"
    export PYTHON_LIB_PATH="/usr/local/lib/python2.7/site-packages"
    export LD_LIBRARY_PATH="/usr/local/cuda/lib64":$LD_LIBRARY_PATH
    ```

1. Install Dependencies:
    ```
    apt-get update
    apt-get install -y build-essential curl libcurl3-dev git zlib1g-dev
    apt-get install -y libfreetype6-dev libpng12-dev libzmq3-dev zip
    apt-get install -y pkg-config python-dev python-numpy python-pip software-properties-common
    ```

1. Build the tensorflow_model_server:
    1. version chosen:
        ```
        Tensorflow: r1.2
        Serving: r0.6
        ```
    1. Setting for Bazel
        ```
        sed -i.bak 's/@org_tensorflow\/\/third_party\/gpus\/crosstool/@local_config_cuda\/\/crosstool:toolchain/g' tools/bazel.rc
        sed -i.bak 's/external\/nccl_archive\///g' tensorflow/tensorflow/contrib/nccl/kernels/nccl_manager.h
        sed -i.bak 's/external\/nccl_archive\///g' tensorflow/tensorflow/contrib/nccl/kernels/nccl_ops.cc
        ```
    1. Build the executable
        ```
        bazel build -c opt --config=cuda tensorflow_serving/model_servers:tensorflow_model_server
        ```
    1. Move the executable and Clean the docker container
        ```
        cp bazel-bin/tensorflow_serving/model_servers/tensorflow_model_server /usr/local/bin/
        bazel clean --expunge
        ```

### Build Models for Serving
1. Create the Model
    Just follow the code provided by the [tensorflow_serving](https://github.com/tensorflow/serving.git)

1. Run the model
    ```
    tensorflow_model_server --port={port_num} --model_name={model_name} --model_base_path={model_path} &> inception_log &
    ```

### Serving Client
The client heavily depends on Tensorflow and GRPC.

Working on to create one client with self-contained dependencies