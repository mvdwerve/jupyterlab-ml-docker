# base it on a normal miniconda3 install
FROM continuumio/miniconda3
MAINTAINER Michael van der Werve <mvdwerve@outlook.com>

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

# install torch
RUN conda install pytorch-cpu torchvision-cpu -c pytorch

# install the widget lab extension for tqdm
RUN jupyter labextension install @jupyter-widgets/jupyterlab-manager

# jupyterlab point
EXPOSE 8888

# define that the normal directory is code
VOLUME ["/project"]
WORKDIR /project

# by default, start jupyterlab
CMD jupyter-lab --allow-root --ip=0.0.0.0 --no-browser --NotebookApp.token="" 
