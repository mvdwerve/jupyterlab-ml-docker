# jupyterlab-ml-docker
Base docker images for CPU and GPU learning.

## Versions
- `cpu`
- `gpu`

## Running GPU version
```
docker run --runtime=nvidia --shm-size 8G --rm -it -p 8888:8888 -v `pwd`:/project -e NVIDIA_VISIBLE_DEVICES=all mvdwerve/jupyterlab-ml:gpu
```

## Running CPU version
```
docker run --sh-size 8G --rm -it -p 8888:8888 -v `pwd`:/project mvdwerve/jupyterlab-ml:cpu
```
