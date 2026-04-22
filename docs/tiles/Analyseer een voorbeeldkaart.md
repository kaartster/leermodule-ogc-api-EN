# Analyze an example map

You just explored what you can do with OGC API - Tiles through the landing page. Now we look at an example web map built with OGC API - Tiles. This helps you understand how a web map works and how OGC API - Tiles components work together.

## View the example in a browser

First, we view the example web map in a browser.

**:arrow_right: Open** [../voorbeelden/tiles/index.html](../voorbeelden/tiles/index.html)

**:arrow_right: Open the map itself and zoom in and out**

This is a web viewer built with the MapLibre library. This map uses the BRT Background Map OGC API – Tiles: <https://api.pdok.nl/kadaster/brt-achtergrondkaart/ogc/v1>

??? info "What is BRT?"

    BRT stands for Basisregistratie Topografie (Topography Registry). Do not confuse it with BGT: Basisregistratie *Grootschalige* Topografie. BRT is intended for small-scale topography: scale 1:250,000 to 1:10,000. That makes BRT ideal as a basemap.

    BRT is a base registry. [More information about base registries can be found here](<../achtergrondinformatie/Wat is geo-informatie.md/#base-registries>).

![BRT Background Map](../assets/tiles/brtachtergrondkaart.png)

!!! question "Question"

    What changes when you zoom in and out on the map?

??? success "Answer"

    When zooming in, new map tiles are loaded. You should see tiles appear one by one very quickly.

**:arrow_right: Open developer tools in your browser.**

**:arrow_right: Refresh the page**

**:arrow_right: Open the Network tab**

**:arrow_right: Look at the requests that appear in the Network tab**

Notice that among others `main.js` and `https://api.pdok.nl/kadaster/brt-achtergrondkaart/ogc/v1/styles/standaard__webmercatorquad?f=json` are loaded.

![Files being loaded: main.js and standaard__webmercatorquad?f=json](../assets/tiles/initial_requests.png)

**:arrow_right: Zoom in and out**

Notice that many files are now loaded, for example `262?f=mvt`. This file is one tile. The full URL for this tile is: <https://api.pdok.nl/kadaster/brt-achtergrondkaart/ogc/v1/tiles/WebMercatorQuad/9/168/262?f=mvt>

![Tile files being loaded](../assets/tiles/tile-requests.png)

You can now see this web viewer uses the BRT Background Map, and specifically the WebMercatorQuad TileMatrixSet. You can tell this from the tile URLs. You can also see the default style is used for this tile matrix set from the style URL loaded after `main.js`: <https://api.pdok.nl/kadaster/brt-achtergrondkaart/ogc/v1/styles/standaard__webmercatorquad?f=json>

**:arrow_right: Look up this TileMatrixSet and Style via the landing page in your browser:** <https://api.pdok.nl/kadaster/brt-achtergrondkaart/ogc/v1>

!!! question "Question"

    Where can you find the URL of the TileMatrixSet and Style used in the example?

??? success "Answer"

    You can find the TileMatrixSet URL on the [Tiles page](<https://api.pdok.nl/kadaster/brt-achtergrondkaart/ogc/v1/tiles>) under 'URL template', by selecting 'WebMercatorQuad' in the dropdown.

    You can find the Style URL on the [Styles page](<https://api.pdok.nl/kadaster/brt-achtergrondkaart/ogc/v1/styles>) under 'URL', by selecting 'BRT Achtergrondkaart Standaard (WebMercatorQuad)' in the dropdown.

So for the tile source, the following URL template is used:

```
https://api.pdok.nl/kadaster/brt-achtergrondkaart/ogc/v1/tiles/WebMercatorQuad/
{z}/{y}/{x}?f=mvt
```

MapLibre translates this into one request per tile. Such a request looks like:

```
https://api.pdok.nl/kadaster/brt-achtergrondkaart/ogc/v1/tiles/WebMercatorQuad/
9/168/262?f=mvt
```

How is this URL structured?

| Template                                                    | Example                                                     | Description                                                                          |
|-------------------------------------------------------------|-------------------------------------------------------------|--------------------------------------------------------------------------------------|
| `https://api.pdok.nl/kadaster/brt-achtergrondkaart/ogc/v1/` | `https://api.pdok.nl/kadaster/brt-achtergrondkaart/ogc/v1/` | Landing page                                                                         |
| `tiles`                                                     | `tiles`                                                     | Dataset tileset                                                                      |
| `{tileMatrixSetId}`                                         | `WebMercatorQuad`                                           | Name of the TileMatrixSet                                                            |
| `{tileMatrix}`                                              | `9`                                                         | Matrix number (zoom level)                                                           |
| `{tileRow}`                                                 | `168`                                                       | Tile row number (position in the matrix)                                             |
| `{tileCol}`                                                 | `262`                                                       | Tile column number (position in the matrix)                                          |
| `f=mvt`                                                     | `f=mvt`                                                     | Tile output format. In this case Mapbox vector tile (mvt)                           |

Read the [previous chapter](<./Verken OGC API - Tiles in de browser.md/#tile-matrix-sets>) again if this is not fully clear yet.

For more information, see [the OGC API workshop](<https://ogcapi-workshop.ogc.org/api-deep-dive/tiles/>).

## View the example in a code editor

Now we will inspect the code closely. Use a code editor or IDE of your choice to view and run code. Below are instructions for Visual Studio Code, but you can use another option.

**:arrow_right: Fork the Git repository**

**:arrow_right: Clone the Git repository**

**:arrow_right: Open the repository**

Let’s run this code first so we can see the application in a browser:

**:arrow_right: Start a local web server, for example with Python:**

```
> python -m http.server
Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
```
**:arrow_right: Now open** [../voorbeelden/tiles/index.html](../voorbeelden/tiles/index.html) **in your browser**

![example map built with maplibre](../assets/tiles/brtachtergrondkaart.png)

Now let’s inspect the code in an editor:

**:arrow_right: View** `..\voorbeelden\tiles\index.html`

**:arrow_right: View** `..\voorbeelden\tiles\main.js`

**:arrow_right: View** <https://api.pdok.nl/kadaster/brt-achtergrondkaart/ogc/v1/styles/standaard__webmercatorquad?f=json>

In `index.html`, you should see a `div` with id `map`.

In `main.js`, `container` refers to the same `map`. In this JavaScript file, the `maplibre-gl` library is imported first. Then the map is defined:

| Variable    | Description                                                                                                                                                                                        |
|-------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `container` | `map` object in `index.html`                                                                                                                                                                       |
| `style`     | points to a json file defining how tiles are visualized <br> <https://api.pdok.nl/kadaster/brt-achtergrondkaart/ogc/v1/styles/standaard__webmercatorquad?f=json>                              |
| `center`    | defines the initial center of the map (x and y coordinates)                                                                                                                                        |
| `zoom`      | defines the initial zoom level                                                                                                                                                                      |
| `minZoom`   | defines the maximum level users can zoom out                                                                                                                                                        |
| `maxZoom`   | defines the maximum level users can zoom in                                                                                                                                                         |

Notice that you do not directly see the tile URL in `main.js`. That URL is referenced in the `style json`. `main.js` calls the style json, and the style json then calls the tile source. The style json also determines how those tiles are rendered.
The tile source in this case is <https://api.pdok.nl/kadaster/brt-achtergrondkaart/ogc/v1/tiles/WebMercatorQuad/{z}/{y}/{x}?f=mvt>

**:arrow_right: Find the tiles URL (the source) in the** `style json`.

!!! note "Want to know more?"

    See the deep dive at <https://ogcapi-workshop.ogc.org/api-deep-dive/tiles/>

**:arrow_right: Look again at** the `style json`: <https://api.pdok.nl/kadaster/brt-achtergrondkaart/ogc/v1/styles/standaard__webmercatorquad?f=json>

This is a very extensive style and therefore a large JSON file. How is it structured?

First, the source is defined: on which URL are the tiles? In this case: <https://api.pdok.nl/kadaster/brt-achtergrondkaart/ogc/v1/tiles/WebMercatorQuad/{z}/{y}/{x}?f=mvt>, but it can be any location. A `style json` can call one or multiple tilesets as source.

Then layers in that tileset are defined, for example map layers such as water or roads.

Finally, the file defines how those layers are displayed (colors, line widths, etc.). MapLibre reads and renders this.

**:arrow_right: View** `main.js` **again**

In this case, the `style json` is on an external location, but it can also be a file on your own server.
In this case, the `style json` is provided by PDOK, but you can also create your own `style json` file. The example is a large style file, but simpler styles are also possible.

### Experiment with the viewer

Try experimenting with variables in `main.js`. Enter some values and see what these variables do.

**:arrow_right: In** `main.js`, **adjust the following values and observe what happens in your web map:**

- `center`
- `zoom`
- `minZoom`
- `maxZoom`

??? hint "Hint: what values are useful for each variable?"

    | Variable | Example | Description |
    |---|---|---|
    | `center` | `[5.9623,52.2118]` for Kadaster headquarters | Center coordinates in Long-Lat coordinates (watch the order). You can look this up via <https://vibhorsingh.com/boundingbox/> |
    | `zoom` | `0` to `22` | Initial zoom level (when user opens the web map) |
    | `minZoom` | `0` to `22` | Maximum zoom-out level |
    | `maxZoom` | `0` to `22` | Maximum zoom-in level |

Read more in [MapLibre documentation](https://maplibre.org/maplibre-gl-js/docs/API/type-aliases/MapOptions).

Hopefully by experimenting you discovered what these parameters do.

## Summary

You have now viewed and analyzed an example map. The example map used the BRT Background Map with the default WebMercator style. You saw how MapLibre can render OGC API vector tiles. You also saw which components are needed:

| Name       | Example                                                                                              | Description                                                  |
|------------|------------------------------------------------------------------------------------------------------|--------------------------------------------------------------|
| Index      | `index.html`                                                                                         | HTML code for base structure.                                |
| JavaScript | `main.js`                                                                                            | JavaScript code for web map functionality.                   |
| Style      | <https://api.pdok.nl/kadaster/brt-achtergrondkaart/ogc/v1/styles/standaard__webmercatorquad?f=json> | Styling of tiles. Calls one or more tilesets.               |
| Tileset    | `https://api.pdok.nl/kadaster/brt-achtergrondkaart/ogc/v1/tiles/WebMercatorQuad/{z}/{y}/{x}?f=mvt` | Tile source.                                                 |
