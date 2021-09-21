# Docker Projects

This repo offers a series of useful images, including:

Images running Jupyter Lab:

- __base-jupyter__: this is the base image from which I create all other __-jupyter__ images. It comes with a number of libraries installed that you can check [here](https://github.com/ItsmeKernel/docker/blob/main/base-jupyter/requirements.txt).
- __tensorflow-jupyter__: extends the __base-jupyter__ image and installs tensorflow on top.

Note that these images serve the content of the volume mounted under _/notebooks/_, allowing you to work seamlessly with notebooks in your local file system.

You can run any of this container by executing something along these lines:
```
docker run --name ds-jupyterlab -p 8888:8888 -v /path/to/my/notebooks:/notebooks/ -it augusto1982/base-jupyter
```
