This repository contains a Dockerfile to create a Docker image for solving linear programming optimization problems in R. The Docker image is available via [Docker Hub](https://hub.docker.com/r/mstrimas/optimizr/).

Containers created based on this image will have R, R Studio, the Hadleyverse of R packages, and a suite of linear programming solvers. This image includes all the open source linear programming solvers, and their R package interfaces, listed in [CRAN Task View for Optimization](https://cran.r-project.org/web/views/Optimization.html#MathematicalProgrammingSolvers):

- [lp_solve](http://lpsolve.sourceforge.net/5.5/) with R packages [lpSolve](https://cran.r-project.org/web/packages/lpSolve/index.html) and [lpSolveAPI](https://cran.r-project.org/web/packages/lpSolveAPI/index.html).
- [COIN-OR Symphony](https://projects.coin-or.org/SYMPHONY) with R packages [Rsymphony](https://cran.r-project.org/web/packages/Rsymphony/index.html), from CRAN, and [lpsymphony](https://www.bioconductor.org/packages/3.3/bioc/html/lpsymphony.html), from Bioconductor.
- [COIN-OR Clp](http://projects.coin-or.org/Clp) with R package [clpAPI](https://cran.r-project.org/web/packages/clpAPI/index.html).
- The [GNU Linear Programming Kit](http://www.gnu.org/software/glpk/) with R packages [glpkAPI](https://cran.r-project.org/web/packages/glpkAPI/index.html) and [Rglpk](https://cran.r-project.org/web/packages/Rglpk/index.html).
- [Gurobi](http://www.gurobi.com/) and it's corresponding R package. This is the only commercial solver in the list and, if you intend on using it, you'll need to provide a license file. Further details below.

# Use

## Install Docker

To use these images, start by installing Docker by following the instructions on the Docker website for [Linux](https://docs.docker.com/linux/step_one/), [Mac](https://docs.docker.com/mac/step_one/), or [Windows](https://docs.docker.com/windows/step_one/).

If you're on Mac or Windows, this will the *Docker Quickstart Terminal*, which is a Linux virtual machine that Docker runs in. Open this application or, if you're on Linux, just open a normal Terminal.

## Start container

To start a container based on the `optimizr` image use:

```
docker run -dp 8787:8787 mstrimas/optimizr
```

Now point your browser to the IP address given by `docker-machine ip`, being sure to append this address with `:8787`. For example, if `docker-machine ip` returns `192.168.99.100`, point your browser to `192.168.99.100:8787`. To log in to RStudio use `rstudio` for the username and password. You're now using RStudio running in the Docker container, which gives you access to all the linear programming solvers listed above.

## Gurobi license

[Gurobi](http://www.gurobi.com/) is an extremely powerful commercial solver for linear and quadratic programming. It is significantly faster than existing open source solvers, however, you'll need a license to use it. Fortunately, Gurobi does offer free academic licenses for those eligible. Note that a Gurobi license is only good for a single machine and therefore you'll need a new one for every Docker container you create. So, if you do go to the trouble of setting up Gurobi on a Docker container, you'll probably want to keep that container around to avoid having to get a new license.

To get a license, follow the instructions on the [Gurobi website](http://www.gurobi.com/downloads/download-center). Now, look at your [current licenses](https://user.gurobi.com/download/licenses/current) and you'll see a `grbgetkey` command listed like:

```
grbgetkey 19b2902a-XXXX-XXXX-XXXX-XXXXXXXXXXXX
```

This command needs to be run in the container to install the license. After you've started an `optimizr` container, get its container ID using `docker ps`, then run the `grbgetkey` command with:

```
docker exec <container id> grbgetkey 19b2902a-XXXX-XXXX-XXXX-XXXXXXXXXXXX
```

You should now be able to use the `gurobi` R package in the Docker container.
