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

COPY ipy_requirements.txt /tmp/ipy_requirements.txt
WORKDIR /tmp/

# Пакеты необходимые для нормальной работы Jupyter Notebooks в VS Code
RUN pip3 install --no-cache-dir -r ipy_requirements.txt

# Установка ML пакетов и других вспомогательных пакетов  
RUN pip3 install --no-cache-dir matplotlib==3.9.2 nltk==3.9.1 bokeh==3.6.0 umap-learn==0.5.7 tqdm==4.66.6 Unidecode==1.3.8

# Установка Pytorch
RUN pip3 install --no-cache-dir torch torchvision==0.20.1+cu124 torchaudio==2.5.1+cu124 --index-url https://download.pytorch.org/whl/cu124 
RUN pip3 install --no-cache-dir torch_tb_profiler

# Установка Transformers
RUN pip3 install --no-cache-dir transformers==4.46.1 evaluate==0.4.3 datasets==3.1.0 gradio==5.4.0 gradio_client==1.4.2 accelerate==1.1.0 bitsandbytes==0.44.1 huggingface_hub==0.26.2 librosa==0.10.2.post1 git-lfs==1.6 ffmpeg==1.4 jiwer pillow tensorboard transformers[agents]

# Очистка образа от мусора
RUN rm -rf /tmp/*

CMD ["bash"]