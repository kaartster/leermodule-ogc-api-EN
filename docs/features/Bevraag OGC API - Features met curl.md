# Query OGC API - Features with curl

We previously saw how to view API documentation in the browser. Now it is time to actually use the API.
In the command line, you can use `curl` to request and send data. You can use it to query APIs and receive data back. The same applies to PDOK OGC APIs. Responses are returned as JSON.
Developers use this principle to implement APIs in their own applications.

In this section, you use the OpenAPI specification to compose GET requests and query the OGC API - Features of the BGT dataset. Then you execute those requests with `curl` and inspect JSON responses.

## Preparation

**:arrow_right: Open a command line / terminal window.**

!!! warning "Warning"

    Do not use PowerShell for these examples. It has its own built-in `curl` with fewer capabilities.

The OpenAPI specification page makes it easy to compose `curl` commands.

**:arrow_right: Go to the BGT OpenAPI specification.**

![BGT OpenAPI specification](../assets/features/bgt_openapi_specification.png)

## Request the OpenAPI specification

Let’s start with a simple request: retrieving the OpenAPI specification itself.

**:arrow_right: Expand** 'GET `/api` This document' **and execute it.**

![GET /api This document](../assets/get-api.png)

You now see the generated `curl` command and response:

![curl get api specification](../assets/features/get-api-response.png)

One parameter is passed: return JSON.

You can copy this command and run it yourself.

!!! warning "Warning"

    For Windows command line (`cmd.exe`): put command on one line and replace single quotes with double quotes.

For Windows:

```
curl -X "GET" "https://api.pdok.nl/lv/bgt/ogc/v1/api?f=json" -H "accept: */*"
```

## Query collections

### Which collections exist?

Use `GET /collections`.

**:arrow_right: Execute and inspect response.**

For Windows:

```
curl -X "GET" "https://api.pdok.nl/lv/bgt/ogc/v1/collections?f=json" -H "accept: */*"
```

Response body:
```
{
  "links": [ ... ],
  "collections": [ ... ]
}
```

!!! tip

    You can also open these URLs in a browser to inspect JSON.

### Information about one specific collection

Example: ['spoor' collection](https://api.pdok.nl/lv/bgt/ogc/v1/collections/spoor)

![railway example](../assets/features/spoorcollectie.jpg)

For Windows:

```
curl -X "GET" "https://api.pdok.nl/lv/bgt/ogc/v1/collections/spoor?f=json" -H "accept: */*"
```

This returns metadata such as `id`, `title`, `description`, `keywords`, and `extent`.

!!! info "CRS"

    You will also see CRS information. CRS (Coordinate Reference System) determines how geographic coordinates are stored and projected (see also [Background information](../achtergrondinformatie/Wat is geo-informatie.md)). PDOK offers data in multiple CRS values.

### View a collection schema

To inspect available attributes and datatypes, request the schema:

For Windows:

```
curl -X "GET" "https://api.pdok.nl/lv/bgt/ogc/v1/collections/spoor/schema?f=json" -H "accept: */*"
```

**:arrow_right: Execute and inspect the result.**

## Request items

### Request items from a collection

Add `items` to request features:

For Windows:
```
curl -X "GET" "https://api.pdok.nl/lv/bgt/ogc/v1/collections/spoor/items?f=json" -H "accept: */*"
```

A default item limit applies.

Set an explicit limit:

```
curl -X "GET" "https://api.pdok.nl/lv/bgt/ogc/v1/collections/spoor/items?limit=100&f=json" -H "accept: */*"
```

### Request one specific item

If you know the item ID:

For Windows:
```
curl -X "GET" "https://api.pdok.nl/lv/bgt/ogc/v1/collections/spoor/items/7022ff26-12e4-5dc8-9a33-56db2da7e607?f=json" -H "accept: */*"
```

### Request items within a bounding box

Use the `bbox` parameter: `xmin,ymin,xmax,ymax`.

![bounding box on map with coordinates](../assets/features/boundingbox.png)

For Windows:
```
curl -X "GET" "https://api.pdok.nl/lv/bgt/ogc/v1/collections/spoor/items?bbox=4.458132,51.922276,4.478388,51.926696&f=json" -H "accept: */*"
```

**:arrow_right: Find bbox coordinates for your own area using** <http://bboxfinder.com>.

### Request items in a specific CRS

By default, features are returned in CRS84. You can request a different CRS.

Check available CRS values for a collection:

```
curl -X "GET" "https://api.pdok.nl/lv/bgt/ogc/v1/collections/put?f=json"  -H "accept: */*"
```

Then request items in RD/Amersfoort:

```
curl -X "GET" "https://api.pdok.nl/lv/bgt/ogc/v1/collections/spoor/items?crs=http://www.opengis.net/def/crs/EPSG/0/28992&f=json"  -H "accept: */*"
```

## Summary

In this section, you requested the OpenAPI specification, used it to compose API calls, queried collection metadata, and retrieved collection items via command line.

These same calls can be integrated into any application, giving you a solid foundation for the next sections.
