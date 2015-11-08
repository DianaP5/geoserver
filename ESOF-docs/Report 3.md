## 1. Introduction

This document intends to describe the software structure of geoserver, derived from the project's source code and documentation.
To represent the projects architecture we will be using the [__4+1__ architectural view model](https://en.wikipedia.org/wiki/4%2B1_architectural_view_model). This model consists of 4 concurrent and a set of use cases (the + 1) which can be found on [Report 2](Report 2.md).

## 2. Views

## 2.1 Implementation view
The following component diagram represents a high level view of the main components of geoserver, as it is implemented.

![Component diagram](img/implementation_view/component_diagram.png)

## 2.2 Logical view
These are the classes that correspond to the overarching components represented on the previous component diagram.


### High level class packages representation
![High level logical view](img/logical_view/logical_view_high_level.png)

### 2.2.1 Geoserver core
![Geoserver core classes](img/logical_view/core_detail.png)

### 2.2.2. Security implementation

#### Security core classes
![Security core classes](img/logical_view/security/sec_core_detail.png)
#### Security authentication classes
![Security authentication classes](img/logical_view/security/sec_auth_detail.png)
#### Security configuration classes
![Security configuration classes](img/logical_view/security/sec_config_detail.png)
#### Security validation classes
![Security validation classes](img/logical_view/security/sec_valid_detail.png)

### 2.2.3. Standards implementation

#### WCS
![WCS core](img/logical_view/standards/wcs_detail.png)
##### WCS 1.0
![WCS core](img/logical_view/standards/wcs_1_0_detail.png)
##### WCS 1.1
![WCS core](img/logical_view/standards/wcs_1_1_detail.png)
##### WCS 2.0
![WCS core](img/logical_view/standards/wcs_2_0_detail.png)

#### WFS
![WFS core](img/logical_view/standards/wfs_detail.png)

#### WMS
![WMS core](img/logical_view/standards/wms_detail.png)

### 2.2.4. Web UI implementation
![web core](img/logical_view/web_detail.png)

## 2.3. Process view
![Activity diagram](img/implementation_view/process_view.jpg)

## 2.4. Deployment view
