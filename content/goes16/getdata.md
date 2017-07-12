+++
description = "How to get GOES-16 data from the OCC Environmental Data Commons"
title = "Get Data"
date = "2017-07-12T12:00:00+00:00"
draft = false
weight = 1
toc = true
bref = ""
+++

### Provisional Data
*__NOAA's GOES-16 satellite has not been declared operational and its data are preliminary and undergoing testing.__*

### Best Effort
The data are being made available on a best effort basis by all parties involved. There are no guarantees the data will be available when you really need it.

### File Formats
The data is being made available in a NetCDF file format. The data are referenced in an angular system (x & y coordinates measure radians).

### Products Available & Name Conventions

There are several Level 1b (L1b) and Level 2 (L2) ABI products available over different regions with different scanning times. The table below summarizes the products, the refresh rate for the products and gives example paths of where to find the data.

| Product Level | Product Name | Product Short Name | ABI Scene | Time Between Images | Example File Name |
| ------------- | :----------: | :----------------: | :-------: | :-----: | :-------: |
|   L1b | Radiances | RadM | Mesoscale | 30-60 seconds | ABI-L1b-RadM/2017/192/19/OR_ABI-L1b-RadM-M3C14_G16_s20171921952189_e20171921954562_c20171921955013.nc |
|   L1b | Radiances | RadC | CONUS | 5 minutes | ABI-L1b-RadC/2017/192/19/OR_ABI-L1b-RadC-M3C14_G16_s20171921952189_e20171921954562_c20171921955013.nc |
|   L1b | Radiances | RadF | Full Disk | 15 minutes | ABI-L1b-RadF/2017/192/19/OR_ABI-L1b-RadF-M3C14_G16_s20171921952189_e20171921954562_c20171921955013.nc |
|   L2 | Cloud & Moisture Imagery | CMIPM | Mesoscale | 30-60 seconds | ABI-L2-CMIPM/2017/191/21/OR_ABI-L2-CMIPM1-M3C02_G16_s20171912128268_e20171912128326_c20171912128391.nc |
|   L2 | Cloud & Moisture Imagery | CMIPC | CONUS | 5 Minutes | ABI-L2-CMIPC/2017/191/21/OR_ABI-L2-CMIPC-M3C02_G16_s20171912122189_e20171912124562_c20171912125065.nc |
|   L2 | Cloud & Moisture Imagery | CMIPF | Full Disk | 15 Minutes | ABI-L2-CMIPF/2017/192/15/OR_ABI-L2-CMIPF-M3C02_G16_s20171921515382_e20171921526149_c20171921526214.nc |
|   L2 | Multi-Band Cloud & Moisture Imagery | MCMIPM | Mesoscale | 30-60 seconds | ABI-L2-MCMIPM/2017/191/21/OR_ABI-L2-MCMIPM2-M3_G16_s20171912130568_e20171912131031_c20171912131105.nc |
|   L2 | Multi-Band Cloud & Moisture Imagery | MCMIPC | CONUS | 5 Minutes | ABI-L2-MCMIPC/2017/191/21/OR_ABI-L2-MCMIPC-M3_G16_s20171912122189_e20171912124562_c20171912125065.nc |
|   L2 | Multi-Band Cloud & Moisture Imagery | MCMIPF | Full Disk | 15 Minutes | ABI-L2-MCMIPF/2017/191/21/OR_ABI-L2-MCMIPF-M3_G16_s20171912115380_e20171912126152_c20171912126330.nc  |

The ABI sensor images over 16 different channels (wavelengths) as described in the table below

| Channel | Central Wave Length (µm) | Sprectrum Name |
| :----:  | :---------: | :------------: |
| 1       |  0.47  |   Visible - Blue |
| 2       |  0.64  | Visible - Red |
| 3       |  0.86  | Near IR - Vegetation |
| 4       |  1.37  | Near IR - Cirrus |
| 5       |  1.6  | Near IR - Snow/Ice |
| 6       |  2.2  | Near IR - Cloud Ice |
| 7       |  3.9  | IR - Shortwave |
| 8       |  6.2  | IR - Upper-Level Water Vapor |
| 9       |  6.9  | IR - Mid-Level Water Vapor |
| 10       |  7.3  | IR - Lower-Level Water Vapor |
| 11       |  8.4 | IR - Cloud Top Phase |
| 12       |  9.6  | IR - Ozone |
| 13       |  10.3  | IR - Clean |
| 14       |  11.2 | IR - Standard |
| 15       |  12.3  | IR - Dirty |
| 16       | 13.3  | IR - CO2 |

The filenames are

    <sensor>-<level>-<product short name>/<year>/<julian day>/<hour>/OR_<sensor>-<level>-<product short name>-M<scanning mode>-C<channel>-G<GOES Satellite>-s<start time>_e<end time>_c<central time>.nc

### Data Access

Data access is provided via a S3-API compatible service. The files may be downloaded with the aws cli, boto, or through a web browser.

[https://osdc.rcc.uchicago.edu/noaa-goes16](https://osdc.rcc.uchicago.edu/noaa-goes16)

This dataset is being generously hosted by The Research Computing Center (RCC) at the University of Chicago.

The [Research Computing Center](https://rcc.uchicago.edu/), within the Office of the Executive Vice President for Research. Innovation, and National Laboratories, was created in early 2010 to provide the University of Chicago community a full-service high-performance computing (HPC) resources, including one of the top 500 HPC cluster, high-speed parallel storage, 3D HD visualization facilities, ready-to-use applications, domain computational scientists, and data-management strategies to researchers and students across all departments and divisions of the University. 


