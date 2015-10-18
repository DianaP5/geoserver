## High Level Requirement Specification for GeoServer

### Table of Contents
1. [Introduction](#intro)
  1. [Context](#context)
  2. [Purpose and Scope](#purpose)
2. [Overall Description and Use Cases](#description)
  1. [WFS, WCS and WMS](#services)  
3. [External Interface Requirements]("#external")
4. [Other Nonfunctional Requirements]("#othernonfunc")
5. [Other Requirements]("#others")

### <a name="intro"></a> 1. Introduction

#### <a name="context"></a> 1.1 Context

GeoServer is an open source java server that allows users to share, process and edit geospatial data. One of the more important aspects of the server is the integration with various geographic information systems in use today, which is done through open standards.

#### <a name="purpose"></a> 1.2 Purpose and Scope

This document intends to represent a high level view of GeoServer, through its features, interfaces and some non-functional requirements considered essential.

### <a name="description"></a> 2. Overall Description and Use Cases

This section presents an overview of the functionalities of GeoServer from various user's perspectives, _TODO:_ and is intended for end users and developers.

![Service Management](img/exp_imp.png)

_Services to be provided for integration with other systems_

![Security Management](img/sec_mgmt.png)

_Security management of the server_

![Data Management](img/data_mgmt.png)

_Data management for the server_


#### <a href=services></a> 2.1 WFS, WCS and WMS

To allow sharing of data GeoServer implements the following widely used open standards for geospatial data:

*  [WFS](http://www.opengeospatial.org/standards/wfs) versions 1.0.0, 1.1.0 and 2.0.0 for vector data. This allows compliant systems acess to the data structures and source data.
  * The WFS implementation is integrated with the Security system to limit access.

* [WCS](http://www.opengeospatial.org/standards/wcs) versions 1.0, 1.1 and 2.0. They work similarly to WFS but for raster data.

* [WMS](http://www.opengeospatial.org/standards/wms) versions 1.1.1, the most used, and 1.3.0. WMS provides a standard for geospatial map image requests, allowing clients to combine multiple images.
 * GeoServer also provides KML as WMS output, allowing integration with for example, google earth.
