# Notes on Linux
## 1. About setup environment
before inatallation, make sure the "Bazel" and "gRPC" are installed.
for "Bazel", after download the relevant binary from offical site(to directory "Downloads"), remember changing the "~/.bashrc" and sourcing it after the execution
```bash
cd ~/Downloads
chmod +x bazel-0.4.5-installer-linux-x86_64.sh
./bazel-0.4.5-installer-linux-x86_64.sh --user

```
add following sentence to "~/.bashrc", and source it
```bash
export PATH="$PATH:$HOME/bin"
```
other dependencies, include
```bash
sudo apt-get update && sudo apt-get install -y \
        build-essential \
        curl \
        libcurl3-dev \
        git \
        libfreetype6-dev \
        libpng12-dev \
        libzmq3-dev \
        pkg-config \
        python-dev \
        python-numpy \
        python-pip \
        software-properties-common \
        swig \
        zip \
        zlib1g-dev
```` 
then use git clone to install tensorflow serving
```bash
git clone --recurse-submodules https://github.com/tensorflow/serving
cd serving
```
remember to configure the TensorFlow (this is not the same TensorFlow that you installed before, so configure it)
```bash
cd tensorflow
./configure
cd ..
```
use Bazel to build/compile the entire tree
```bash
bazel build -c opt tensorflow_serving/...
```
Binaries are placed in the bazel-bin directory, and can be run using a command like:
```bash
bazel-bin/tensorflow_serving/model_servers/tensorflow_model_server
```
To test your installation, execute:
```bash
bazel test -c opt tensorflow_serving/...
```
## 2. impelement the serving
the files related the project such as training a model, building/saving/exporting a model, loading and exucting/testing the model, can be saved in "bazel-bin/tensorflow_serving/example/". When excuting them, we can pass parameters in the command line. for example, train and save a model (the trained model will be saved in "/tmp/mnist_model")
```bash
$ bazel build -c opt //tensorflow_serving/example:mnist_saved_model # no need to execute if you have Bazel build the entire tree. 
$ bazel-bin/tensorflow_serving/example/mnist_saved_model /tmp/mnist_model
Training model...

...

Done training!
Exporting trained model to /tmp/mnist_model
Done exporting!
```
recall that the Serving related file is stored in the directory "bazel-bin/tensorflow_serving/model_servers/". To open a port and start the TFserving for some specific model, we can use
```bash
$ bazel build -c opt //tensorflow_serving/model_servers:tensorflow_model_server # no need to execute if you have Bazel build the entire tree. 
$ bazel-bin/tensorflow_serving/model_servers/tensorflow_model_server --port=9000 --model_name=mnist --model_base_path=/tmp/mnist_model/
``` 
we can then open another terminal to test the severing, namely load the model from serving and test it
```bash
$ bazel build -c opt //tensorflow_serving/example:mnist_client # no need to execute if you have Bazel build the entire tree. 
$ bazel-bin/tensorflow_serving/example/mnist_client --num_tests=1000 --server=localhost:9000
...
Inference error rate: 10.5%
```






















