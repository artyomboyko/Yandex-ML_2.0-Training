FROM ubuntu:24.04

# Установка переменных окружения
## Отключаем предупреждение о том, что pip используется от имени root
ENV PIP_ROOT_USER_ACTION=ignore 

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
COPY base_requirements.txt ml_requirements.txt pytorch_requirements.txt transformers_requirements.txt ./

# Установка пакетов базовых зависимостей и других вспомогательный пакетов. 
RUN pip3 install --no-cache-dir -r base_requirements.txt

# Установка ML пакетов.  
RUN pip3 install --no-cache-dir -r ml_requirements.txt

# Установка Pytorch.
RUN pip3 install --no-cache-dir -r pytorch_requirements.txt

# Установка Transformers
RUN pip3 install --no-cache-dir -r transformers_requirements.txt

# Очистка образа от мусора
RUN rm -rf /tmp/*

CMD ["bash"]