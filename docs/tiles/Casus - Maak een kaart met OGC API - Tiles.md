# Build a map with OGC API – Tiles
We will build a map ourselves using vector tiles and the MapLibre library. MapLibre is a JavaScript library for creating interactive web maps. The goal is not to learn MapLibre itself; we use it to demonstrate how OGC API works.

You will build this map through a case study. First we introduce the case, then you build your own map, and finally you add OGC API - Tiles to your map.

## Case study introduction

How livable is your neighborhood? In this assignment, you create a map that provides insight into the quality of the local living environment.

You can show livability with different map layers. For example: are there enough trees? Are there enough schools nearby? You will map this for the neighborhood where you live.

With geodata you can provide insight into these kinds of questions. PDOK publishes many datasets about the living environment (and other themes) through OGC APIs. Specialists and developers can use those APIs to build maps and viewers that help policy makers, analysts, and residents understand their environment.

In this case study, you work step by step:

1. **Design your web map:** who is it for, what is the goal, which data is needed, and in what form?
2. **Set up a development environment:** prepare your code workspace.
3. **Build a base map viewer:** start with a basemap.
4. **Find suitable tile data:** search and select data sources.
5. **Add tile data to your map:** add map layers to your web map.
6. **Evaluate the final result:** does the map match your design?

Let’s get started.

## Design your web map

A good information product needs a good design. That certainly applies to web maps. Think in advance about the map goal, target audience, and what the audience needs.

Use these design questions:

- **Target audience:** who is the web map for?
- **Goal and scope:** what should the audience achieve with it?
- **Required information:** what data is needed and in what form?
- **Geographic scope and scale:** which area and scale level?

Create a short *design document* that answers these questions.

### Target audience

Different audiences have different needs.

Ask yourself: who is the map for? Experts may need detailed information and can handle jargon. A broader audience usually needs more general information with minimal jargon.

!!! warning "Accessibility"

    Also consider accessibility: should the map be suitable for users with limited digital skills or visual impairments?

!!! tip

    For this fictional assignment, we recommend choosing "interested citizen" as target audience. This broad audience reduces the risk of not finding suitable data while still meeting the learning goals.

**:arrow_right: Record the target audience in your design document.**

### Goal and scope

Ask yourself: what should users achieve with this map? Which questions should it answer? What is the underlying need?

Suppose your goal is: *provide insight into neighborhood livability*. Define what you mean by *insight* and *livability*.

Define scope as well: what is the map intended for, and what is it not intended for?

!!! tip

    For this fictional assignment, we recommend: "provide insight into the quality of the neighborhood living environment."

**:arrow_right: Record goal and scope in your design document.**

### Required information

To help your audience achieve their goal, determine which information is needed and in what form.

- **Information need:** operational information or tactical/strategic information?
- **Aggregation level:** detailed data or aggregated information?
- **Time scale:** current data or multi-year averages?
- **Visualization:** how should data be visualized?

This determines which datasets you select.

!!! warning "Accessibility"

    Also consider visualization accessibility, for example for color blindness.

**:arrow_right: Record required information and form in your design document.**

### Geographic scope and scale

At which scale should your audience use the information? National, municipal, neighborhood?

Scale level also determines whether data should be detailed or abstract.

You can map your own area or another location in the Netherlands.

!!! tip

    For this fictional assignment, we recommend using your own neighborhood.

**:arrow_right: Record geographic scope and scale in your design document.**

## Build your own web map

Now that your design is ready, set up your development environment and start building. Use the example available in this repository as your base.

### Set up a development environment

Prepare an environment where you can develop and test your web map.

If you already cloned this repository in [Analyze an example map](<./Analyseer een voorbeeldkaart.md/#view-the-example-in-a-code-editor>), you can continue there.

=== "VSCode"

    1. Open VSCode.
    2. Click 'Clone Git Repository'.
    3. Use URL: <https://github.com/PDOK/leermodule-ogc-api>
    4. Choose destination and open repository.
    5. Trust authors if prompted.
    6. Example code is in `docs/voorbeelden/tiles`.
    7. Create a new folder and copy the example code there.
    8. Start a local web server:

        ```
        cd %yourfolder
        python -m http.server
        ```

    9. Open `localhost:8000` in your browser.

=== "Classic approach with file manager and text editor"

    1. Go to <https://github.com/PDOK/leermodule-ogc-api>
    2. Download ZIP and extract it.
    3. Example code is in `docs/voorbeelden/tiles`.
    4. Create a new folder and copy example code there.
    5. Start a local web server:

        ```
        cd %yourfolder
        python -m http.server
        ```

    6. Open `localhost:8000` in your browser.

### Build a base map

Modify `index.html` and `main.js` based on your design:

- Web map title
- Basemap and style
- Geographic settings:
    - Initial zoom level
    - Initial center
    - Map bounds

#### Modify index.html

**:arrow_right: Open `index.html`**

**:arrow_right: Change title:**

    <title>Your title</title>

#### Modify main.js

**:arrow_right: Open `main.js`**

    const map = new maplibregl.Map({
    container: 'map', // container id
    style: 'https://api.pdok.nl/kadaster/brt-achtergrondkaart/ogc/v1/styles/standaard__webmercatorquad?f=json', // style URL
    center: [5.44, 52.05], // starting position [lng, lat]
    zoom: 7, // starting zoom level
    minZoom: 6, // minimum zoom level
    maxZoom: 14 // maximum zoom level

For this assignment, we recommend using the WebMercator BRT basemap.

**:arrow_right: Go to <https://api.pdok.nl/kadaster/brt-achtergrondkaart/ogc/v1/styles> and choose a WebMercatorQuad style.**

To center on your own area of interest, use:

**:arrow_right: <https://vibhorsingh.com/boundingbox/>**

Copy center values and update:

    center: [5.44, 52.05]

Set map limits and zoom limits:

    zoom: 7,
    minZoom: 6,
    maxZoom: 14,
    maxBounds: [[5.08530, 52.07246], [5.16769, 52.10060]]

!!! tip

    `maxBounds`, `maxZoom`, and `minZoom` must match each other. You may need trial and error.

!!! question "Question"

    Why can zoom levels differ between <https://vibhorsingh.com/boundingbox/> and your own web map?

??? success "Answer"

    The bounding box tool uses XYZ Mapbox tiles with a different tiling scheme (for example 512×512 tiles instead of 256×256).

### Find suitable vector tile data

Now add thematic layers. Based on your design, find suitable datasets.

We focus specifically on **PDOK vector tiles**.

Useful sources:

- [Nationaal Georegister](https://www.nationaalgeoregister.nl/)
- [PDOK.nl](https://www.pdok.nl/)

In NGR, apply filters:

1. Organization: **Beheer PDOK**
2. Source type: **service**
3. Online source: **OGC:API tiles**

This gives all PDOK OGC API - Tiles services.

!!! info

    The number of available datasets can change over time.

Then evaluate datasets against your design:

- Is the dataset suitable for your audience?
- Is the content relevant for your goal?
- Is the data form suitable?
- Is scale and geographic extent suitable?

Find either a Tile Set URL or Style URL and add it to your map.

### Add vector tile data to your map

There are two methods:

1. Add individual layers
2. Use a style

#### Add vector tiles as individual layers

From landing page → Tiles:

- Select `WebMercatorQuad`
- Click `View metadata`
- Open `JSON`
- Copy URL

Add this to `main.js`:

    map.on('load', () => {
        map.addSource('top10nl', {
            type: 'vector',
            url:
                'https://api.pdok.nl/brt/top10nl/ogc/v1/tiles/WebMercatorQuad?f=tilejson'
        });
        map.addLayer({
            'id': 'gebouw_vlak',
            'type': 'fill',
            'source': 'top10nl',
            'source-layer': 'gebouw_vlak',
            'paint': {
                'fill-color': '#ff0000ff'
            }
        });
    });

!!! info "Zoom level"

    Check in which zoom levels the tileset is available: <https://api.pdok.nl/brt/top10nl/ogc/v1/tiles/WebMercatorQuad>

How to find available source-layer names:

1. Check available feature collections (if OGC API - Features exists)
2. Inspect a style JSON (`"layers"`)
3. Open style in a GIS client like QGIS

#### Add vector tiles via a style

In `main.js`, style is configured as:

    style: 'https://api.pdok.nl/kadaster/brt-achtergrondkaart/ogc/v1/styles/standaard__webmercatorquad?f=json', // style URL

You can replace this with:

1. An existing style
2. A modified existing style
3. A new custom style

For example, local style file:

    style: './yourstyle.json', // style URL

A sample style is provided in [style_voorbeeld.json](../voorbeelden/tiles/style_voorbeeld.json).

For custom styles, use MapLibre style documentation: <https://maplibre.org/maplibre-style-spec/>

Geometry type mapping:

| Geometry type | MapLibre style spec type |
| --- | --- |
| Point | `symbol` or `circle` |
| LineString | `line` |
| Polygon | `fill` (or `line` for outline only) |

#### Summary: adding layers

| Method | Option | Description |
| --- | --- | --- |
| Add individual layers |  | Add a source and layers in `main.js`; can be used on top of an existing style |
| Add layers via style | Ready-made style | Use URL of an existing style |
|  | Modify existing style | Copy and edit an existing style, host it, and reference it in `main.js` |
|  | New style | Create and host a new style, then reference it in `main.js` |

#### Assignment: add your own layers

**:arrow_right: Add at least 4 extra layers**

**:arrow_right: Including at least:**

- **1 point layer (`symbol` or `circle`)**
- **1 line layer (`line`)**
- **1 polygon layer (`fill`)**

**:arrow_right: Use at least 3 different colors**

Use your design to decide which layers to add.

### Optional: extra functionality

!!! info "This section is optional"

Add extra functionality to your web map. See MapLibre docs:

- [MapLibre GL JS API](<https://maplibre.org/maplibre-gl-js/docs/API/>)
- [MapLibre GL JS examples](<https://maplibre.org/maplibre-gl-js/docs/examples/>)
- [Plugins for MapLibre GL JS](<https://maplibre.org/maplibre-gl-js/docs/plugins/>)

Examples:

- [Legend](<https://github.com/watergis/maplibre-gl-legend>)
- [Popups](<https://maplibre.org/maplibre-gl-js/docs/examples/attach-a-popup-to-a-marker-instance/>)
- [Controls](<https://github.com/korywka/mapbox-controls>)

## Evaluate the final result

Compare your final map to your original design:

- **Target audience:** is your map suitable for your intended audience?
- **Goal and scope:** can users achieve the intended goal?
- **Required information:** does your map contain suitable information in the right form?
- **Geographic scope and scale:** is your data appropriate for the intended scale?

In short: does your map help users answer their questions and provide real value?

**:arrow_right: Evaluate your final product and adjust where needed.**

## Conclusion

You have now built a web map with vector tiles. Congratulations!

| Component | Description |
| --- | --- |
| Design your web map | Define audience, goal, data needs, and geographic scope |
| Set up environment | Prepare and copy code |
| Build a base map | Configure base `index.html` and `main.js` |
| Find vector tile data | Select suitable datasets via NGR/PDOK |
| Add vector tile data | Add individual layers and/or styles |
| Evaluate result | Check whether final map matches design |
