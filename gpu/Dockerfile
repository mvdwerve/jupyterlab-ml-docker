# base it on the latest 9.1-cudnn7 image
FROM nvidia/cuda:9.1-cudnn7-runtime-ubuntu16.04
MAINTAINER Michael van der Werve <mvdwerve@outlook.com>

### 
# COPIED FROM MINICONDA DOCKERFILE
###
ENV LANG=C.UTF-8 LC_ALL=C.UTF-8
ENV PATH /opt/conda/bin:$PATH

RUN apt-get update --fix-missing && \
    apt-get install -y wget bzip2 ca-certificates curl git && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN wget --quiet https://repo.anaconda.com/miniconda/Miniconda3-4.5.4-Linux-x86_64.sh -O ~/miniconda.sh && \
    /bin/bash ~/miniconda.sh -b -p /opt/conda && \
    rm ~/miniconda.sh && \
    /opt/conda/bin/conda clean -tipsy && \
    ln -s /opt/conda/etc/profile.d/conda.sh /etc/profile.d/conda.sh && \
    echo ". /opt/conda/etc/profile.d/conda.sh" >> ~/.bashrc && \
    echo "conda activate base" >> ~/.bashrc

ENV TINI_VERSION v0.16.1
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /usr/bin/tini
RUN chmod +x /usr/bin/tini
###
# END OF COPY FROM MINICONDA3 DOCKERFILE
###

# default packages
RUN conda install --yes \
	nodejs \
        matplotlib \
        opencv \
        pandas \
        scipy \
        scikit-learn \
        numpy \
        jupyterlab \
        ipywidgets \
        tqdm 

# install torchvision and cuda for pytorch from the pytorch channel
RUN conda install pytorch torchvision cuda91 -c pytorch

# install the widget lab extension for tqdm
RUN jupyter labextension install @jupyter-widgets/jupyterlab-manager

# jupyterlab port
EXPOSE 8888

# expose default working directory 
VOLUME ["/project"]
WORKDIR /project

CMD jupyter-lab --allow-root --ip=0.0.0.0 --no-browser --NotebookApp.token="" 
