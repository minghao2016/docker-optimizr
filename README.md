This repository contains Dockerfiles for Docker containers. Consult the subdirectories for descriptions of each container. 

The available Docker images are:

- `optimizr`: a Docker image for solving linear programming optimization problems in R. Contains R, R Studio, the Hadleyverse of packages, and a variety of R packages for solving linear programming optimization problems.
- `prioritizr`: a Docker image for systematic conservation prioritization. Builds on top of `optimizr`, but also contains additional packages for solving conservation prioritization problems using integer programming.

## Install Docker

To use these images, start by installing Docker by following the instructions on the Docker website for [Linux](https://docs.docker.com/linux/step_one/), [Mac](https://docs.docker.com/mac/step_one/), or [Windows](https://docs.docker.com/windows/step_one/).

If you're on Mac or Windows, this will the *Docker Quickstart Terminal*, which is a Linux virtual machine that Docker runs in. Open this application or, if you're on Linux, just open a normal Terminal.