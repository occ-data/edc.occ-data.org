+++
title = "Get Data"
date = "2017-07-12"
draft = false
weight = 100
description = "How to get NEXRAD data from the OCC Environmental Data Commons"
bref= "Simple ways to display NEXRAD LEVEL 2 data in Python using the Signpost ID Service"
toc= true
+++

### What is NEXRAD?

The Next Generation Weather Radar (NEXRAD) networks 160 Doppler radar sites throughout the United States and select overseas locations detecting precipitation and atmospheric movement. Level-II data include the original three meteorological base data quantities: reflectivity, mean radial velocity, and spectrum width, as well as the dual-polarization base data of differential reflectivity, correlation coefficient, and differential phase. NEXRAD Level II data is in the .GZ binary format specific to the NEXRAD project. The archives run June 1991 to present.

Data is made available to the research community as part of the [Open Common Consortium's collaboration with NOAA](http://occ-data.org/OCC_NOAA_CRADA). For more information visit the [NOAA Nexrad site](https://data.noaa.gov/dataset/noaa-next-generation-radar-nexrad-level-ii-base-data). 

### Why IDs? 

The NEXRAD dataset is ID'd by the [Signpost digital ID system](../signpost/). Signpost balances the needs of both data archiving for persistent storage, that is, assigning identifiers to unique pieces of information, and also active computation, that is, for finding locations of data on a living system where data may be physically moved or updated. OCC Members constructed a simple implementation of this design in a two-layer identification scheme service with a REST-like API interface. By utilizing the Signpost digital identifier service, we can relocate data files from our data commons to another commons and no researcher needs to change their code.

### Data Updates

New Level II data is added and indexed as soon as it is made available. 

### How can I use the data?

Anyone can freely download the data.   For [OSDC Allocation Grantees](https://www.opensciencedatacloud.org/), VMs have are available with tools for working with NEXRAD. 

* First use the [query tool or API](https://www.opensciencedatacloud.org/publicdata/noaa-nexrad-l2/) to find the digital IDs for the subset of interest. 
* Get the location of the data from the ID.  (See the [example notebook](../python/) for ideas how to do this.)
* Use standard s3 tools like [awscli](https://aws.amazon.com/cli/) or [the python boto library](https://github.com/boto/boto) to pull the data into your analysis environment.  