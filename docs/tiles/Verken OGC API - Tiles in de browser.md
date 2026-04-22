# Explore OGC API - Tiles in the browser

Let’s first explore in the browser what you can do with OGC API - Tiles. We do this using the landing page of the BGT OGC API. We go through the components one by one, demonstrate the possibilities, and view data previews.

## api.pdok.nl

**:arrow_right: Go to <https://api.pdok.nl>**

Here you will find an overview of all PDOK APIs.

**:arrow_right: Scan the whole page.**

!!! question "Question"

    Are these all OGC APIs, or are there other API types as well?

**:arrow_right: Find and open the following API: *Basisregistratie Grootschalige Topografie (OGC API)***

## Landing page

You are now on the landing page of the BGT OGC API.

![Screenshot of the BGT OGC API landing page](../assets/landing_page.png)

BGT (Large-Scale Topography Registry) is a national dataset with objects in public space that are usually managed by governments, such as roads, water, and green areas. We use the OGC API of this dataset as an example. At this moment, BGT is the most complete OGC API implementation at PDOK because it contains all building blocks currently implemented by PDOK.

??? info "What is the Large-Scale Topography Registry?"

    The BGT is a nationwide dataset with *large-scale* topography. These are geographic objects intended for use at large scales: 1:500 to 1:5000. In this context, *large-scale* does not refer to territorial extent, although it is indeed a large dataset. The BGT includes roads, water bodies, green areas, and buildings. It is maintained by municipalities, provinces, and national authorities. It is used, among other things, to support management and maintenance of public space. [More information about BGT can be found here.](https://www.digitaleoverheid.nl/overzicht-van-alle-onderwerpen/stelsel-van-basisregistraties/10-basisregistraties/bgt/)

    BGT is a base registry. That means regulations define how governments must maintain and use the dataset and what quality requirements apply. A base registry always has one or more source owners. There are more base registries, and many contain geodata, such as BAG, BRT, and BRK. [More information about the base registry system can be found here.](https://www.digitaleoverheid.nl/overzicht-van-alle-onderwerpen/stelsel-van-basisregistraties/10-basisregistraties/)

The landing page is a human-readable API entry point and description. Human-readable? Yes—because there is also a machine-oriented version.

!!! question "Question"

    Where can you find the machine-oriented description?

**:arrow_right: View the machine-oriented description.**

**:arrow_right: Then return to the HTML view (the human-readable version).**

A landing page contains a dataset description, references, keywords, and metadata.

BGT is made available as OGC API – Features and OGC API – Tiles. Therefore, this landing page has 6 components. Not every landing page has 6 components: some are mandatory and always present, while others appear only for Features and/or Tiles implementations.

| Page                                            | Explanation                                                         | When?                     |
|-------------------------------------------------|---------------------------------------------------------------------|---------------------------|
| [OpenAPI specification](#openapi-specification) | Description of API calls offered by this API                        | Always (OGC API - Common) |
| [Conformance](#conformance)                     | Which OGC standards does this API conform to?                       | Always (OGC API - Common) |
| [Collections](#collections)                     | Feature data                                                        | OGC API – Features        |
| [Tiles](#tiles)                                 | Vector tiles (visualization)                                        | OGC API – Tiles           |
| [Styles](#styles)                               | Styles (rendering)                                                  | OGC API – Styles          |
| [Tile Matrix Sets](#tile-matrix-sets)           | Structure of tiles                                                  | OGC API – Tiles           |

Let’s explore these pages.

## OGC API - Common components

### OpenAPI specification

**:arrow_right: On the landing page, click 'OpenAPI specification'**

![Screenshot of the OpenAPI specification](../assets/openapispecification.png)

Here you see the API’s Swagger UI. It shows all API calls supported by this API and how to use them. The Swagger UI gives example requests and lets you compose requests and test them directly in the browser.

!!! info "Swagger UI"

    Swagger UI is a widely used way to document APIs in a human-readable format. Read more: <https://swagger.io/>

Why is this page called 'OpenAPI specification'? Because by conforming to OGC API specifications, the API also conforms to OpenAPI specification requirements.

!!! info "OpenAPI specification"

    The OpenAPI specification is a standard for formally describing APIs in a machine-readable way. An OpenAPI document is YAML or JSON and follows a fixed structure. Read more: <https://swagger.io/specification/>

Let’s test something directly in Swagger UI.

**:arrow_right: Expand** 'GET `/api` This document' **:**

![GET /api This document](../assets/get-api.png)

This is the API call to request the OpenAPI specification itself.

**:arrow_right: Click *Try it out***

**:arrow_right: Click *Execute***

You now see the executed `curl` command and the response:

![curl get api specification](../assets/openapispecification_get.png)

One parameter is passed: return result as JSON. The response indeed returns JSON. Below you also see possible response codes and meanings.

!!! question "What is the version number of this specific API?"

??? success "Answer"

    The BGT OGC API version is 1.0.0. Is it 3.0.0? No—that is the OpenAPI version (`"openapi"`). The API version is found under `"info"."version"`.

You have now seen what you can do with the OpenAPI specification (Swagger UI). Developers can quickly compose working API calls and use them in applications.

!!! info "OpenAPI specification Swagger UI"

    We will use this much more in [one of the next sections](<../features/Bevraag OGC API - Features met curl.md>).

**:arrow_right: Return to the landing page (click BGT in the breadcrumb).**

### Conformance

**:arrow_right: On the landing page, click 'Conformance'**

![Screenshot of the Conformance page](../assets/conformance.png)

The Conformance page shows which OGC standards this API implements. So we can see exactly which building blocks and versions the BGT OGC API conforms to.

We also see that some standards are still draft versions.

**:arrow_right: Return to the landing page**

## OGC API - Features components

### Collections

We do not explore this page here. We cover it in the [OGC API - Features](../features/Introductie.md) section.

## OGC API - Tiles components

### Tiles

**:arrow_right: On the landing page, click 'Tiles'**

OpenAPI specification and Conformance were descriptive pages; now we will actually look at data.

![Screenshot of the Tiles page](../assets/tiles/tiles.png)

OGC API - Tiles can serve vector tiles and also other tile types such as aerial imagery. Here we focus on **vector tiles**.

The BGT dataset is offered as vector tiles in multiple map projections. A client requests data tile by tile. Those tiles are optimized to be compact while preserving useful visualization quality.

!!! info "*Vector* Tiles?"

    Traditionally, map tiles are images. A Web Map Service (WMS), for example, serves `png` or `jpeg` image tiles. Images load fast, but must be rendered server-side and users cannot easily choose styles. Zooming can become pixelated. Vector tiles solve this by simplifying vector data and splitting it into tiles. They combine vector flexibility with raster-like speed.

    See also [Raster or vector data?](<../achtergrondinformatie/Wat is geo-informatie.md/#raster-or-vector-data>). 

On this page you find the available Tile Matrix Sets. Each projection has its own set.

![alt text](../assets/achtergrondinformatie/Projection_conique.jpg){ width="250" }![alt text](../assets/achtergrondinformatie/Projection_cylindrique.jpg){ width="250" }![alt text](../assets/achtergrondinformatie/Projection_azimutale_stereographique.jpg){ width="250" }

!!! info "Coordinate reference systems and map projections"

    For more background, see [Background information](<../achtergrondinformatie/Wat is geo-informatie.md/#what-are-coordinate-reference-systems>).

**:arrow_right: Click around this page.**

!!! question "Question"

    How can you see in which Tile Matrix Sets the BGT OGC API is offered? Which three are they?

??? success "Answer"

    Via the dropdown menu. This dataset is offered in:

    * NetherlandsRDNewQuad
    * EuropeanETRS89_LAEAQuad
    * WebMercatorQuad

<a name="verschil-tussen-tile-matrix-sets"></a>
On the right, you see a preview of the selected Tile Matrix Set. At this zoom level, differences are minimal, but at smaller scales (zoomed out), projection differences can strongly distort country shapes and sizes.

When do you choose which projection? It depends on your application goal, geographic area, and standards. In the Netherlands, RD New is the standard, so use NetherlandsRDNewQuad. Some software only supports Web Mercator, then use WebMercatorQuad.

**:arrow_right: Select NetherlandsRDNewQuad in the dropdown.**

You may notice that URL template and example URL change with the selected Tile Matrix Set.

The URL template is: `https://api.pdok.nl/lv/bgt/ogc/v1/tiles/NetherlandsRDNewQuad/{z}/{y}/{x}?f=mvt`

You can use this URL to load tiles in a client.

!!! question "Question"

    What do `{z}`, `{y}`, and `{x}` stand for?

??? success "Answer"

    In this context, `{z}/{y}/{x}` identifies one specific tile: `{z}` is zoom level, `{y}` and `{x}` identify the tile within that zoom level. [See below for more details about Tile Matrix Sets.](<#tile-matrix-sets>)

A client can replace `{z}/{y}/{x}` based on the user viewport. You can see an example under *Example URL*.

**:arrow_right: Click 'View metadata'.**

You now open the page that describes the BGT NetherlandsRDNewQuad Tile Matrix Set.

![NetherlandsRDNewQuad for BGT](../assets/tiles/NetherlandsRDNewQuad.png)

!!! question "Question"

    In how many zoom levels is BGT OGC API - Tiles available? Which levels are they?

??? success "Answer"

    For BGT OGC API - Tiles, tiles are available only at zoom level 12. The Tile Matrix Set supports more levels, but this API dataset offers only one.

You have now seen previews of NetherlandsRDNewQuad, learned how to find available zoom levels, and identified the URL needed to use tiles in your own client or application.

:material-lightbulb: A dataset can be offered in one or more Tile Matrix Sets. A Tile Matrix Set is for one projection. An API does not necessarily include all zoom levels of that set.

**:arrow_right: Return to the landing page**

### Styles

**:arrow_right: On the landing page, click 'Styles'**

![Screenshot of the Styles page](../assets/tiles/styles.png)

Here you find available visualizations (styles) for this dataset. A style defines colors, line widths, labels, symbols, etc.

**:arrow_right: Click around this page.**

!!! question "Question"

    How can you see which styles the BGT OGC API offers?

??? success "Answer"

    Via the dropdown menu.

On the right, you see a preview of the selected style.

**:arrow_right: Try different styles and inspect the differences.**

A style is always linked to one Tile Matrix Set. For BGT, two styles are offered, and each style is available for each Tile Matrix Set, resulting in six styles in total.

Official styles are provided via the `styles` endpoint. You can also create custom styles and use them with the dataset in a client.

**:arrow_right: Select `BGT Achtergrondvisualisatie (NetherlandsRDNewQuad)`.**

!!! question "Question"

    How can you implement this style in your own application?

??? success "Answer"

    Use `https://api.pdok.nl/lv/bgt/ogc/v1/styles/bgt_achtergrondvisualisatie__netherlandsrdnewquad` plus JSON output (`?f=json`) as needed.

**:arrow_right: View the JSON representation of the style.**

- In `layers`, map layers are defined.
- In `sources`, the source for the style is defined: the BGT OGC API - Tiles.

You have now seen style previews and learned which URL you need to use a style in a client or application.

:material-lightbulb: A dataset can have multiple styles, each tied to one Tile Matrix Set.

:material-lightbulb: If no official style suits your needs, you can create your own style.

**:arrow_right: Return to the landing page**

### Tile Matrix Sets

**:arrow_right: On the landing page, click 'Tile Matrix Sets'**

![Screenshot of the Tile Matrix Sets page](../assets/tiles/tilematrixsets.png)

This page describes the Tile Matrix Sets. A Tile Matrix Set is linked to one map projection because each projection has its own extent, origin, units, and projection behavior.

![alt text](../assets/tiles/tilematrix.png)

A Tile Matrix Set contains multiple Tile Matrices: one per zoom level, forming a pyramid.

![alt text](../assets/tiles/tilematrixset.png)

For BGT OGC API there are three Tile Matrix Sets.

**:arrow_right: Click `NetherlandsRDNewQuad`**

You see a table with all zoom levels in this set. In total there are 16 zoom levels.

!!! question "Question"

    How many tiles does zoom level 16 contain?

??? success "Answer"

    4,294,967,296 (matrix width 65536 × matrix height 65536).

**:arrow_right: Also compare with `WebMercatorQuad`.**

You have now seen the formal description of available Tile Matrix Sets and gained insight into how vector tiles work.

:material-lightbulb: A Tile Matrix Set is a pyramid with zoom levels and one matrix per zoom level.

**:arrow_right: Return to the landing page**

We have now reviewed all pages of the BGT OGC API landing page.

## Summary
In this section, you explored the OGC API landing page (HTML view) in a browser. We reviewed the different pages and their relation to OGC API building blocks.

Hopefully this gave you a clear picture of what an OGC API can do and how to quickly inspect what data is available, specifically for OGC API - Tiles. We used the BGT dataset as example.

| Component             | Explanation                                                                                          |
|-----------------------|------------------------------------------------------------------------------------------------------|
| OpenAPI specification | Swagger UI that shows API capabilities.                                                              |
| Conformance           | Overview of standards this API conforms to.                                                          |
| Tiles                 | Tileset URLs and available projections for this dataset.                                             |
| Styles                | URLs and previews of styles provided by PDOK.                                                        |
| Tile Matrix Sets      | Description of Tile Matrix Sets: zoom levels and tile pixel dimensions.                              |
