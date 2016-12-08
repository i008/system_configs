#### FILES NEEDED:
- cuda_8.0.27_linux
- NVIDIA-Linux-x86_64-367.27




#### Downgradin gcc 5++ to 4.9++

```bash
sudo su -
apt-get install build-essential
add-apt-repository ppa:ubuntu-toolchain-r/test
apt-get update
apt-get install gcc-4.9 g++-4.9 cpp-4.9
cd /usr/bin
rm gcc g++ cpp
ln -s gcc-4.9 gcc
ln -s g++-4.9 g++
ln -s cpp-4.9 cpp
```


#### STEPS:
- Download cuda-8.run file
- Download Nvidia-367.18-driver.run file
- Remove old drivers (apt remove --purge nvidia*)
- Remove old nvidia.deb packages (just in case that's necessary?)
- Remove cuda folders (/usr/local/cuda*) 
- reboot
- run the cuda-8.run file. Decline on installing the old drivers (362?)
- reboot
- sudo bash NVIDIA-Linux-x86_64-367.27.run --no-x-check
- reboot




Maybe needed:

```bash
if [ -z $LD_LIBRARY_PATH ]; then
  LD_LIBRARY_PATH=/usr/local/cuda-8.0/lib64:/usr/local/cuda-8.0/lib
else
  LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda-8.0/lib64:/usr/local/cuda-8.0/lib
fi
export LD_LIBRARY_PATH
```


#### Theano config

```
CONFIG THEANO: ~/.theanorc

[global]
floatX = float32
device = gpu0

[lib]
cnmem = 0.7

[cuda]
root = /usr/local/cuda-8.0


```


#### Instal CuDNN for (CUDA 8+)
https://developer.nvidia.com/rdp/cudnn-download
cuDNN v5.1 Library for Linux
```bash
aws s3 cp s3://i008/cudnn-8.0-linux-x64-v5.1.tgz . 
tar -zxf cudnn-8.0-linux-x64-v5.1.tgz 
cd cuda  
sudo cp lib64/* /usr/local/cuda/lib64/
sudo cp include/* /usr/local/cuda/include/
```
Test cuDNN installation:
```python
import theano
theano.sandbox.cuda.dnn.version() #shouldnt throw any exceptions
```



THEANO DEPS:
```bash
sudo apt-get install python-numpy python-scipy python-dev python-pip python-nose g++ libopenblas-dev git
```


