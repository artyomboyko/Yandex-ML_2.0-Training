FROM ubuntu:24.04

WORKDIR /tmp/

# Обновление системы, установка Python и полезных утилит
RUN apt-get -y update && apt-get -y upgrade
RUN apt-get -y install wget zlib1g htop iotop python3-pip python3-wheel python3-setuptools python-is-python3 git

# Установка NVIDIA CUDA Toolkit Toolkit 12.6 Update 2
RUN wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2404/x86_64/cuda-keyring_1.1-1_all.deb \
    && dpkg -i cuda-keyring_1.1-1_all.deb \
    && apt-get -y update \
    && apt-get -y install cuda-toolkit-12-6 cudnn9-cuda-12

# Очистка кеша apt
RUN apt-get clean

# Отключаем внешнее урпавление системными пакетами Python.
RUN rm -f /usr/lib/python3.12/EXTERNALLY-MANAGED

WORKDIR /tmp/
COPY ipy_requirements.txt ml_requirements.txt pytorch_requirements.txt ./

# Установка пакетов необходимых для Jupyter Notebooks и других вспомогательный пакетов 
RUN pip3 install --no-cache-dir -r ipy_requirements.txt

# Установка ML пакетов  
RUN pip3 install --no-cache-dir -r ml_requirements.txt

# Установка Pytorch
RUN pip3 install --no-cache-dir -r pytorch_requirements.txt

# Установка Transformers
RUN pip3 install --no-cache-dir transformers==4.46.1 evaluate==0.4.3 datasets==3.1.0 gradio==5.4.0 gradio_client==1.4.2 accelerate==1.1.0 bitsandbytes==0.44.1 huggingface_hub==0.26.2 librosa==0.10.2.post1 git-lfs==1.6 ffmpeg==1.4 jiwer pillow tensorboard transformers[agents]

# Очистка образа от мусора
RUN rm -rf /tmp/*

CMD ["bash"]