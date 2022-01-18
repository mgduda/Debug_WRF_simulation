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

Version 4.3.x: [WPS](https://www2.mmm.ucar.edu/people/duda/files/debug/WPS_v4.3.tar.gz)
    [WRF](https://www2.mmm.ucar.edu/people/duda/files/debug/WRF_v4.3.tar.gz)

After downloading a basic configuration, you can unpack the tar file *within
your `WPS` or `WRF/run` directory* before trying to run the WPS programs or the
WRF model. It's critically important to verify that the basic configuration runs
successfully on your system using just a single processor -- without verifying
this, you won't have a known-working configuration to begin with!

Once you have a working basic configuration, the suggested sequence of steps
to work towards your configuration (which is not working) is as follows. Each
of the steps in the outline below is a link to more detailed information about
that step.

### Incremental configuration changes
- Adjust the coarse horizontal domain so that it matches your configuration
- Adjust the vertical grid so that it matches your configuration
- Try with more than on MPI task
- Add the first nested domain (if nested domains are being used)
- Change physics suite / schemes to match
- Activate model option one at a time (e.g., adaptive timestep, DFI, etc.)

