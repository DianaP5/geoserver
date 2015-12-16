## Software evolution on Geoserver for ESOF

### Table of Contents
1. [Introduction](#intro)
1. [Feature selection](#select)
1. [Specification](#specs)
  1. [Artifacts in need of refactoring](#artifacts)
    1. [Changes by source file](#change)
    1. [Caveat and impact on other components](#caveat)
  1. [Testing changes](#test)

### <a name="intro"></a> 1. Introduction

This report will be looking at a requested feature for Geoserver, analysing the impact the implementation of this new feature will have on the project, the components that would be affected and the tests that would have to be changed and/or added due to the new feature.

### <a name="select"></a> 2. Feature selection

The original intent was to attempt to implement a new feature and this weighed heavily on the choice of the feature for study. However, due to time constraints and a less than ideal grasp of the whole project we were unable to do so.

We will be drafting the specification and analysing the possible implementation and validation of [GEOS-7342](https://osgeo-org.atlassian.net/browse/GEOS-7342) : LayerGroup chooser in the LayerGroup page suggests LGs from other workspaces

### <a name="specs"></a> 3. Specification

When creating a new layer group in Geoserver it's possible to set a workspace for it. It is also possible to add layers and other layer groups o the newly created layer. The web UI provides the user with a suggestion list of all possible (existing) layers and layer groups. If however the user has set a workspace for the new layer group, it will not be possible to add layers and layer groups that do not belong to the same workspace despite them appearing on the suggested list.
Some users have shown a desire to have the suggestion list only show valid entries, reacting to the workspace selected.

#### <a name="artifacts"></a> 3.1 Artifacts in need of refactoring

The bulk of the change to the code would be done on package _main.org.geoserver.web.data.layergroup_.

##### <a name="change"></a> 3.1.1 Changes by source file:

* __AbstractLayerGroupPage.java__

  In source file AbstractLayerGroupPage.java the web UI page data forms are set. The dropdown list of available workspaces is created here. For the improvement we are analysing this value in variable __wsChoice__ (line 119). The set up for adding existing layers and layer groups is done on line 169:
> form.add(lgEntryPanel = new LayerGroupEntryPanel( "layers", layerGroup ));

* __LayerGroupEntryPanel.java__

  Here we would add a third parameter to the LayerGroupEntryPanel constructor, representing the workspace we want to be restricted to.
A new variable of would be added to hold the workspace.
The "add layer" and "add layer group" pop windows are added on this file from lines 106 to 123 and from lines 129 to 145 respectively. The content that will fill the choice lists is read at line 112 for layers:
> popupWindow.setContent( new LayerListPanel(popupWindow.getContentId())

  and line 135 for layer groups:
> popupWindow.setContent( new LayerGroupListPanel(popupWindow.getContentId())

  To construct the lists of choices two other classes are used then:

  LayerGroupListPanel and LayerListPanel. We would have o pass them the selected workspace, using their constructors as well.

* __LayerListPanel.java__

  The list of layers is obtained through a subclass LayerListProvider whose constructor would be changed to receive the workspace selected. This subclass has a function __*getProperties()*__ (line 46) in which the list of layers is obtained. In here, before returning the list we would remove those elements for which the workspace property does not match the one received by the constructor.

* __LayerGroupListPanel.java__

  Once again, same approach. The selected workspace would be passes as an extra constructor parameter. In function __*getProperties()*__ (line 42) the layer groups of different workspaces would be removed from the list that's returned.

##### <a name="caveat"></a> 3.1.2 Caveat and impact on other components

All these constructors marked for change would also be coded to handle the workspace parameter being NULL in which case they would behave as they do now.
Since these components are only used for the purpose of handling layer and layer group creation through the web UI, and used in the same manner in both cases, the transition from current version to one with the proposed changes would be seamless, except perhaps in cases were some community modules which make use of the altered classes are in use, which would also have to change their code by adding NULL as parameter to the constructors marked for change above.

##### <a name="test"></a> 3.2 Testing changes

The classes *LayerGroupNewPageTest* in source file LayerGroupNewPageTest.java from package __test.org.geoserver.web.data.layergroup__ and *NewLayerPageTest* in file NewLayerPageTest.java in package __test.org.geoserver.web.data.layer__ are where the classes that would be changed are currently tested. They do not require any change to test the changes proposed.
