## Architectural Design for GeoServer

### Table of Contents
1. [Introduction](#intro)
2. [Views](#views)    
  1. [Implementation view](#implementation)
  2. [Logical view](#logical)
    1. [Geoserver core](#geo_core)
    2. [Security implementation](#security)
        1. [Security core classes](#sec_core)
        2. [Security authentication classes](#sec_auth)
        3. [Security configuration classes](#sec_config)
        4. [Security validation classes](#sec_valid)
    3. [Standard implementation](#standard)
        1. [WCS](#wcs)
            2. [WCS 1.0](#wcs_1_0)
            3. [WCS 1.1](#wcs_1_1)
            4. [WCS 2.0](#wcs_2_0)
        2. [WFS](#wfs)
        3. [WMS](#wms)
    4. [Web UI implementation](#web)
  3. [Process view](#process)
  4. [Deployment view](#deployment)

## <a name="intro"></a> 1. Introduction

This document intends to describe the software structure of geoserver, derived from the project's source code and documentation.
To represent the projects architecture we will be using the [__4+1__ architectural view model](https://en.wikipedia.org/wiki/4%2B1_architectural_view_model). This model consists of 4 concurrent and a set of use cases (the + 1) which can be found on [Report 2](Report 2.md).

## <a name="views"></a> 2. Views

## <a name="implementation"></a> 2.1 Implementation view
The following component diagram represents a high level view of the main components of geoserver, as it is implemented.

![Component diagram](img/implementation_view/component_diagram.png)

## <a name="logical"></a> 2.2 Logical view
These are the classes that correspond to the overarching components represented on the previous component diagram.


### High level class packages representation
![High level logical view](img/logical_view/logical_view_high_level.png)

### <a name="geo_core"></a> 2.2.1 Geoserver core
![Geoserver core classes](img/logical_view/core_detail.png)

### <a name="security"></a> 2.2.2. Security implementation

#### <a name="sec_core"></a> Security core classes
![Security core classes](img/logical_view/security/sec_core_detail.png)
#### <a name="sec_auth"></a> Security authentication classes
![Security authentication classes](img/logical_view/security/sec_auth_detail.png)
#### <a name="sec_config"></a> Security configuration classes
![Security configuration classes](img/logical_view/security/sec_config_detail.png)
#### <a name="sec_valid"></a> Security validation classes
![Security validation classes](img/logical_view/security/sec_valid_detail.png)

### <a name="std_core"></a> 2.2.3. Standards implementation

#### <a name="wcs"></a> WCS
![WCS core](img/logical_view/standards/wcs_detail.png)
##### <a name="wcs_1_0"></a> WCS 1.0
![WCS 1.0](img/logical_view/standards/wcs_1_0_detail.png)
##### <a name="wcs_1_1"></a> WCS 1.1
![WCS 1.1](img/logical_view/standards/wcs_1_1_detail.png)
##### <a name="wcs_2_0"></a> WCS 2.0
![WCS 2.0](img/logical_view/standards/wcs_2_0_detail.png)

#### <a name="wfs"></a> WFS
![WFS core](img/logical_view/standards/wfs_detail.png)

#### <a name="wms"></a> WMS
![WMS core](img/logical_view/standards/wms_detail.png)

### <a name="web"></a> 2.2.4. Web UI implementation
![web core](img/logical_view/web_detail.png)

## <a name="process"></a> 2.3. Process view
![Activity diagram](img/implementation_view/process_view.JPG)

## <a name="deployment"></a> 2.4. Deployment view
