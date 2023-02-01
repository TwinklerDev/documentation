# 
# Key Concepts

To use Twinkler effectively it is best to understand the following key concepts.

# Project

All activity in Twinkler occurs within the context of a project.  A project holds one or more sites, coverages and layers ie. a radio network. For example, a project may be:

* the in-service network of one area eg. a state or region
* the network of a client or customer
* a potential network build being evaluated
* a play area to test coverage ideas

See [Project](/map-menu?id=sites) for more details.

# Map

The map is the main part of the screen that displays sites, coverage and layers. 

<div style="text-align:center"><img src="/_media/map_types.png" /></div>

The map is based on Google Maps and supports two map types - **street maps** (with terrain) and **satellite view** (with labels). The terrain map is great for understanding how coverage has been affected by land elevation. The satellite view gives an appreciation of land use and population dispersion.

<div style="text-align:center"><img src="/_media/terrain_example.png"/>&nbsp;<img src="/_media/satellite_example.png" /></div>

**Google Street View** is also supported, which is great for on-the-ground visuals of sites and antennas.

<div style="text-align:center"><img src="/_media/streetview_man.png"/></div>

<div style="text-align:center"><img src="/_media/streetview_selection.png"/>&nbsp;<img src="/_media/streetview_example_01.png" /></div>

A **legend** of signal strength values for the selected coverage can be displayed on the map (it is configurable). If another display measurement is selected then a legend for that measurement is displayed eg. metres for elevation, Mbps for throughout.

<div style="text-align:center"><img src="/_media/legend_dbm.png" /></div>

There are several options to select what features and color-schemes are shown on the map ie. the **map style**. The map style options are applied and saved to the whole project, and are located in the Project menu ([link](map-menu.md?id=map-style)).

# Site

A site is a point on the map from which coverage predictions can be made. It may, for example be a rooftop, street pole, dedicated tower or the side of a building.

Each site is shown on the map with a selectable [image](/parameters?id=IMAGES) and a selectable [color](/parameters?id=COLORS) eg. a red target. ![red target](/_media/red_target.png)

See [Sites](/map-menu?id=sites) for more details.

# Coverage

"Coverage" is the area through which radio waves propagate from the transmitting antenna. The radio coverage shown on the map is an estimate (or prediction) of the power of the radio signal that will be received at each point surrounding the transmitting antenna, based on the predition parameters.

<div style="text-align:center"><img src="/_media/coverage_example.png"/></div>

See [Coverage](/map-menu?id=coverage) and [Radio Coverage Prediction](radio-prediction.md?id=radio-coverage-prediction) for more details.

# Tags

Tags are pieces of information (or metadata) associated with a site or coverage prediction, which allow the sites and coverages to be filtered on the map in real-time. A tag, for example, could be "In Service", "Future", "Transmission Hub" or "Ericsson". Tags are applied to as many sites or coverages as is necessary.

The user is able to filter what sites and coverage predictions are shown on the map by combining multiple tags. 

<div style="text-align:center"><img src="/_media/tag_example.png" /></div>

See [Site](/map-menu?id=site) and [Coverage](/map-menu?id=coverage) for more details.

# Antenna

<div style="text-align:center"><img src="/_media/antenna_ceiling.png"/>&nbsp;<img src="/_media/antenna_patch.png"/></div>

Antennas are a fundamental component of all radio communication links. The antenna turns electrical signals into radio waves (transmit), and radio waves back into electrical signals (receive). Twinkler allows the gain and directionality of the transmit antenna to be specified, as well as the gain of the receive antenna.  

<div style="text-align:center"><img src="/_media/antenna_panel.png"/>&nbsp;<img src="/_media/antenna_tower.png"/></div>

See [Antenna](/main-menu?id=antenna) and [Radio Coverage Prediction](radio-prediction?id=radio-coverage-prediction) for more details.

# Layers

A layer is geospatial information that is placed on top of the Google Map by the user. Layers give additional information that is relevant to the project, such as infrastructure layout, customer locations, population boundaries or points of interest.

Layers can be uploaded from a vector file, or delivered over the web through a third party map server.

<div style="text-align:center"><img src="/_media/layers_example.png"/></div>

See [Layers](/map-menu?id=layers) for more details.

# Organisations

Twinkler allows multiple users to collaborate and share radio network designs. Users are grouped together into an **organisation**. An organisation, for example, may be a wireless operator or consulting company.

Within an organisation, each user may be a member of one or more **groups**, controlled by the administrator(s) of the organisation. Every user selects which group(s) may access their projects, on a project-by-project basis. 

#### Organisation On-boarding

An organisation in Twinkler is initially established as part of the on-boarding process. The key pieces of information to establish an organisation are:

* The email domain(s) of the organisation
* The administrator(s) email address(es)

The email domain(s) is used to determine whether a Twinkler user is a candidate for membership of the organisation. Only an administrator can actually add/remove users to/from the organisation. 

The administrator also can create and remove groups, as well as add/remove users to/from groups.

#### User On-boarding

Three steps are required for a user to become part of an organisation:

1. The user creates a (free) account on Twinkler, using their organisation email address for the account
2. An administrator in the organisation adds the user's account to the organisation
3. The user updates their settings, to change from using their personal projects to the organisation projects.  

#### Users and Groups 

A key part of an organisation in Twinkler is the management of users and groups, which is performed by the administrator. The example diagram below illustrates how a user may be a member of any number of groups.

<div style="text-align:center"><img src="/_media/organisation.png" /></div>

#### Project Access Control

The owner of each project controls which groups have **edit**, **read** and **view** access of the project.

<div style="text-align:center"><img src="/_media/access_control.png" /></div>

In the example above, Engineering and Opoerations have "Edit" access to the project. The levels of access are:

* **Edit** access gives the ability to change the project, such as add coverage and sites.

* **Read** access gives the ability to explore the whole project including all coverage parameters, as well as copy and export the project and coverage.

* **View** access is the most limited, restricting users to only seeing sites and coverage on the map.

For more information see [Organisation Management](main-menu?id=organisation-management)
