# Direct insertion of NASA Airborne Snow Observatory-derived snow depth time-series into the _iSnobal_ energy balance snow model

[![GitHub version](https://badge.fury.io/gh/USDA-ARS-NWRC%2FWRR_2018_Hedrick.svg)](https://badge.fury.io/gh/USDA-ARS-NWRC%2FWRR_2018_Hedrick)
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.1343647.svg)](https://doi.org/10.5281/zenodo.1343647)
[![Docker Automated build](https://img.shields.io/docker/automated/usdaarsnwrc/smrf.svg)](https://hub.docker.com/r/usdaarsnwrc/wrr_2018_hedrick/)

## Water Resources Research

Andrew Hedrick@#, Danny Marks@, Scott Havens@, Mark Robertson@, Micah Johnson@, Micah Sandusky@, Hans-Peter Marshall#, Patrick Kormos^, Kat J. Bormann*, and Thomas H. Painter*

@ USDA-ARS Northwest Watershed Research Center, Boise, Idaho, USA. \
\# Department of Geosciences, Boise State University, Boise, Idaho, USA. \
^ Colorado Basin River Forecast Center, National Weather Service, Salt Lake City, Utah, USA. \
\* Jet Propulsion Laboratory/California Institute of Technology, Pasadena, California, USA. 

Corresponding author: Andrew Hedrick (andrew.hedrick@ars.usda.gov)

## Background / Considerations

This Docker image contains all the necessary software for reproducing the model results presented in the above titled scientific manuscript. This application of the _iSnobal_ snow model (__Marks et al., 1999__) produces daily estimates of 19 snowpack parameters over the Tuolumne River Basin in California. In addition, this software produces all 10 of the 50-meter resolution hourly forcing grids required as input to the snow model. These forcing grids are in netCDF format and take up a considerable amount of disk space. Each variable file is approximately 65GB for an entire year and subsequently, all forcing grids for each year take up around 650GB on the local filesystem where the `/data/` directory is mounted. It is suggested that the user mount the `/data/` directory directly onto an external hard drive or server system with at least 3TB of available storage.

In addition to the software contained in this Docker image, any person seeking to reproduce the manuscript results would need to download the data and configuration scripts located at https://doi.org/10.5281/zenodo.1228399. This dataset contains: 

1. the hourly meteorological measurements from the weather stations in vector format (.csv files),
2. the configuration files for executing the AWSM automated protocol,
3. the static 50-meter grids for the Tuolumne Basin,
4. the ASO 50-meter snow depth products for all 36 updates presented in the manuscript,
5. and the shell scripts for restarting _iSnobal_ with each updated initialization file.

The initial model run does not contain any updates from the Airborne Snow Observatory snow depths. These updates must be manually initiated in the command line. Outputs from the updating shell scripts will be placed in the `/data/` directory alongside the non-updated results.

## Contents

`/data/` This is the directory that should be mounted to your computer's local filesystem. All model outputs are directed into this folder.

`/code/ipw` This directory contains the compiled source code for the Image Processing Workbench (IPW), which houses the iSnobal model and other associated programs.

`/code/smrf` This directory holds the Spatial Modeling for Resources Framework (SMRF) described in detail by __Havens et al., 2017__. SMRF is responsible for distributing the point meteorological data over the modeling domain in order to create the hourly forcing grids required by _iSnobal_.

`/code/awsm` Within this directory is the Automated Water Supply Model (AWSM), which automates the previously ad hoc process for running SMRF and _iSnobal_.

## Running with Docker

To mount a data volume, so that you can share data between the local filesystem and the docker, the `-v` option must be used.
For a more in-depth dicussion and tutorial, read https://docs.docker.com/storage/volumes/. The container
has a shared data volume at `/data` where the container can access the local filesystem.

When the image is run, it will go into the Python terminal within the image. Within this terminal, AWSM can be imported. The
command `/bin/bash` can be appended to the end of `docker run` command to enter into the docker terminal for full control. It will start
in the `/data` location with IPW code in `/code/ipw`, SMRF code in `/code/smrf`, and AWSM code in `/code/awsm`.

For Linux
`docker run -v <path>:/data -it usdaaranwrc/wrr_2018_hedrick`

For MacOSX:
`docker run -v /Users/<path>:/data -it usdaaranwrc/wrr_2018_hedrick`

For Windows:
`docker run -v /c/Users/<path>:/data -it usdaaranwrc/wrr_2018_hedrick`

## References

Hedrick, A. R., Marks, D., Havens, S., Robertson, M., Johnson, M., Sandusky, M., Marshall, H.-P., Kormos, P. R., Bormann, K. J., & Painter, T. H. (2018). Direct insertion of NASA Airborne Snow Observatory-derived snow depth time-series into the iSnobal energy balance snow model. _submitted to Water Resources Research_.

Havens, S., Marks, D., Kormos, P., & Hedrick, A. (2017). Spatial Modeling for Resources Framework (SMRF): A modular framework for developing spatial forcing data for snow modeling in mountain basins. _Computers & Geosciences_, 109(September 2016), 295–304. https://doi.org/10.1016/j.cageo.2017.08.016

Marks, D., Domingo, J., Susong, D., Link, T. E., & Garen, D. C. (1999). A spatially distributed energy balance snowmelt model for application in mountain basins. _Hydrological Processes_, 13(12–13), 1935–1959. https://doi.org/10.1002/(SICI)1099-1085(199909)13:12/13<1935::AID-HYP868>3.0.CO;2-C
