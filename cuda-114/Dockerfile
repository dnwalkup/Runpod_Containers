## Dockerfile

ARG BASE_IMAGE=nvidia/cuda:11.4.2-cudnn8-devel-ubuntu20.04

FROM ${BASE_IMAGE} as dev-base

SHELL ["/bin/bash", "-o", "pipefail", "-c"]
ENV DEBIAN_FRONTEND noninteractive\
    SHELL=/bin/bash
RUN apt-key del 7fa2af80
RUN apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/3bf863cc.pub
RUN apt-get update --yes && \
    # - apt-get upgrade is run to patch known vulnerabilities in apt-get packages as
    #   the ubuntu base image is rebuilt too seldom sometimes (less than once a month)
    apt-get upgrade --yes && \
    apt install --yes --no-install-recommends\
    wget\
    bash\
    openssh-server &&\
    apt-get clean && rm -rf /var/lib/apt/lists/* && \
    echo "en_US.UTF-8 UTF-8" > /etc/locale.gen
RUN apt-get update
RUN apt-get -y install software-properties-common gcc
RUN add-apt-repository -y ppa:deadsnakes/ppa
RUN apt-get update
RUN apt-get -y install python3
RUN apt-get -y install python3-pip
RUN apt-get -y install python3-distutils
RUN apt-get -y install python3-apt
RUN apt -y install rename
RUN apt-get -y install zip unzip
RUN pip3 install jupyterlab
RUN pip3 install ipywidgets
RUN pip3 install pycuda
RUN pip3 install ipython
RUN pip3 install Pillow
RUN pip3 install triton
RUN pip3 install transformers
RUN pip3 install tensorboard
RUN pip3 install OmegaConf
RUN pip3 install tqdm
RUN pip3 install ftfy
RUN pip3 install wget
RUN pip3 install -U --no-cache-dir gdown

ADD start.sh /

RUN chmod +x /start.sh

CMD [ "/start.sh" ]