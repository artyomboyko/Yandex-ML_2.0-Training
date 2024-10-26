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

# Позволяет устанавливать пакеты в системный Python.
RUN rm -f /usr/lib/python3.12/EXTERNALLY-MANAGED

# Пакеты необходимые для нормальной работы Jupyter Notebooks в VS Code
RUN pip3 install --no-cache-dir ipykernel ipython ipywidgets 

# Установка ML пакетов и других вспомогательных пакетов  
RUN pip3 install --no-cache-dir matplotlib nltk bokeh umap-learn tqdm 

# Установка Pytorch
RUN pip3 install --no-cache-dir torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu124 

# Установка Transformers
RUN pip3 install --no-cache-dir transformers evaluate datasets gradio accelerate bitsandbytes huggingface_hub librosa git-lfs ffmpeg jiwer pillow tensorboard transformers[agents]

# Очистка образа от мусора
RUN rm -rf /tmp/*

CMD ["bash"]