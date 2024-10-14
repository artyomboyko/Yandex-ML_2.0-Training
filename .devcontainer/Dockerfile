FROM ubuntu:24.04
WORKDIR /tmp/
RUN wget https://developer.download.nvidia.com/compute/cuda/repos/wsl-ubuntu/x86_64/cuda-keyring_1.1-1_all.deb \
    dpkg -i cuda-keyring_1.1-1_all.deb \
    apt-get update -y && apt-get upgrade -y && apt-get -y install cuda-toolkit-12-6

RUN python -m pip install --upgrade pip
COPY requirements.txt /tmp
RUN pip install --no-cache-dir -r /tmp/requirements.txt

RUN pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu124