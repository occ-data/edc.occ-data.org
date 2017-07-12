+++
description = "Using GDAL to Work with GOES-16 NetCDF Data"
title = "GDAL"
date = "2017-07-12T12:00:00+00:00"
draft = false
weight = 300
toc = true
bref = "This is an example of how to use GDAL to turn a NetCDF file into a png image"
+++

# GDAL Setup
The Geospatial Data Abstraction Library (GDAL; [gdal.org](http://www.gdal.org)) is a library and set of command line tools. GDAL supports reading the GOES-16 NetCDF files after a series of patches were recently upstreamed by the OCC team. The patches should be incorporated into GDAL version 2.2, and so for now GDAL must be built from source to work fully with the GOES-16 dataset.

# Using GDAL with Docker
The easiest way to get started with GDAL is to use the docker image built by OCC which includes the HDF5 & NetCDF libraries. This image builds GDAL from source so it is always the latest version. The dockerfile can be found on the [OCC GDAL container repo](https://github.com/occ-data/GDAL-Container).

In the directory with the GOES-16 data you want to work with:
```
docker run -d --rm -ti --name gdal -v $(pwd):/data quay.io/occ_data/gdal:latest
```
This command will pull the docker container from Quay, run the container naming it "gdal" for future commands, and mount the current working directory as /data inside the container.

To test that it is working we can run the `gdalinfo` command over a file. This command will tell us information about the file metadata.
```
docker exec -ti gdal gdalinfo OR_ABI-L1b-RadF-M3C02_G16_s20171921545382_e20171921556149_c20171921556183.nc
```
which returns:
```
Driver: netCDF/Network Common Data Format
Files: OR_ABI-L1b-RadF-M3C02_G16_s20171921545382_e20171921556149_c20171921556183.nc
Size is 512, 512
Coordinate System is `'
Metadata:
  NC_GLOBAL#cdm_data_type=Image
  NC_GLOBAL#Conventions=CF-1.7
  NC_GLOBAL#dataset_name=OR_ABI-L1b-RadF-M3C02_G16_s20171921545382_e20171921556149_c20171921556183.nc
  NC_GLOBAL#date_created=2017-07-11T15:56:18.3Z
  NC_GLOBAL#id=97e2d087-457b-4601-8a03-1bf0b0afa589
  NC_GLOBAL#institution=DOC/NOAA/NESDIS > U.S. Department of Commerce, National Oceanic and Atmospheric Administration, National Environmental Satellite, Data, and Information Services
  NC_GLOBAL#instrument_ID=FM1
  NC_GLOBAL#instrument_type=GOES R Series Advanced Baseline Imager
  NC_GLOBAL#iso_series_metadata_id=a70be540-c38b-11e0-962b-0800200c9a66
  NC_GLOBAL#keywords=SPECTRAL/ENGINEERING > VISIBLE WAVELENGTHS > VISIBLE RADIANCE
  NC_GLOBAL#keywords_vocabulary=NASA Global Change Master Directory (GCMD) Earth Science Keywords, Version 7.0.0.0.0
  NC_GLOBAL#license=Unclassified data.  Access is restricted to approved users only.
  NC_GLOBAL#Metadata_Conventions=Unidata Dataset Discovery v1.0
  NC_GLOBAL#naming_authority=gov.nesdis.noaa
  NC_GLOBAL#orbital_slot=GOES-Test
  NC_GLOBAL#platform_ID=G16
  NC_GLOBAL#processing_level=National Aeronautics and Space Administration (NASA) L1b
  NC_GLOBAL#production_data_source=Realtime
  NC_GLOBAL#production_environment=OE
  NC_GLOBAL#production_site=WCDAS
  NC_GLOBAL#project=GOES
  NC_GLOBAL#scene_id=Full Disk
  NC_GLOBAL#spatial_resolution=0.5km at nadir
  NC_GLOBAL#standard_name_vocabulary=CF Standard Name Table (v25, 05 July 2013)
  NC_GLOBAL#summary=Single reflective band ABI L1b Radiance Products are digital maps of outgoing radiance values at the top of the atmosphere for visible and near-IR bands.
  NC_GLOBAL#timeline_id=ABI Mode 3
  NC_GLOBAL#time_coverage_end=2017-07-11T15:56:14.9Z
  NC_GLOBAL#time_coverage_start=2017-07-11T15:45:38.2Z
  NC_GLOBAL#title=ABI L1b Radiances
Subdatasets:
  SUBDATASET_1_NAME=NETCDF:"OR_ABI-L1b-RadF-M3C02_G16_s20171921545382_e20171921556149_c20171921556183.nc":Rad
  SUBDATASET_1_DESC=[21696x21696] toa_outgoing_radiance_per_unit_wavelength (16-bit integer)
  SUBDATASET_2_NAME=NETCDF:"OR_ABI-L1b-RadF-M3C02_G16_s20171921545382_e20171921556149_c20171921556183.nc":DQF
  SUBDATASET_2_DESC=[21696x21696] status_flag (8-bit integer)
Corner Coordinates:
Upper Left  (    0.0,    0.0)
Lower Left  (    0.0,  512.0)
Upper Right (  512.0,    0.0)
Lower Right (  512.0,  512.0)
Center      (  256.0,  256.0)
```
The NetCDF files contain subdatasets, in this example `NETCDF:"OR_ABI-L1b-RadF-M3C02_G16_s20171921545382_e20171921556149_c20171921556183.nc":Rad` and `NETCDF:"OR_ABI-L1b-RadF-M3C02_G16_s20171921545382_e20171921556149_c20171921556183.nc":DQF`. These strings can be used as input into GDAL to refer to the specific subsets.


## Unscaling and Converting to PNG
To create a png image which we can view we should first extract the subdataset we are interested in and unscale the data values. The `gdal_translate` program is what we will use for this step. It can extract the dataset and do the unscaling in a single step. The NetCDF files for GOES-16 store most data values as 16-bit integers, however working with 32-bit floating point numbers is significantly easier so we will do that conversion at this step as well.
```
docker exec -ti gdal gdal_translate -ot float32 -unscale -CO COMPRESS=deflate NETCDF:"OR_ABI-L1b-RadF-M3C02_G16_s20171921545382_e20171921556149_c20171921556183.nc":Rad fulldisk.tif
```
If this command runs successfully it should have created a `fulldisk.tif` in your directory.

After you have this fulldisk file you can convert it to a png image again using `gdal_translate`.
```
docker exec -ti gdal gdal_translate -ot Byte -of png -scale 0 650 0 255 fulldisk.tif fulldisk.png
```
This command will convert the tiff file to a png while scaling the data values from 0-650 in the tiff to 0-255 so that they fit in a byte for the png file.
![Full Disk GOES-16 Sample Image Created Using GDAL](gdal_fulldisk.png "Full Disk GOES-16 png")

## Reprojecting GOES-16 Data
Now that you have a basic idea of how to work with the data you may be interested in using it in GIS applications such as ArcGIS or QGIS. To do this we need to reproject the data from the geostationary viewpoint into a rectilinear projection such as geographic (just lat-lon values). We will use the `gdalwarp` utility to do this reprojection process while using the tiff file from the previous step.
```
docker exec -ti gdal gdalwarp -t_srs EPSG:4326 -dstnodata -999.0 fulldisk.tif fulldisk_geo.tif
```
This step will create a fulldisk_geo.tif file which uses the projection defined by `EPSG:4326` (geographic). This file can be readily loaded into GIS software and reprojected further or displayed with other datasets.

To compare the difference after reprojection we will also create a png file here using a step similar to that in the previous section.
```
docker exec -ti gdal gdal_translate -ot Byte -of png -scale 0 650 0 255 fulldisk_geo.tif fulldisk_geo.png
```
which will create a fulldisk_geo.png file in your current directory. Opening this file you can see the difference where the data has been turned from looking spherical into being elongated and stretched.

![Geographic Full Disk GOES-16 Sample Image](gdal_fulldisk_geo.png "Full Disk GOES-16 After Being Reprojected to Geographic Projection")
