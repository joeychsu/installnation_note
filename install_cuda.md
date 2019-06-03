# Install Nvidia CUDA-9.0 on Ubuntu 16.04 for Deep Learning
* The latest version of CUDA is 9.1. However some deep learning frameworks are not yet ready for CUDA 9.1. The installation script of CUDA-9.1 is very similar to this one.
* OS: Ubuntu 16.04 x86_64
*	(Optional) Uninstall old version CUDA Toolkit such as:
```
sudo apt-get purge cuda
sudo apt-get purge libcudnn6
sudo apt-get purge libcudnn6-dev
```
*	Install CUDA Toolkit 9.0 and cuDNN 7.0 as follows:
```
wget http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/cuda-repo-ubuntu1604_9.0.176-1_amd64.deb
wget http://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1604/x86_64/libcudnn7_7.0.5.15-1+cuda9.0_amd64.deb
wget http://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1604/x86_64/libcudnn7-dev_7.0.5.15-1+cuda9.0_amd64.deb
wget http://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1604/x86_64/libnccl2_2.1.4-1+cuda9.0_amd64.deb
wget http://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1604/x86_64/libnccl-dev_2.1.4-1+cuda9.0_amd64.deb
sudo dpkg -i cuda-repo-ubuntu1604_9.0.176-1_amd64.deb
sudo dpkg -i libcudnn7_7.0.5.15-1+cuda9.0_amd64.deb
sudo dpkg -i libcudnn7-dev_7.0.5.15-1+cuda9.0_amd64.deb
sudo dpkg -i libnccl2_2.1.4-1+cuda9.0_amd64.deb
sudo dpkg -i libnccl-dev_2.1.4-1+cuda9.0_amd64.deb
sudo apt-get update
sudo apt-get install cuda=9.0.176-1
sudo apt-get install libcudnn7-dev
sudo apt-get install libnccl-dev
```
*	Reboot the system to load the NVIDIA drivers.
*	Set up the development environment by modifying the PATH and LD_LIBRARY_PATHvariables, also add them to the end of .bashrc file:
```
export PATH=/usr/local/cuda-9.0/bin${PATH:+:${PATH}}
export LD_LIBRARY_PATH=/usr/local/cuda-9.0/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
```
* 如果在 Ubuntu 14 想安裝 cuda 10 可參考 : 
```
wget http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1404/x86_64/cuda-repo-ubuntu1404_10.0.130-1_amd64.deb
wget http://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1404/x86_64/libcudnn7_7.4.1.5-1+cuda10.0_amd64.deb
wget http://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1404/x86_64/libcudnn7-dev_7.4.1.5-1+cuda10.0_amd64.deb
wget http://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1404/x86_64/libnccl2_2.3.5-2+cuda10.0_amd64.deb
wget http://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1404/x86_64/libnccl-dev_2.3.5-2+cuda10.0_amd64.deb
sudo dpkg -i cuda-repo-ubuntu1404_10.0.130-1_amd64.deb
sudo dpkg -i libcudnn7_7.4.1.5-1+cuda10.0_amd64.deb
sudo dpkg -i libcudnn7-dev_7.4.1.5-1+cuda10.0_amd64.deb
sudo dpkg -i libnccl2_2.3.5-2+cuda10.0_amd64.deb
sudo dpkg -i libnccl-dev_2.3.5-2+cuda10.0_amd64.deb
sudo apt-get update
sudo apt-get install cuda=10.0.130-1
sudo apt-get install libcudnn7-dev
sudo apt-get install libnccl-dev
```
* 各 lib 要求的版本沒有硬性要求，只要結尾都是 cuda10.0_amd64.deb

## 參考資料 : 
1. https://yangcha.github.io/CUDA90/
2. nvidia-driver 安裝 / 更新 : https://gist.github.com/wangruohui/df039f0dc434d6486f5d4d098aa52d07#install-nvidia-graphics-driver-via-apt-get

