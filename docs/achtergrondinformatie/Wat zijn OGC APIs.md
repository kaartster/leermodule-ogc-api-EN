# What are OGC APIs?

**:arrow_right: Watch this video first:**

<div class="video-wrapper">
  <iframe src="https://www.youtube-nocookie.com/embed/hNmZJ1itqfM"
          title="OGC APIs"
          frameborder="0"
          allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
          allowfullscreen>
  </iframe>
</div>

An OGC API is a standardized interface that allows users and systems to query and view geodata via the internet. An API, an Application Programming Interface, can be used by people to request data. But even more often, APIs are used by systems (machines) to communicate with each other. In this way, developers can easily integrate data from other sources into their own software. An API is therefore like a power socket for data. Unlike in the past, you no longer need specific geodata knowledge to do this.

An OGC API follows API standards defined by the Open Geospatial Consortium (OGC). This is a global organization that creates open standards for the geoinformation domain. The standard defines exactly how the interface must be structured. The OGC API standard is an open standard that is widely adopted.

An OGC API always consists of the same components. OGC API also has different forms for making data available. Which form you choose depends on what you want to do with the geodata. For organizations publishing data through an OGC API, it depends on how they want to make data available.

## OGC API components

!!! warning "TO DO"

The overview below shows how the OGC API standard is built from building blocks. All these building blocks contain one or more specifications defined by OGC and approved by the geo community.

![The OGC API building blocks](../assets/ogc-api-building-blocks.png)

The table below shows which building blocks exist, whether they have been implemented by PDOK (status: January 2026), and where this building block is covered in this learning module.

| Component                                            | Description                          | Available at PDOK? |                                   Learning module                                |
|------------------------------------------------------|--------------------------------------|:------------------:|:---------------------------------------------------------------------------------:|
| [**Common**](<https://ogcapi.ogc.org/common/>)       | The foundation for every OGC API     |         ✅         | [Features](<../features/Introductie.md>) and [Tiles](<../tiles/Introductie.md>) |
| [**Features**](<https://ogcapi.ogc.org/features>)    | Vector data                          |         ✅         |                    [Features](<../features/Introductie.md>)                      |
| [**Tiles**](<https://ogcapi.ogc.org/tiles>)          | Map tiles (visualization)            |         ✅         |                       [Tiles](<../tiles/Introductie.md>)                         |
| [**Styles**](<https://ogcapi.ogc.org/styles>)        | Visualization rules                  |         ✅         |                       [Tiles](<../tiles/Introductie.md>)                         |
| [**Records**](<https://ogcapi.ogc.org/records>)      | Metadata                             |         ❌         |                                         ❌                                         |
| [**Maps**](<https://ogcapi.ogc.org/maps>)            | Ready-to-use maps and map tiles      |         ❌         |                                         ❌                                         |
| [**Coverages**](<https://ogcapi.ogc.org/coverages/>) | Raster data                          |         ❌         |                                         ❌                                         |
| [**EDR**](<https://ogcapi.ogc.org/edr>)              | Environment Data Retrieval           |         ❌         |                                         ❌                                         |

Let’s briefly examine the building blocks one by one.

### Common

The basic building block every OGC API needs at minimum. This block contains an API landing page, API conformance page, and API specification.

### Features

Building block for querying and editing feature data (vector data). This block consists of the following parts:

* **Part 1: Core**
* **Part 2: CRS** for storing or querying feature data in a specific coordinate reference system;
* **Part 3: Filtering** for querying feature data based on filters;
* **Part 4: [CRUD](https://nl.wikipedia.org/wiki/CRUD)** for creating, replacing, updating, and deleting feature data.
* *Draft* Part 5: Schemas
* *Draft* Part 6: Property Selection
* *Draft* Part 7: Geometry Simplification
* *Draft* Part 8: Sorting
* *Draft* Part 9: Text Search
* *Draft* Part 10: Search/Queries

### Tiles

Building block for requesting geodata as map tiles and viewing this data.

### Styles

Building block for providing and applying visualization rules.

### Records

Building block for searching and requesting metadata about geodata (for example timeliness, descriptions, constraints, contacts).

### Maps

Building block for requesting geodata as a ready-to-use map.

### Coverages

Building block for requesting raster data, including cell-level computations.

### EDR

Building block for Environment Data Retrieval (EDR): integrally querying spatial climate data that combines multiple dimensions. Think of querying humidity, temperature, and precipitation in 3D over time.

![Overview of OGC APIs](../assets/achtergrondinformatie/ogcapis-overview.png)

* Processes
* Moving Features
* Routes
* 3D GeoVolumes
* Joins
* Discrete Global Grid System [(DGGS)](https://ogcapi.ogc.org/dggs/)
* Connected Systems
