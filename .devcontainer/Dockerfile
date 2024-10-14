FROM ubuntu:24.04

WORKDIR /tmp/

RUN apt-get -y update && apt-get -y upgrade

RUN apt-get -y install wget zlib1g htop iotop python3-pip python3-wheel python3-setuptools python-is-python3 \
    jupyterlab ipykernel git

RUN wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2404/x86_64/cuda-keyring_1.1-1_all.deb \
    && dpkg -i cuda-keyring_1.1-1_all.deb \
    && apt-get -y update \
    && apt-get -y install cuda-toolkit-12-6 cudnn9-cuda-12 \

RUN python -m pip install --upgrade pip
RUN pip3 install --break-system-packages --no-cache-dir torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu124 
RUN pip3 install --break-system-packages --no-cache-dir transformers evaluate datasets gradio accelerate bitsandbytes huggingface_hub

RUN RUN apt-get clean && rm -rf /tmp/*

CMD bash