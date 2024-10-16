FROM ubuntu:24.04

WORKDIR /tmp/

RUN apt-get -y update && apt-get -y upgrade
RUN apt-get -y install wget zlib1g htop iotop python3-pip python3-wheel python3-setuptools python-is-python3 git

# Allow installing stuff to system Python.
RUN rm -f /usr/lib/python3.12/EXTERNALLY-MANAGED

RUN wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2404/x86_64/cuda-keyring_1.1-1_all.deb \
    && dpkg -i cuda-keyring_1.1-1_all.deb \
    && apt-get -y update \
    && apt-get -y install cuda-toolkit-12-6 cudnn9-cuda-12 

RUN pip3 install --no-cache-dir torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu124 

RUN pip3 install --no-cache-dir torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu124 
RUN pip3 install --no-cache-dir transformers evaluate datasets gradio accelerate bitsandbytes huggingface_hub librosa git-lfs ffmpeg jiwer pillow
RUN pip3 install --no-cache-dir jupyterlab ipykernel
RUN apt-get clean && rm -rf /tmp/*

CMD ["bash"]