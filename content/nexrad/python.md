+++
date = "2017-04-10T16:41:54+01:00"
weight = 110
description = "Work with NEXRAD data using Python and Jupyter"
title = "Python | Jupyter"
draft = false
bref= "Work with NEXRAD data using Python and Jupyter"
toc = true
+++

### EXAMPLE:  Analysis of NOAA's NEXRAD dataset using Signpost, Jupyter, and Py-ART

A sample analysis of NEXRAD data is available showing how to:

* setup your work environment
* pull some data from the ID service 
* download files from the repositories the ID service references
* make multiple plots of raw reflectivity data
* filter the reflectivity data for 'bioscatter'
* animate plots 

The sample notebook looks at an interesting Mayfly hatching event and shows how to review and filter detected "bioscatter".

For [OSDC Griffin](https://www.opensciencedatacloud.org/) allocation grantees, we have two VMs available as public snapshots: nexrad-jupyter and nexrad-jupyter-docker that contain all the tools required to run the analysis.  Use the README.md in the VM root directory, or check the [OSDC Griffin support docs example](https://www.opensciencedatacloud.org/support/griffin.html#example-installing-software-and-running-a-jupyter-notebook) on how to install software and port forward Jupyter notebook to view and work locally.   

For advanced users familiar with docker commands, we recommend using the nexrad-jupyter-docker, which containerizes the different tasks, including the deployment of the notebook itself.  The containerization allows for deployment of the analysis without any of the required software installed on the VM itself.  In both snapshots, the resulting analysis is essentially the same.  

### Where is the Notebook?

If you are using either public snapshot, all software has already been installed.  

For the larger community, the same notebooks are public at [https://github.com/occ-data/nexrad-jupyter-osdc](https://github.com/occ-data/nexrad-jupyter-osdc).   To simply view as a webpage, go to  [https://occ-data.github.io/nexrad-jupyter-osdc/nexrad/nexrad_display_id_service_HTML_.html](https://occ-data.github.io/nexrad-jupyter-osdc/nexrad/nexrad_display_id_service_HTML_.html).   

Not all browsers handle the animation in the Jupyter notebook demo well.   We had success using Chrome.  