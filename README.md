# Direct insertion of NASA Airborne Snow Observatory-derived snow depth time-series into the iSnobal energy balance snow model
## Water Resources Research

Andrew Hedrick<sup>1,2</sup>, Danny Marks<sup>1</sup>, Scott Havens<sup>1</sup>, Mark Robertson<sup>1</sup>, Micah Johnson<sup>1</sup>, Micah Sandusky<sup>1</sup>, Hans-Peter Marshall<sup>2</sup>, Patrick Kormos<sup>3</sup>, Kat Bormann<sup>4</sup>, and Thomas H. Painter<sup>4</sup>

<sup>1</sup>USDA-ARS Northwest Watershed Research Center, Boise, Idaho, USA.

<sup>2</sup>Department of Geosciences, Boise State University, Boise, Idaho, USA.

<sup>3</sup>Colorado Basin River Forecast Center, National Weather Service, Salt Lake City, Utah, USA.

<sup>4</sup>Jet Propulsion Laboratory/California Institute of Technology, Pasadena, California, USA.

Corresponding author: Andrew Hedrick (andrew.hedrick@ars.usda.gov) 

## Contents

`/data/`

`/code/ipw`

`/code/smrf`

`/code/awsm`

## Running with Docker

To mount a data volume, so that you can share data between the local filesystem and the docker, the `-v` option must be used. 
For a more in depth dicussion and tutorial, read https://docs.docker.com/engine/userguide/containers/dockervolumes/. The container
has a shared data volume at `/data` where the container can access the local filesystem.

When the image is ran, it will go into the Python terminal within the image. Within this terminal, AWSM can be imported. The
command `/bin/bash` can be appended to the end of docker run to enter into the docker terminal for full control. It will start
in the `/data` location with SMRF code in `/code/smrf` and AWSM code in `/code/awsm`.

For Linux
`docker run -v <path>:/data -it usdaaranwrc/wrr_2018_hedrick`

For MacOSX:
`docker run -v /Users/<path>:/data -it usdaaranwrc/wrr_2018_hedrick`

For Windows:
`docker run -v /c/Users/<path>:/data -it usdaaranwrc/wrr_2018_hedrick`



