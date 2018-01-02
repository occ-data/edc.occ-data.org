+++
description = "How to get NWM data from the OCC Environmental Data Commons"
title = "Get Data"
date = "2018-01-01T12:00:00+00:00"
draft = false
weight = 1
toc = true
bref = ""
+++

### Best Effort
The data are being made available on a best effort basis by all parties involved. There are no guarantees the data will be available when you really need it.

### National Water Model Retrospective Version 1.0

* 24 Year retrospective simulation (Jan 1 1993 - Sept 30 2016)
* A reanalysis rather than a reforecast (forcing different than real-time runs)
* Output fields are fewer and less frequent than real-time to conserve space
* Provides historical context to current conditions
* Can be used to infer flow frequencies and perform temporal analyses
* 32 Tb in size, with hourly streamflow output and 3-hourly land surface output

#### Reanalsys Technical Details

* Forced with [NLDAS](http://www.emc.ncep.noaa.gov/mmb/nldas/) and [NARR](https://www.esrl.noaa.gov/psd/data/gridded/data.narr.html)
* 1992 used as a warmup period so the data in 1993 is good.
* 1-km raster, 250-m raster, and vector data.
* Uses the NHDPlus flow lines, lakes, and reservoirs.

### File Formats
The data is being made available in a NetCDF file format. The data are a combination of raster in a projected format and vector data that must be referenced with associated geographical information located in other files.

### Products Available & Name Conventions

There are several files which contain various output products for each time step. They are detailed below. The files are compressed with the zip format to reduce filesize.



| Product Name | File Description | Time Between Files | Example File Name |
| ------------- | :----------: | :----------------: | :-------: |
| CHRT | Streamflow values at points associated with flow lines | 1-hour | 201409090000.CHRTOUT_DOMAIN1.zip |
| LAKE | Output values at points associated with lakes & reservoirs | 1-hour | 201409090000.LAKEOUT_DOMAIN1.zip |
| LDAS | Land surface model output including radiation, ET, snow, etc.  at 1-km resolution | 3-hourly | 201409090000.LDASOUT_DOMAIN1.zip |
| RT | Ponded water depth and depth to soil saturation at 250-m resolution | 3-hourly | 201409090000.RTOUT_DOMAIN1.zip |


The filenames are

    <year><month><day><hour>00.<product>OUT_DOMAIN1.zip

### Archive Data Access

Data access is provided via a S3-API compatible service. The files may be downloaded with the aws cli, boto, or through a web browser.

[https://griffin-objstore.opensciencedatacloud.org/nwm-archive/](https://griffin-objstore.opensciencedatacloud.org/nwm-archive/)

This endpoint is S3-api compatible, so when you visit in your browser it will return XML with a truncated list of files available to download.

We recommend using the [awscli](https://aws.amazon.com/cli/) or the [python boto library](https://github.com/boto/boto) to access the data. An example awscli command to list the contents of the bucket would look like:
```
aws s3 ls s3://nwm-archive/ --no-sign-request --endpoint-url https://griffin-objstore.opensciencedatacloud.org --no-verify-ssl
```

### Real-time Data Access

If you could like to access a real-time data feed of forecasts from the National Water Model that data is available from NOAA at the following location.

[ftp://ftpprd.ncep.noaa.gov/pub/data/nccf/com/nwm/prod/](ftp://ftpprd.ncep.noaa.gov/pub/data/nccf/com/nwm/prod/)

