Each user need to build the docker image by themselves, see https://vsupalov.com/docker-shared-permissions/

Please replace repo, tag, xxx with your own values

to build docker image:

```docker build - < Dockerfile -t repo:tag --build-arg USER_ID=$(id -u) --build-arg GROUP_ID=$(id -g)```

to run docker container:

```docker run --gpus all --rm -itd --name xxx -v $(pwd):/workspace/ repo:tag bash```

to attach to docker container:

```docker attach xxx```

if too slow, try adding

```RUN export PIP_DEFAULT_TIMEOUT=100```

I added this to Dockerfile to accelerate pip install:

```-i https://pypi.tuna.tsinghua.edu.cn/simple```

This image has no cuda and cudnn installed outside pip, therefore tensorflow will not be able to use gpu, but jax and torch will be able to use gpu. Since I only use tensorboard in tensorflow, I don't need gpu for tensorflow.
