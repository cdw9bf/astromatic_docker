# Docker Images for Astromatic Tools 

Contained in this repo are the images needed to build a working docker container with the Astromatic tools (scamp, swarp, sextractor). The container `AstromaticTools` contains all three binaries as well as Opencv4 for python, astropy, and jupyter notebook. 


## Building the Containers
The build order goes `ubuntubase` -> `opencv4base` -> `AstromaticTools`. If you don't desire opencv4, you will still need to install ATLAS and FFTW from that container.

To build the docker containers,

```bash
docker build -f base_images/UbuntuBase -t ubuntubase .
docker build -f base_images/OpenCv4Base -t opencv4base . 

docker build -f AstromaticTools -t astromatictools . 
```

## Running the container 

To start the container in headless mode, run:
```bash
docker run -p 8888:8888 -d astromatictools
```
This runs the container locally and binds your local port `8888` to the container's port `8888` which is served by the juptyer notebook. To get into the container, go to `http://localhost:8888` in your browser. 

The password is `password`. Follow [this guide](https://jupyter-notebook.readthedocs.io/en/stable/public_server.html#preparing-a-hashed-password) for instructions on how to create a new hashed password. 

## Motivation
I noticed a while back that it was a bit difficult to compile these tools correctly on a modern linux machine. The code may compile but Scamp would have constant segment faults unless you use an older version of GCC. 
There's not much documentation online as to why this happens, nor am I good enough at C++ to know why this was happening. I only know that it doesn't happen when compiled with an older version. 


Hopefully others will be spared my same headache. 


# Astromatic
Here is their [github](https://github.com/astromatic) link where the project is being maintained nowadays. 

