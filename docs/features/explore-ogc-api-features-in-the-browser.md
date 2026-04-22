# Explore OGC API - Features in the browser

Let’s first explore in the browser what you can do with OGC API - Features. We use the landing page and go through the components one by one, demonstrate possibilities, and inspect data previews.

## api.pdok.nl

**:arrow_right: Go to <https://api.pdok.nl>**

Here you find an overview of all PDOK APIs.

**:arrow_right: Scan the whole page.**

!!! question "Question"

    Are these all OGC APIs, or also other API types?

**:arrow_right: Find and open: *Basisregistratie Grootschalige Topografie (OGC API)***

## Landing page

You are now on the landing page of the BGT OGC API.

![Screenshot of the BGT OGC API landing page](../assets/landing_page.png)

BGT is a national dataset with public-space objects such as roads, water, and green areas. We use this dataset as example. At the moment, BGT is the most complete OGC API implementation at PDOK.

??? info "What is the Large-Scale Topography Registry?"

    The BGT is a nationwide dataset with *large-scale* topography (intended use scale 1:500 to 1:5000). It includes roads, water bodies, green areas, and buildings and is maintained by municipalities, provinces, and national authorities. [More information about BGT.](https://www.digitaleoverheid.nl/overzicht-van-alle-onderwerpen/stelsel-van-basisregistraties/10-basisregistraties/bgt/)

    BGT is a base registry with legal obligations for maintenance and quality. [More information about the base registry system.](https://www.digitaleoverheid.nl/overzicht-van-alle-onderwerpen/stelsel-van-basisregistraties/10-basisregistraties/)

The landing page is a human-readable API entry point, and there is also a machine-oriented representation.

!!! question "Question"

    Where can you find the machine-oriented description?

**:arrow_right: View the machine-oriented description.**

**:arrow_right: Then go back to HTML view (human-readable).**

The landing page includes dataset description, references, keywords, and metadata.

BGT is available as OGC API – Features and OGC API – Tiles. Therefore this landing page has 6 components.

| Page                                          | Explanation                                                        | When?                     |
|-----------------------------------------------|--------------------------------------------------------------------|---------------------------|
| [OpenAPI specification](#openapi-specification) | Description of API calls this API provides                         | Always (OGC API - Common) |
| [Conformance](#conformance)                   | Which OGC standards this API conforms to                           | Always (OGC API - Common) |
| [Collections](#collections)                   | Feature data                                                       | OGC API – Features        |
| [Tiles](#ogc-api---tiles-components)          | Vector tiles (visualization)                                       | OGC API – Tiles           |
| [Styles](#ogc-api---tiles-components)         | Styles (rendering)                                                 | OGC API – Styles          |
| [Tile Matrix Sets](#ogc-api---tiles-components) | Tile structure                                                     | OGC API – Tiles           |

Let’s explore the pages.

## OGC API - Common components

### OpenAPI specification

**:arrow_right: Click 'OpenAPI specification' on the landing page**

![Screenshot of the OpenAPI specification](../assets/openapispecification.png)

This is the Swagger UI for the API. It shows all supported API calls and how to use them. You can compose and test requests directly.

!!! info "Swagger UI"

    Swagger UI is a widely used way to document APIs in a human-readable format. Read more on <https://swagger.io/>.

!!! info "OpenAPI specification"

    OpenAPI specification is a standard for machine-readable API descriptions in YAML/JSON. Read more on <https://swagger.io/specification/>.

Try this call:

**:arrow_right: Expand** 'GET `/api` This document' **and execute it.**

![GET /api This document](../assets/get-api.png)

You now see the executed `curl` command and response.

![curl get api specification](../assets/openapispecification_get.png)

!!! question "What is the version number of this API?"

??? success "Answer"

    The BGT OGC API version is 1.0.0. The value 3.0.0 refers to the OpenAPI specification version (`"openapi"`). API version is under `"info"."version"`.

**:arrow_right: Return to landing page**

### Conformance

**:arrow_right: Click 'Conformance'**

![Screenshot of the Conformance page](../assets/conformance.png)

This page shows which OGC standards and versions this API implements.

**:arrow_right: Return to landing page**

## OGC API - Features components

### Collections

**:arrow_right: Click 'Collections'**

![Screenshot of the Collections page](../assets/features/collections.png)

Here you see all collections offered by the BGT OGC API.

A collection is a set of objects (*features*) of one type. You can think of it as a table.

Each collection has description, keywords, image, update date, spatial extent, and temporal extent.

Let’s use collection 'Bak' as an example.

**:arrow_right: Click 'View schema' for collection 'Bak'**

The schema shows columns/attributes, datatypes, required fields, and descriptions.

!!! info "Columns, attributes, or fields?"

    In practice, these terms all refer to a property of an object with a certain datatype.

!!! question "Question"

    In which column is geometry stored? Is Bak made of points, lines, or polygons?

??? success "Answer"

    Geometry is stored in attribute `geometry`. It is a `point`.

**:arrow_right: Return to 'Collections' and click 'Bak (BAK)'**

![Bak collection page](../assets/features/collectie_bak.png)

You can browse features here in three ways:

1. In the user interface
2. As GeoJSON in a selected CRS
3. As JSON-FG in a selected CRS

!!! info "GeoJSON and JSON-FG"

    GeoJSON supports geometry in JSON and is widely used for web applications, but formally supports only WGS84.

    JSON-FG extends GeoJSON and formally supports all CRS values.

**:arrow_right: Click ['Features'](https://api.pdok.nl/lv/bgt/ogc/v1/collections/bak/items)**

You can now browse items and apply filters:

- **CRS**
- **Reference date**
- **Limit**
- **Lokaal_id**

Set these filters:

- **CRS: http://www.opengis.net/def/crs/EPSG/0/28992**
- **Reference date: 01-01-2026**
- **Limit: 10 items**
- **Lokaal_id: empty**

Apply filters and inspect map + tables.

!!! question "Question"

    When was bak `G0518.fcb8ea5528fbb4fae0402a0a313c2f1b` created?

??? success "Answer"

    `creation_date` = `2013-09-30T22:00:00Z`

!!! question "Question"

    What does the 'Next' button do?

??? success "Answer"

    It retrieves the next set of results according to the current limit.

??? info "Pagination"

    Results are split into pages to avoid loading everything at once.

!!! question "Question"

    What changed in the browser URL when you went to the next page?

??? success "Answer"

    A `cursor=...` parameter was added.

??? info "Cursor pagination and offset pagination"

    Cursor pagination uses an identifier for a result batch and scales better for large datasets than offset pagination.

#### Filter by bounding box

A key spatial filter is `bbox` (bounding box): left-bottom x/y and right-top x/y.

**:arrow_right: Draw a rectangle on the map using the square icon.**

![Draw a bounding box](../assets/features/draw-boundingbox-1.png)

![Draw a bounding box](../assets/features/draw-boundingbox-2.png)

Results within the rectangle are shown on the map and in tables.

#### Filters in the URL

Filters are part of the URL. Example (decoded):

```
https://api.pdok.nl/lv/bgt/ogc/v1/collections/bak/items?
crs=http://www.opengis.net/def/crs/EPSG/0/28992&
datetime=2026-01-01T00:00:00.000Z&
f=html&
limit=10&
bbox=4.2272271035977065,52.04836512237336,4.265429015995505,52.06308825720682
```

| Parameter | Value | Explanation |
| --- | --- | --- |
| `https://api.pdok.nl/lv/bgt/ogc/v1/collections/bak/items` |  | Collection items endpoint |
| `crs` | `http://www.opengis.net/def/crs/EPSG/0/28992` | CRS in which item coordinates are returned |
| `cursor` | `Ww\|Mhj0MA` | Returned page identifier |
| `datetime` | `2026-01-01T00:00:00.000Z` | Reference date |
| `f` | `html` | Response format |
| `limit` | `10` | Max items per response |
| `bbox` | `4.2272271035977065,52.04836512237336,4.265429015995505,52.06308825720682` | Spatial filter |

You can also inspect results in GeoJSON and JSON-FG and compare differences.

You now know how to browse OGC API - Features collections, filter in browser, and retrieve results.

:material-lightbulb: A dataset can be published in one or more collections.

:material-lightbulb: A collection is a standalone component with its own schema.

:material-lightbulb: Parameters let you select format and filter data.

**:arrow_right: Return to the landing page**

<a name="ogc-api---tiles-components"></a>
## OGC API - Tiles components

We do not explore these pages here. See [OGC API - Tiles](../tiles/introduction.md):

* Tiles
* Styles
* Tile Matrix Sets

## Summary

In this section, you explored an OGC API landing page (HTML view) in the browser. You saw how to quickly inspect available data, specifically for OGC API - Features, using BGT as example.

| Component | Explanation |
| --------- | ----------- |
| OpenAPI specification | Swagger UI showing API capabilities |
| Conformance | Overview of standards this API conforms to |
| Collections | The collections (tables/map layers) exposed by this OGC API |
