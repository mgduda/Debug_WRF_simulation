![WRF logo](/assets/images/wrf_logo.jpg)

# Tips for debugging a failed WRF simulation

This document is designed to aid in debugging a failed WRF simulation and
follows a typical workflow employed by staff in the Mesoscale and Microscale
Meteorology Lab at NCAR. The essential idea is to begin with a working
configuration of the model, and to incrementally change that configuration until
it fails in the same way as the original, failed simulation. In this way, it's
much easier to identify the specific cause for the failure.

Schematically, the process is shown in the cartoon, below.

![High-level debugging schematic](/assets/images/debug_overview.svg)

Here, "Basic configuration" is a well-tested configuration of the WPS and WRF
model.

## Basic configurations

Basic configurations of the WPS and WRF are provided for the last several
WRF/WPS releases in the links, below. If you happen to be working with an older
version of the WRF modeling system, we strongly encourage you to try reproducing
your setup with the current WRF/WPS releases.

| WRF Version | WPS download | WRF download |
| ----------- | ------------ | ------------ |
| 4.3.x       | [WPS](https://www2.mmm.ucar.edu/people/duda/files/debug/WPS_v4.3.tar.gz) | [WRF](https://www2.mmm.ucar.edu/people/duda/files/debug/WRF_v4.3.tar.gz) |
| 4.2.x       | [WPS](https://www2.mmm.ucar.edu/people/duda/files/debug/WPS_v4.2.tar.gz) | [WRF](https://www2.mmm.ucar.edu/people/duda/files/debug/WRF_v4.2.tar.gz)

In addition to the basic configurations for the WPS and WRF model, meteorological
data are needed by the WPS. The following links provide three time periods of GFS
0.25-degree data that have been verified to work well with the basic configuration:

[2022-01-01 00 UTC](https://www2.mmm.ucar.edu/people/duda/files/debug/gfs_2021010100.grib2)

[2022-01-01 03 UTC](https://www2.mmm.ucar.edu/people/duda/files/debug/gfs_2021010103.grib2)

[2022-01-01 06 UTC](https://www2.mmm.ucar.edu/people/duda/files/debug/gfs_2021010106.grib2)

After downloading a basic configuration, you can unpack the tar file *within
your `WPS` or `WRF/run` directory* before trying to run the WPS programs or the
WRF model. It's critically important to verify that the basic configuration runs
successfully on your system using just a single processor -- without verifying
this, you won't have a known-working configuration to begin with!

Once you have a working basic configuration, the suggested sequence of steps
to work towards your configuration (which is not working) is as follows. Each
of the steps in the outline below is a link to more detailed information about
that step.

## Plan for incremental changes to basic configuration

- [Adjust the horizontal domain so that it matches your configuration](#adjust-the-horizontal-domain)
- [Adjust the vertical grid so that it matches your configuration](#adjust-the-vertical-grid)
- [Try with more than on MPI task](#use-multiple-mpi-tasks)
- Add the first nested domain (if nested domains are being used)
- Change physics suite / schemes to match
- Activate model option one at a time (e.g., adaptive timestep, DFI, etc.)

### Adjust the horizontal domain

The idea here is to change only the geographic location, horizontal resolution, and
number of gridpoints in the single horizontal domain.

*Tip: If your simulation fails after changing the horizontal domain, you can then
try changing one aspect of the horizontal domain at a time: geographic location,
then resolution, and finally number of gridpoints.*

### Adjust the vertical grid

If you are using something other than the default vertical grid, you can rerun the real.exe
program after editing the namelist.input file to use the same vertical levels as in your
failed model setup.

### Use multiple MPI tasks

Try using more than one MPI task.

*Tip: If the model now fails when attempting to use the same number of MPI tasks as in
your failed model setup, try gradually increasing the number of MPI tasks.*

